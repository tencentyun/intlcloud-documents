## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Node.js through SASL_PLAINTEXT over public network.

## Prerequisites

- [Install GCC](https://gcc.gnu.org/install/)
- [Install Node.js](https://nodejs.org/en/download/)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/nodejskafkademo/PUBLIC_SASL)

## Directions

### Step 1. Install the C++ dependent library

1. Run the following command to switch to the `yum` source configuration directory `/etc/yum.repos.d/`.

   ```bash
   cd /etc/yum.repos.d/
   ```

2. Create the `yum` source configuration file `confluent.repo`.

   ```
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

3. Run the following command to install the C++ dependent library.

   ```bash
   yum install librdkafka-devel
   ```

### Step 2. Install the Node.js dependent library

1. Run the following command to specify the OpenSSL header file path for the preprocessor.

   ```bash
   export CPPFLAGS=-I/usr/local/opt/openssl/include
   ```

2. Run the following command to specify the OpenSSL library path for the connector.

   ```bash
   export LDFLAGS=-L/usr/local/opt/openssl/lib
   ```

3. Run the following command to install the Node.js dependent library.

   ```bash
   npm install i --unsafe-perm node-rdkafka
   ```

### Step 3. Prepare configurations

Create the CKafka configuration file `setting.js`.

```js
module.exports = {
    'sasl_plain_username': 'ckafka-xxxxxxx#ckafkademo',
    'sasl_plain_password': 'ckafkademo123',
    'bootstrap_servers': ["xxx.ckafka.tencentcloudmq.com:6018"],
    'topic_name': 'xxx',
    'group_id': 'xxx'
}
```


| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| sasl_plain_username | Username in the format of `instance ID` + `#` + `username`. The instance ID can be obtained in **Basic Info** on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), and the username is set when the user is created in **User Management** |
| sasl_plain_password | User password, which is set when the user is created in **User Management** on the instance details page in the CKafka console. |
| bootstrap_servers | SASL access point, which can be obtained in **Basic Info** > **Access Mode** on the instance details page in the CKafka console.![img](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| topic_name | Topic name, which can be created and obtained in **Topic Management** on the instance details page in the CKafka console. <br/>![img](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |
| group_id          | Consumer group ID, which can be customized based on business requirements.                            |

### Step 4. Send messages

1. Write a message production program named `producer.js`.
   <dx-codeblock>
   :::  js
   const Kafka = require('node-rdkafka');
   const config = require('./setting');
   console.log("features:" + Kafka.features);
   console.log(Kafka.librdkafkaVersion);

   var producer = new Kafka.Producer({
       'api.version.request': 'true',
       'bootstrap.servers': config['bootstrap_servers'],
       'dr_cb': true,
       'dr_msg_cb': true,
       'security.protocol' : 'SASL_PLAINTEXT',
       'sasl.mechanisms' : 'PLAIN',
       'sasl.username' : config['sasl_plain_username'],
       'sasl.password' : config['sasl_plain_password']
   });

   var connected = false

   producer.setPollInterval(100);

   producer.connect();

   producer.on('ready', function() {
   connected = true
   console.log("connect ok")

   });

   function produce() {
   try {
       producer.produce(
       config['topic_name'],
       new Buffer('Hello CKafka SASL'),
       null,
       Date.now()
       );
   } catch (err) {
       console.error('Error occurred when sending message(s)');
       console.error(err);
   }
   }

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

   producer.on('delivery-report', function(err, report) {
       console.log("delivery-report: producer ok");
   });
   // Any errors we encounter, including connection errors
   producer.on('event.error', function(err) {
       console.error('event.error:' + err);
   })

   setInterval(produce,1000,"Interval");
   :::
   </dx-codeblock>


2. Execute the following command to send messages.

   ```bash
   node producer.js
   ```

3. View the execution result.
   ![](https://main.qcloudimg.com/raw/195f4aee06ba86755407b4a75812c256.png)

4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the target topic, and click **More** > **Message Query** to view the message just sent.
   ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)

### Step 5. Subscribe to messages

1. Create a message consumption program named `consumer.js`.
   <dx-codeblock>
   :::  js
    consumer.on('event.log', function(event) {
       console.log("event.log", event);
   });

   consumer.on('error', function(error) {
       console.log("error:" + error);
   });

   consumer.on('event', function(event) {
           console.log("event:" + event);
   });const Kafka = require('node-rdkafka');
   const config = require('./setting');
   console.log(Kafka.features);
   console.log(Kafka.librdkafkaVersion);
   console.log(config)

   var consumer = new Kafka.KafkaConsumer({
       'api.version.request': 'true',
       'bootstrap.servers': config['bootstrap_servers'],
       'security.protocol' : 'SASL_PLAINTEXT',
       'sasl.mechanisms' : 'PLAIN',
       'message.max.bytes': 32000,
       'fetch.message.max.bytes': 32000,
       'max.partition.fetch.bytes': 32000,
       'sasl.username' : config['sasl_plain_username'],
       'sasl.password' : config['sasl_plain_password'],
       'group.id' : config['group_id']
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
   :::
   </dx-codeblock>


2. Execute the following command to send messages.

   ```bash
   node consumer.js
   ```

3. View the execution result.
   ![](https://main.qcloudimg.com/raw/deecbf58c00e07531b4ea703c4046b46.png)

4. On the **Consumer Group** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group name, enter the topic name, and click **Query Details** to view the consumption details.
  ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
