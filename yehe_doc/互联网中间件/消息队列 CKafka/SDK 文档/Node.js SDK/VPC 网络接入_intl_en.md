## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Node.js in a VPC.

## Prerequisites

- [Install GCC](https://gcc.gnu.org/install/)
- [Install Node.js](https://nodejs.org/en/download/)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/nodejskafkademo/VPC)

## Directions

### Preparations

1. Upload the `nodejskafkademo` in the downloaded demo to the Linux server.
2. Log in to the Linux server and enter the `nodejskafkademo` directory.

### Step 1. Install the C++ dependency library

1. Run the following command to switch to the `yum` source configuration directory `/etc/yum.repos.d/`.

   ```bash
   cd /etc/yum.repos.d/
   ```

2. Create the `yum` source configuration file `confluent.repo`.

   ```bash
   [Confluent.dist]
   name=Confluent repository (dist)
   baseurl=https://packages.confluent.io/rpm/5.1/7
   gpgcheck=1
   gpgkey=https://packages.confluent.io/rpm/5.1/archive.key
   enabled=1   
   [Confluent]
   name=Confluent repository
   baseurl=https://packages.confluent.io/rpm/5.1
   gpgcheck=1
   gpgkey=https://packages.confluent.io/rpm/5.1/archive.key
   enabled=1
   ```

3. Run the following command to install the C++ dependency library.

   ```bash
   yum install librdkafka-devel
   ```


### Step 2. Install the Node.js dependency library

1. Run the following command to specify the OpenSSL header file path for the preprocessor.

   ```bash
   export CPPFLAGS=-I/usr/local/opt/openssl/include
   ```

2. Run the following command to specify the OpenSSL library path for the connector.

   ```bash
   export LDFLAGS=-L/usr/local/opt/openssl/lib
   ```

3. Run the following command to install the Node.js dependency library.

   ```bash
   npm install i --unsafe-perm node-rdkafka
   ```


### Step 3. Prepare the configurations

Create the CKafka configuration file `setting.js`.

```js
module.exports = {
    'bootstrap_servers': ["xxx.ckafka.tencentcloudmq.com:6018"],
    'topic_name': 'xxx',
    'group_id': 'xxx'
}
```

| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| bootstrap_servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/88b29cffdf22e3a0309916ea715057a1.png) |
| topic_name          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |
| group_id          | You can customize it. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |

### Step 4. Send a message

1. Write the message production program `producer.js`.
```
const Kafka = require('node-rdkafka');
      const config = require('./setting');
      console.log("features:" + Kafka.features);
      console.log(Kafka.librdkafkaVersion);
      
      var producer = new Kafka.Producer({
          'api.version.request': 'true',
          // To set the entry service, please get the corresponding service address in the console
          'bootstrap.servers': config['bootstrap_servers'],
          'dr_cb': true,
          'dr_msg_cb': true,
      
          // Number of retries upon request error. We recommend you set the value to be greater than 0. Retries can ensure as much as possible that the message will not be lost
          'retries': '0',
          // The time between when a request fails and the next time the request is retried
          "retry.backoff.ms": 100,
          // Timeout period of the producer network request
          'socket.timeout.ms': 6000,
      });
      
      var connected = false
      
      producer.setPollInterval(100);
      
      producer.connect();
      
      producer.on('ready', function() {
      connected = true
      console.log("connect ok")
      });
      
      producer.on("disconnected", function() {
      connected = false;
      producer.connect();
      })
      
      producer.on('event.log', function(event) {
          console.log("event.log", event);
      });
      
      producer.on("error", function(error) {
          console.log("error:" + error);
      });
      
      function produce() {
          try {
              producer.produce(
              config['topic_name'],   
              null,      
              new Buffer('Hello CKafka Default'),      
              null,   
              Date.now()
              );
          } catch (err) {
              console.error('Error occurred when sending message(s)');
              console.error(err);
          }
      
      }
      
      producer.on('delivery-report', function(err, report) {
          console.log("delivery-report: producer ok");
      });
      
      producer.on('event.error', function(err) {
          console.error('event.error:' + err);
      })
      
      setInterval(produce, 1000, "Interval");
```

2. Run the following command to send the message.

   ```bash
   node producer.js
   ```

3. View the operation result.
   ![](https://main.qcloudimg.com/raw/195f4aee06ba86755407b4a75812c256.png)

4. On the **Topic Management** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic and click **More** > **Message Query** to view the just sent message.
   ![](https://main.qcloudimg.com/raw/e20a0809942f90e0efd5fd1f217574b0.png)

### Step 5. Subscribe to a message

1. Create the message consumer program `consumer.js`.
```
const Kafka = require('node-rdkafka');
      const config = require('./setting');
      console.log(Kafka.features);
      console.log(Kafka.librdkafkaVersion);
      console.log(config)
      
      var consumer = new Kafka.KafkaConsumer({
          'api.version.request': 'true',
          // To set the entry service, please get the corresponding service address in the console
          'bootstrap.servers': config['bootstrap_servers'],
          'group.id' : config['group_id'],
      
          // Consumer timeout period when the Kafka consumer grouping mechanism is used. If the broker does not receive the heartbeat of the consumer within this period,
          // the consumer will be considered to have failed and the broker will initiate rebalance
          'session.timeout.ms': 10000,
          // Client request timeout period. If no response is received after this time elapses, the request will time out and fail
          'metadata.request.timeout.ms': 305000,
          // Set the internal retry interval of the client
          'reconnect.backoff.max.ms': 3000
      
      });
      
      consumer.connect();
      
      consumer.on('ready', function() {
      console.log("connect ok");
      consumer.subscribe([config['topic_name']]);
      consumer.consume();
      })
      
      consumer.on('data', function(data) {
      console.log(data);
      });
      
      consumer.on('event.log', function(event) {
          console.log("event.log", event);
      });
      
      consumer.on('error', function(error) {
          console.log("error:" + error);
      });
      
      consumer.on('event', function(event) {
              console.log("event:" + event);
      });
```


2. Run the following command to consume the message.

   ```bash
   node consumer.js
   ```

3. View the operation result.
   ![](https://main.qcloudimg.com/raw/deecbf58c00e07531b4ea703c4046b46.png)

4. On the **Consumer Group** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name in **Topic Name**, and click **Query Details** to view the consumption details.
   ![](https://main.qcloudimg.com/raw/3020dcb5f8fd73e02949b20fef4f956f.png)
