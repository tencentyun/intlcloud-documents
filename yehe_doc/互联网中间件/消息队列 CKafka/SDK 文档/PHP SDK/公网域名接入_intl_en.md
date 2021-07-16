## Overview

This document describes how to access CKafka to send/receive messages with the SDK for PHP over the public network.

## Prerequisites

- [Install librdkafka](https://github.com/edenhill/librdkafka/)
- [Install PHP 5.6 or above](https://www.php.net/manual/en/install.php)
- [Install PEAR](https://pear.php.net/manual/en/installation.getting.php)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/phpkafkademo/gongwang)

## Directions

### Step 1. Add the Rdkafka extension

1. Find the latest version of Rdkafka extension package for PHP [here](http://pecl.php.net/package/rdkafka).
   >?Different package versions require different PHP versions. 4.1.2 is used here as an example.

2. Install the Rdkafka extension.
   ```bash
   wget --no-check-certificate https://pecl.php.net/get/rdkafka-4.1.2.tgz
   pear install rdkafka-4.1.2.tgz
   # If the installation succeeds, the system will prompt "install ok" and "You should add "extension=rdkafka.so" to php.ini"
   # If the installation fails and the system prompts `could not extract the package.xml file from "rdkafka-4.1.2.tgz"`, please decompress the package manually, copy the `package.xml` file into the `rdkafka` directory, and run `pear install package.xml` to install it
   # For other errors, please follow the prompts to troubleshoot
   # After successful installation, add `extension=rdkafka.so` to `php.ini`
   # After `php --ini` is executed, `Loaded Configuration File:` shows the location of `php.ini` 
   echo 'extension=rdkafka.so' >> /etc/php.ini
   ```

### Step 2. Prepare configurations

Create the configuration file `CKafkaSetting.php`.
```php
<?php
return [
    'bootstrap_servers' => 'bootstrap_servers1:port,bootstrap_servers2:port',
    'topic_name' => 'topic_name',
    'group_id' => 'php-demo',
    'ckafka_instance_id' => 'ckafka_instance_id',
    'sasl_username' => 'username',
    'sasl_password' => 'password'
];
```

| Parameter | Description |
| ------------------ | ------------------------------------------------------------ |
| bootstrap_servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/c5cf200a66f6dcf627d2ca6f1c747ecf.png) |
| topic_name          | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |
| group_id          | Consumer group ID. You can customize it according to your business needs. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |
| ckafka_instance_id | Instance ID, which can be obtained in **Basic Info** on the **Instance Details** page in the CKafka console.<br/>![](https://main.qcloudimg.com/raw/9c417da4953669372fa4c13973096d3b.png) |
| sasl_username    | Username, which is set when the user is created on the **User Management** page in the console.             |
| sasl_password    | Password, which is set when the user is created on the **User Management** page in the console.             |



### Step 3. Send a message

1. Write the message production program `Producer.php`.
  ```php
<?php

$setting = require __DIR__ . '/CKafkaSetting.php';

$conf = new RdKafka\Conf();
// To set the entry service, please get the corresponding service address in the console
$conf->set('bootstrap.servers', $setting['bootstrap_servers']);
// ---------- You need to set the following when enabling SASL authentication ----------
// The SASL authentication mechanism type is `PLAIN` by default
$conf->set('sasl.mechanism', 'PLAIN');
// Set the username: instance ID + # + username configured in **User Management**
$conf->set('sasl.username', $setting['ckafka_instance_id'] . '#' . $setting['sasl_username']);
// Set the password: the password configured in **User Management**
$conf->set('sasl.password', $setting['sasl_password']);
// Configure an ACL policy locally.
$conf->set('security.protocol', 'SASL_PLAINTEXT');
// ---------- You need to set the following when enabling SASL authentication ----------
// There are three ack mechanisms for a Kafka producer as described below:
// -1 or all: the broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and syncs it to the followers in all ISRs.
// This configuration provides the highest data reliability, and messages will never be lost as long as one synced replica survives. Note: this configuration cannot ensure that replicas will be returned after the data is written to all of them.
// It can be used together with the `min.insync.replicas` parameter at the topic level.
// 0: the producer does not wait for acknowledgment of sync completion from the broker before it continues to send the next message or next batch of messages. This configuration has the highest production performance but lowest data reliability.
// (Data loss may occur when the server fails. If the leader is dead but the producer is unaware of that, the broker cannot receive messages.)
// 1: the producer sends the next message or next batch of messages after it receives an acknowledgment that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability.
// (Messages may be lost if the leader is dead but has not been replicated yet.)
// If you do not explicitly configure this, the value of 1 will be used by default. You can customize this according to your business conditions
$conf->set('acks', '1');
// Number of retries upon request error. We recommend you set the value to be greater than 0. Retries can ensure as much as possible that the message will not be lost
$conf->set('retries', '0');
// The time between when a request fails and the next time the request is retried
$conf->set('retry.backoff.ms', 100);
// Timeout period of the producer network request
$conf->set('socket.timeout.ms', 6000);
$conf->set('reconnect.backoff.max.ms', 3000);

// Register the callback for message sending
$conf->setDrMsgCb(function ($kafka, $message) {
    echo '[Producer] sent a message: message=' . var_export($message, true) . "\n";
});
// Register the callback for message sending error
$conf->setErrorCb(function ($kafka, $err, $reason) {
    echo "[Producer] run into an error while sending the message: err=$err reason=$reason \n";
});

$producer = new RdKafka\Producer($conf);
// Please set `LOG_DEBUG` when debugging
//$producer->setLogLevel(LOG_DEBUG);
$topicConf = new RdKafka\TopicConf();
$topic = $producer->newTopic($setting['topic_name'], $topicConf);
// Produce a message and send it
for ($i = 0; $i < 5; $i++) {
    // `RD_KAFKA_PARTITION_UA` lets Kafka select a partition freely
    $topic->produce(RD_KAFKA_PARTITION_UA, 0, "Message $i");
    $producer->poll(0);
}

while ($producer->getOutQLen() > 0) {
    $producer->poll(50);
}

echo "[Producer] sent the message successfully\n";
  ```

2. Run `Producer.php` to send the message.
```bash
php Producer.php
```

3. View the operation result.
  ```bash
>[Producer] sent a message: message=RdKafka\Message::__set_state(array(
>   'err' => 0,
>   'topic_name' => 'topic_name',
>   'timestamp' => 1618800895159,
>   'partition' => 0,
>   'payload' => 'Message 0',
>   'len' => 9,
>   'key' => NULL,
>   'offset' => 0,
>   'headers' => NULL,
>))
>[Producer] sent a message: message=RdKafka\Message::__set_state(array(
>   'err' => 0,
>   'topic_name' => 'topic_name',
>   'timestamp' => 1618800895159,
>   'partition' => 0,
>   'payload' => 'Message 1',
>   'len' => 9,
>   'key' => NULL,
>   'offset' => 1,
>   'headers' => NULL,
>))

...

>[Producer] sent the message successfully
  ```

4. On the **Topic Management** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic and click **More** > **Message Query** to view the just sent message.
![](https://main.qcloudimg.com/raw/c18f71eecfa5f2d9ef9df19b7eb876fc.png)


### Step 4. Consume the message

1. Write the subscribe message consumer program `Consumer.php`.
  ```php
<?php

$setting = require __DIR__ . '/CKafkaSetting.php';

$conf = new RdKafka\Conf();
$conf->set('group.id', $setting['group_id']);
// To set the entry service, please get the corresponding service address in the console
$conf->set('bootstrap.servers', $setting['bootstrap_servers']);
// ---------- You need to set the following when enabling SASL authentication ----------
// The SASL authentication mechanism type is `PLAIN` by default
$conf->set('sasl.mechanism', 'PLAIN');
// Set the username: instance ID + # + username configured in **User Management**
$conf->set('sasl.username', $setting['ckafka_instance_id'] . '#' . $setting['sasl_username']);
// Set the password: the password configured in **User Management**
$conf->set('sasl.password', $setting['sasl_password']);
// Configure an ACL policy locally.
$conf->set('security.protocol', 'SASL_PLAINTEXT');
// ---------- You need to set the following when enabling SASL authentication ----------
// Consumer timeout period when the Kafka consumer grouping mechanism is used. If the broker does not receive the heartbeat of the consumer within this period,
// the consumer will be considered to have failed and the broker will initiate rebalance
$conf->set('session.timeout.ms', 10000);
// Client request timeout period. If no response is received after this time elapses, the request will time out and fail
$conf->set('request.timeout.ms', 305000);
// Set the internal retry interval of the client
$conf->set('reconnect.backoff.max.ms', 3000);

$topicConf = new RdKafka\TopicConf();
#$topicConf->set('auto.commit.interval.ms', 100);
// Offset reset policy. Please set as appropriate according to the business scenario. Improper setting may result in the loss of consumed data.
$topicConf->set('auto.offset.reset', 'earliest');
$conf->setDefaultTopicConf($topicConf);

$consumer = new RdKafka\KafkaConsumer($conf);
// Please set `LOG_DEBUG` when debugging
//$consumer->setLogLevel(LOG_DEBUG);
$consumer->subscribe([$setting['topic_name']]);

$isConsuming = true;
while ($isConsuming) {
    $message = $consumer->consume(10 * 1000);
    switch ($message->err) {
        case RD_KAFKA_RESP_ERR_NO_ERROR:
            echo "[Consumer] received a message:" . var_export($message, true) . "\n";
            break;
        case RD_KAFKA_RESP_ERR__PARTITION_EOF:
            echo "[Consumer] is waiting for messages\n";
            break;
        case RD_KAFKA_RESP_ERR__TIMED_OUT:
            echo "[Consumer] waiting timed out\n";
            $isConsuming = false;
            break;
        default:
            throw new \Exception($message->errstr(), $message->err);
            break;
    }
}
  ```


2. Run `Consumer.php` to consume the message.
```bash
php Consumer.php
```

3. View the operation result.
  ```bash
  >[Consumer] received a message: RdKafka\Message::__set_state(array(
  >   'err' => 0,
  >   'topic_name' => 'topic_name',
  >   'timestamp' => 1618800895159,
  >   'partition' => 0,
  >   'payload' => 'Message 0',
  >   'len' => 9,
  >   'key' => NULL,
  >   'offset' => 0,
  >   'headers' => NULL,
  >))
  >[Consumer] received a message: RdKafka\Message::__set_state(array(
  >   'err' => 0,
  >   'topic_name' => 'topic_name',
  >   'timestamp' => 1618800895159,
  >   'partition' => 0,
  >   'payload' => 'Message 1',
  >   'len' => 9,
  >   'key' => NULL,
  >   'offset' => 1,
  >   'headers' => NULL,
  >))
  
  ...
  ```

4. On the **Consumer Group** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name in **Topic Name**, and click **Query Details** to view the consumption details.
![](https://main.qcloudimg.com/raw/3020dcb5f8fd73e02949b20fef4f956f.png)
