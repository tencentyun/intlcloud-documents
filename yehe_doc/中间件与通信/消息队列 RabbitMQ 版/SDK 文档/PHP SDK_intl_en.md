## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for PHP as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [Install PHP 5.6 or later](https://www.php.net/manual/en/install.php)
- [Install PEAR](https://pear.php.net/manual/en/installation.getting.php)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-php-sdk-demo.zip)

## Directions

### Step 1. Install the `php-amqplib` library

RabbitMQ officially recommends the `php-amqplib` client. First, you need to import the `php-amqplib` library into your project.

1. Add the `composer.json` file to your project.
   ```json
   {
       "require": {
           "php-amqplib/php-amqplib": ">=3.0"
       }
   }
   ```

2. Use Composer for installation.
   ```shell
   composer.phar install
   ```
   You can also run the following command:
   ```shell
   composer install
   ```

3. Import the library file into the client files to create a client.
   ```php
   require_once('../vendor/autoload.php');
   ```
   After completing the above steps, you can create a connection for interaction with the server.


### Step 2. Send messages

Create and compile a message producing program (with a direct exchange as an example).

```php
require_once('../vendor/autoload.php');

use PhpAmqpLib\Connection\AMQPStreamConnection;
use PhpAmqpLib\Message\AMQPMessage;

$exchange_name = 'exchange_name';
$exchange_type = 'direct';

// Create a connection
$connection = new AMQPStreamConnection(
    $host,
    $port,
    $username,
    $password,
    $vhost,
    false,
    'PLAIN');
// Establish a channel
$channel = $connection->channel();
// Declare the exchange
$channel->exchange_declare($exchange_name, $exchange_type, false, true, false);

// Set the message routing key
$routing_keys = array('info', 'waring', 'error');

for ($x = 0; $x < count($routing_keys); $x++) {
    // Message content
    $msg = new AMQPMessage('This is a direct[' . $routing_keys[$x] . '] message!');
    // Send a message to the specified exchange and set the routing key
    $channel->basic_publish($msg, $exchange_name, $routing_keys[$x]);

    echo " [Producer(Routing)] Sent '" . $msg->body . "'\n";
}
// Release resources
$channel->close();
$connection->close();
```

| Parameter | Description |
| :---------------- | :----------------------------------------------------------- |
| $exchange_name    | Exchange name, which can be obtained from the exchange list in the console.                  |
| $exchange_type    | It must be the same as the type of the above exchange.                         |
| $host              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/25fa29cbd4558973eba4645db1942f32.png) |
| $port             | Cluster access port.                                     |
| $username        | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
| $password          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/3b1372347067abadbe8848c22df665fc.png) |
| $vhost       | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/135399240e27162af544b20ef0ce54f9.png) |
| $routing_keys[$x] | Routing key bound to the consumer message queue, which is also the message routing rule and can be obtained in the **Binding Key** column in the binding list in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/2fc168768fdd01bb1476576f54f72c91.png) |

### Step 3. Consume messages

Create and compile a message consuming program.

```php
<?php

require_once('../vendor/autoload.php');
require_once('../Constant.php');

use PhpAmqpLib\Connection\AMQPStreamConnection;

$exchange_name = 'exchange_name';
$exchange_type = 'direct';
$queue_name = 'route_queue1';

// Create a connection
$connection = new AMQPStreamConnection(
    $host,
    $port,
    $username,
    $password,
    $vhost,
    false,
    'PLAIN');
// Establish a channel
$channel = $connection->channel();
// Declare the exchange
$channel->exchange_declare($exchange_name, $exchange_type, false, true, false);
// Declare the message queue
$channel->queue_declare($queue_name, false, true, false, false);

// Set the queue routing key
$routing_keys = array('info', 'waring', 'error');
for ($x = 0; $x < count($routing_keys); $x++) {
    // Bind the message queue to the specified exchange and set `routingKey`
    $channel->queue_bind($queue_name, $exchange_name, $routing_keys[$x]);
}

echo " [Consumer1(Routing: info/waring/error)] Waiting for messages. To exit press CTRL+C\n";

// Message callback (message consumption logic)
$callback = function ($msg) {
    echo ' [Consumer1(Routing: info/waring/error)] Received ', $msg->body, "\n";
};
// Create a consumer to listen on the specified message queue
$channel->basic_consume($queue_name, '', false, true, false, false, $callback);

while ($channel->is_open()) {
    $channel->wait();
}
// Disable the resource
$channel->close();
$connection->close();

```

| Parameter | Description |
| :---------------- | :----------------------------------------------------------- |
| $exchange_name    | Exchange name, which can be obtained from the exchange list in the console.                  |
| $exchange_type    | It must be the same as the type of the above exchange.                         |
| $queue_name      | Queue name, which can be obtained from the queue list in the console.                         |
| $host              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/8e032a165ed6b94548d77a4358d5dd04.png) |
| $port             | Cluster access port.                                     |
| $username        | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
| $password          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/6322cc8d7f251a78c906ea53be692af6.png) |
| $vhost       | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/90998c05bce789c1a73b411e75da69b1.png) |
| $routing_keys[$x] | Routing key bound to the consumer message queue, which is also the message routing rule and can be obtained in the **Binding Key** column in the binding list in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/a73031e2ed05980fdc89bcde13d84ba4.png) |



### Step 4. View messages

To check whether messages are sent to TDMQ for RabbitMQ successfully, view the connected consumer status on the **[Cluster](https://console.cloud.tencent.com/tdmq/rabbit-cluster)** > **Queue** page in the console.

![img](https://qcloudimg.tencent-cloud.cn/raw/808280beb9a7c350af07fc111c13d7ed.png)



>? For the complete sample code and other use cases, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-php-sdk-demo.zip) or [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html).

