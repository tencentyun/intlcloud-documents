## Overview

This document describes how to access CKafka to send/receive messages with the SDK for PHP through SASL_PLAINTEXT over public network.

## Prerequisites

- [Install librdkafka](https://github.com/edenhill/librdkafka/)
- [Install PHP 5.6 or later](https://www.php.net/manual/en/install.php)
- [Install PEAR](https://pear.php.net/manual/en/installation.getting.php)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/phpkafkademo/PUBLIC_SASL)

## Directions

### Step 1. Add rdkafka extension

1. On the [rdkafka official website](http://pecl.php.net/package/rdkafka), find the PHP-rdkafka extension package of the latest version.
   >?PHP-rdkafka extension packages of different versions have different requirements on the PHP version. This procedure takes the PHP-rdkafka extension package of version 4.1.2 as an example.

2. Install the rdkafka extension.
   ```bash
   wget --no-check-certificate https://pecl.php.net/get/rdkafka-4.1.2.tgz
   pear install rdkafka-4.1.2.tgz
   # If the installation is successful, “install ok” and “You should add “extension=rdkafka.so” to php.ini” are displayed
   # If the installation fails and the system prompts “could not extract the package.xml file from “rdkafka-4.1.2.tgz””, please decompress the package manually, copy the package.xml file into the “rdkafka” directory, and run “pear install package.xml” to install it
   # For other errors, please follow the prompts to troubleshoot
   # After successful installation, add “extension=rdkafka.so” to “php.ini”
   # After you run “php --ini”, the value of “Loaded Configuration File” is the location of “php.ini” 
   echo 'extension=rdkafka.so' >> /etc/php.ini
   ```

### Step 2. Prepare configurations

Create a configuration file named `CKafkaSetting.php`.
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

| Parameter              | Description                                                         |
| ------------------ | ------------------------------------------------------------ |
| bootstrap_servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section in **Basic Info** on the instance details page in the console. <br/>![img](https://main.qcloudimg.com/raw/c5cf200a66f6dcf627d2ca6f1c747ecf.png) |
| topic_name          | Topic name, which can be copied in **Topic Management** on the instance details page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |
| group_id          | Consumer group ID. You can customize it according to your business needs. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |
| ckafka_instance_id | Instance ID, which can be obtained in **Basic Info** on the instance details page in the CKafka console.<br/>![](https://main.qcloudimg.com/raw/9c417da4953669372fa4c13973096d3b.png) |
| sasl.username    | Username, which is set when the user is created in **User Management** on the instance details page in the console.                     |
| sasl_password    | Password, which is set when the user is created in **User Management** on the instance details page in the console             |



### Step 3. Send messages

1. Write a message production program named `Producer.php`.
  ```php
<?php

$setting = require __DIR__ . '/CKafkaSetting.php';

$conf = new RdKafka\Conf();
// Set the ingress service. Obtain the corresponding service address in the console
$conf->set('bootstrap.servers', $setting['bootstrap_servers']);
// ---------- Set this part if SASL authentication is enabled ----------
// The SASL authentication mechanism is PLAIN by default
$conf->set('sasl.mechanism', 'PLAIN');
// Set the username. Format: instance ID + # + username specified on the **User Management** tab page in the console
$conf->set('sasl.username', $setting['ckafka_instance_id'] . '#' . $setting['sasl_username']);
// Set the password, which is set on the **User Management** tab page in the console
$conf->set('sasl.password', $setting['sasl_password']);
// Configure an ACL policy locally
$conf->set('security.protocol', 'SASL_PLAINTEXT');
// ---------- Set this part if SASL authentication is enabled ----------
// Kafka producer supports 3 ACK mechanisms:
// -1 or all: the broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and syncs it to followers in all ISRs.
// This configuration provides the highest data reliability, as messages will never get lost as long as one synced replica survives. It should be noted that this configuration cannot guarantee that replicas will be returned after data has been read from or written to all of them.
// It can be used together with the “min.insync.replicas” parameter at the topic level.
// 0: the producer continues to send the next message or next batch of messages without waiting for the broker’s acknowledgment of sync. This configuration provides the highest production performance but the lowest data reliability.
// (Data may get lost when the server fails. If the leader is dead but the producer is unaware of that, the broker cannot receive messages.)
// 1: the producer sends the next message or next batch of messages after it receives an acknowledgment that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability.
// (Messages may get lost if the leader is dead but has not been replicated yet.)
// If you do not configure this parameter, the default value will be 1. You can customize this according to your business requirements.
$conf->set('acks', '1');
// Number of retries upon request error. It is recommended that you set the parameter to a value greater than 0 to enable retries and guarantee that messages are not lost to the greatest extent possible.
$conf->set('retries', '0');
// Retry interval upon request failure
$conf->set('retry.backoff.ms', 100);
// Timeout duration of a producer network request
$conf->set('socket.timeout.ms', 6000);
$conf->set('reconnect.backoff.max.ms', 3000);

// Register a callback for message sending
$conf->setDrMsgCb(function ($kafka, $message) {
    echo '**Producer** sent a message: message=' . var_export($message, true) . "\n";
});
// Register a callback for message sending errors
$conf->setErrorCb(function ($kafka, $err, $reason) {
    echo "**Producer** message sending error: err=$err reason=$reason \n";
});

$producer = new RdKafka\Producer($conf);
// Set the field to LOG_DEBUG for debugging
//$producer->setLogLevel(LOG_DEBUG);
$topicConf = new RdKafka\TopicConf();
$topic = $producer->newTopic($setting['topic_name'], $topicConf);
// Produce and send a message
for ($i = 0; $i < 5; $i++) {
    // RD_KAFKA_PARTITION_UA: allow Kafka to choose any partition
    $topic->produce(RD_KAFKA_PARTITION_UA, 0, "Message $i");
    $producer->poll(0);
}

while ($producer->getOutQLen() > 0) {
    $producer->poll(50);
}

echo "**Producer** successfully sent the message\n";
  ```

2. Run `Producer.php` to send messages.
```bash
php Producer.php
```

3. View the execution result.
  ```bash
>**Producer** sent a message: message=RdKafka\Message::__set_state(array(
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
>**Producer** sent a message: message=RdKafka\Message::__set_state(array(
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

>**Producer** successfully sent the message
  ```

4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the target topic, and click **More** > **Message Query** to view the message just sent.
![](https://main.qcloudimg.com/raw/c18f71eecfa5f2d9ef9df19b7eb876fc.png)


### Step 4. Consume messages

1. Write a message consumption program named `Consumer.php`.
  ```php
<?php

$setting = require __DIR__ . '/CKafkaSetting.php';

$conf = new RdKafka\Conf();
$conf->set('group.id', $setting['group_id']);
// Set the ingress service. Obtain the corresponding service address in the console
$conf->set('bootstrap.servers', $setting['bootstrap_servers']);
// ---------- Set this part if SASL authentication is enabled ----------
// The SASL authentication mechanism is PLAIN by default
$conf->set('sasl.mechanism', 'PLAIN');
// Set the username. Format: instance ID + # + username specified on the **User Management** tab page in the console
$conf->set('sasl.username', $setting['ckafka_instance_id'] . '#' . $setting['sasl_username']);
// Set the password, which is set on the **User Management** tab page in the console
$conf->set('sasl.password', $setting['sasl_password']);
// Configure an ACL policy locally
$conf->set('security.protocol', 'SASL_PLAINTEXT');
// ---------- Set this part if SASL authentication is enabled ----------
// Consumer timeout period when the Kafka consumer grouping mechanism is used. If the broker does not receive the heartbeat of the consumer within this period,
// the consumer will be considered to have failed and the broker will initiate rebalance.
$conf->set('session.timeout.ms', 10000);
// Client request timeout duration. If no response is received within this duration, the request will time out and fail.
$conf->set('request.timeout.ms', 305000);
// Set the interval between retries for the client
$conf->set('reconnect.backoff.max.ms', 3000);

$topicConf = new RdKafka\TopicConf();
#$topicConf->set('auto.commit.interval.ms', 100);
// Offset resetting policy. Set it according to the business scenario. Improper setting can result in data consumption failure.
$topicConf->set('auto.offset.reset', 'earliest');
$conf->setDefaultTopicConf($topicConf);

$consumer = new RdKafka\KafkaConsumer($conf);
// Set the field to LOG_DEBUG for debugging
//$consumer->setLogLevel(LOG_DEBUG);
$consumer->subscribe([$setting['topic_name']]);

$isConsuming = true;
while ($isConsuming) {
    $message = $consumer->consume(10 * 1000);
    switch ($message->err) {
        case RD_KAFKA_RESP_ERR_NO_ERROR:
            echo "**Consumer** received a message:" . var_export($message, true) . "\n";
            break;
        case RD_KAFKA_RESP_ERR__PARTITION_EOF:
            echo "**Consumer** is waiting for messages\n";
            break;
        case RD_KAFKA_RESP_ERR__TIMED_OUT:
            echo "**Consumer** wait timed out\n";
            $isConsuming = false;
            break;
        default:
            throw new \Exception($message->errstr(), $message->err);
            break;
    }
}
  ```


2. Run `Consumer.php` to consume messages.
```bash
php Consumer.php
```

3. View the execution result.
  ```bash
  >**Consumer** received a message: RdKafka\Message::__set_state(array(
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
  >**Consumer** received a message: RdKafka\Message::__set_state(array(
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

4. On the **Consumer Group** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name, and click **Query Details** to view the consumption details.
![](https://main.qcloudimg.com/raw/3020dcb5f8fd73e02949b20fef4f956f.png)
