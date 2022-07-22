## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Go as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1112/43069).
- [You have installed Go](https://golang.org/dl/)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-go-sdk-demo.zip)

## Directions

1. Run the following command to install the required package in the client environment:
<dx-codeblock>
:::  shell
go get "github.com/rabbitmq/amqp091-go"
:::
</dx-codeblock>
2. After the installation is completed, import the client into your Go project file.
<dx-codeblock>
:::  go
import (amqp "github.com/rabbitmq/amqp091-go")
:::
</dx-codeblock>
3. After the import, you can use the client in your project.


## Example

1. Establish the connection and communication channel.
<dx-codeblock>
:::  go
   // Required parameters
   const (
   	host     = "amqp-xx.rabbitmq.x.tencenttdmq.com" // Service access address
   	username = "roleName" // Role name in the console
   	password = "eyJrZX..." // Role token
   	vhost    = "amqp-xx|Vhost" // Full name of the vhost to be used
   )
   // Create a connection
   conn, err := amqp.Dial("amqp://" + username + ":" + password + "@" + host + ":5672/" + vhost)
   failOnError(err, "Failed to connect to RabbitMQ")
   defer func(conn *amqp.Connection) {
   	err := conn.Close()
   	if err != nil{
   	}
   }(conn)
   
   // Establish a channel
   ch, err := conn.Channel()
   failOnError(err, "Failed to open a channel")
   defer func(ch *amqp.Channel) {
   	err := ch.Close()
   	if err != nil{
   	}
   }(ch)
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
<td align="left">Cluster access address, which can be obtained in the console by clicking <strong>Access Address</strong> in the “Operation” column on the <strong>Cluster</strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/b69f4d057db7758046aff3598f65378a.png" alt="img"></td>
</tr>
<tr>
<td align="left">name-server</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">password</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/9354cc833c8524d7cd9edb83b1690eb6.png" alt=""></td>
</tr>
<tr>
<td align="left">vhost</td>
<td align="left">Vhost name in the format of <strong>“cluster ID + | + vhost name”</strong>. <img src="https://qcloudimg.tencent-cloud.cn/raw/13cf5fe0796be0e2d4cbcb48354a0b2f.png" alt="img"></td>
</tr>
</tbody></table>
2. Declare the exchange.
<dx-codeblock>
:::  go
   // Declare the exchange (the name and type must be the same as those of the existing exchange)
   	err = ch.ExchangeDeclare(
   		"logs-exchange",   // Exchange name
   		"fanout", // Exchange type
   		true,     // durable
   		false,    // auto-deleted
   		false,    // internal
   		false,    // no-wait
   		nil,      // arguments
   	)
   	failOnError(err, "Failed to declare a exchange")
:::
</dx-codeblock>
3. Publish a message.
   A message can be directly sent to the exchange or the specified queue (`hello world` and `work`).
 - Publish the message to the exchange:
<dx-codeblock>
:::  go
   // Message content
   body := "this is new message."
   // Publish the message to the exchange   
   err = ch.Publish(
   	"logs-exchange",         // exchange
   	"", // routing key (Set whether the routing key is required based on the used exchange type). If no exchange is selected, this parameter will be the message queue name
   	false,      // mandatory
   	false,      // immediate
   	amqp.Publishing{
   		ContentType: "text/plain",
   		Body:        []byte(body),
   	})
   failOnError(err, "Failed to publish a message")
:::
</dx-codeblock>
 - Publish the message to the specified queue:
<dx-codeblock>
:::  go
 // Publish the message to the specified message queue
 err = ch.Publish(
	"",         // exchange
	queue.Name, // routing key
	false,      // mandatory
	false,      // immediate
	amqp.Publishing{
		ContentType: "text/plain",
		Body:        []byte(body),
	})
 failOnError(err, "Failed to publish a message")
:::
</dx-codeblock>
4. Subscribe to a message.
<dx-codeblock>
:::  go
   // Create a consumer and consume the message in the specified message queue
   msgs, err := ch.Consume(
   	"message-queue", // message-queue
   	"",           // consumer
   	false,        // Set to manual acknowledgment as needed
   	false,        // exclusive
   	false,        // no-local
   	false,        // no-wait
   	nil,          // args
   )
   failOnError(err, "Failed to register a consumer")
   
   // Obtain the message in the queue
   forever := make(chan bool)
   go func() {
   	for d := range msgs {
   		log.Printf("Received a message: %s", d.Body)
   		t := time.Duration(1)
   		time.Sleep(t * time.Second)
   		// Manually return the acknowledgment
   		d.Ack(false)
   	}
   }()
   log.Printf(" [Consumer] Waiting for messages.")
   <-forever
:::
</dx-codeblock>
5. The consumer uses the routing key.
<dx-codeblock>
:::  go
   // You need to specify the exchange and routing key in the message queue
   err = ch.QueueBind(
   	q.Name, // queue name
   	"routing_key",     // routing key
   	"topic_demo", // exchange
   	false,
   	nil,
   )
   failOnError(err, "Failed to bind a queue")
:::
</dx-codeblock>


>? For detailed samples, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-go-sdk-demo.zip) or [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html).

