## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for C++ as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1112/43069).
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-cpp-sdk-demo.zip)

## Directions

### Step 1. Prepare the environment

1. Install a [C and C++ client library](https://www.rabbitmq.com/devtools.html?spm=a2c4g.11186623.0.0.22d166975jyVxo#c-dev). This document uses AMQP-CPP as an example.
2. Import the dynamic library and header file.

### Step 2. Produce messages

1. Establish a connection.
<dx-codeblock>
:::  c++
   auto evbase = event_base_new();
   LibEventHandlerMyError hndl(evbase);
   
   // Establish a connection
   AMQP::TcpConnection connection(&hndl, AMQP::Address(
       "amqp://admin:eyJrZXlJZC...@amqp-xxx.rabbitmq.ap-sh.public.tencenttdmq.com:5672/amqp-xxx|vhost-cpp"));
   	// The service address is in the format of “amqp://username:password@host:port/vhost”.
   // Create a channel
   AMQP::TcpChannel channel(&connection);
   channel.onError([&evbase](const char *message) {
       std::cout << "Channel error: " << message << std::endl;
       event_base_loopbreak(evbase);
   });
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">String</td>
<td align="left">Cluster access address, which can be obtained in the console by clicking <strong>Access Address</strong> in the “Operation” column on the <strong>Cluster</strong> page. <img src="https://main.qcloudimg.com/raw/0238d2d64bd896704ebef400fc08a7f1.png" alt="img"></td>
</tr>
<tr>
<td align="left">port</td>
<td align="left">Port number in the cluster access address.</td>
</tr>
<tr>
<td align="left">name-server</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">password</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png" alt=""></td>
</tr>
<tr>
<td align="left">vhost</td>
<td align="left">Vhost name in the format of <strong>“cluster ID + | + vhost name”</strong>. <img src="https://main.qcloudimg.com/raw/ae6ec1a5a94c9befea289ad7f5b46aed.png" alt="img"></td>
</tr>
</tbody></table>
2. Send messages.
<dx-codeblock>
:::  c++
   // Declare an exchange
   channel.declareExchange(exchange_name, AMQP::ExchangeType::direct);
   
   // Send messages to the exchange
   channel.publish(exchange_name, routing_key, "Hello client this is a info message");
   
   event_base_dispatch(evbase);
   event_base_free(evbase);
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">exchange_name</td>
<td align="left">Exchange name, which can be obtained from the exchange list in the console.</td>
</tr>
<tr>
<td align="left">routing_key</td>
<td align="left">The routing key supported by the message queue.</td>
</tr>
</tbody></table>

### Step 3. Consume messages

1. Establish a connection.
<dx-codeblock>
:::  c++
ConnHandler handler;
// Establish a connection
AMQP::TcpConnection connection(handler, AMQP::Address(host, part, AMQP::Login(username, password), vhost));
// Create a channel
AMQP::TcpChannel channel(&connection);
channel.onError([&handler](const char *message) {
		std::cout << "Channel error: " << message << std::endl;
		handler.Stop();
});
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">String</td>
<td align="left">Cluster access address, which can be obtained in the console by clicking <strong>Access Address</strong> in the “Operation” column on the <strong>Cluster</strong> page. <img src="https://main.qcloudimg.com/raw/0238d2d64bd896704ebef400fc08a7f1.png" alt="img"></td>
</tr>
<tr>
<td align="left">port</td>
<td align="left">Port number in the cluster access address.</td>
</tr>
<tr>
<td align="left">name-server</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">password</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png" alt=""></td>
</tr>
<tr>
<td align="left">vhost</td>
<td align="left">Vhost name in the format of <strong>“cluster ID + | + vhost name”</strong>. <img src="https://main.qcloudimg.com/raw/ae6ec1a5a94c9befea289ad7f5b46aed.png" alt="img"></td>
</tr>
</tbody></table>
2. Declare an exchange and a message queue and bind them.
<dx-codeblock>
:::  c++
// Declare an exchange
channel.declareExchange(exchange_name, AMQP::ExchangeType::direct);
// Declare a message queue
channel.declareQueue(queue_name, AMQP::durable);
// Bind the message queue to the exchange
channel.bindQueue(exchange_name, queue_name, routing_key);
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">exchange_name</td>
<td align="left">Exchange name, which can be obtained from the exchange list in the console.</td>
</tr>
<tr>
<td align="left">queue_name</td>
<td align="left">Message queue name, which can be obtained from the queue list in the console.</td>
</tr>
<tr>
<td align="left">routing_key</td>
<td align="left">The routing key supported by the message queue.</td>
</tr>
</tbody></table>
#### 2. Subscribe to messages
<dx-codeblock>
:::  c++
// Subscribe to the message
channel.consume(queue_name)
		.onReceived
		(
		[&channel](const AMQP::Message &msg, uint64_t tag, bool redelivered) {
				// Process the message
				std::cout << "Received: " << msg.body() << std::endl;
				// Acknowledge the message, or reject it if the consumption failed
				channel.ack(tag);
		}
);
handler.Start();
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">queue_name</td>
<td align="left">Message queue name, which can be obtained from the queue list in the console.</td>
</tr>
</tbody></table>


>?For a complete sample or more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-cpp-sdk-demo.zip), [AMQP-CPP ](https://github.com/CopernicaMarketingSoftware/AMQP-CPP), or [AMQP-CPP Examples](https://github.com/hoxnox/examples.amqp-cpp).

