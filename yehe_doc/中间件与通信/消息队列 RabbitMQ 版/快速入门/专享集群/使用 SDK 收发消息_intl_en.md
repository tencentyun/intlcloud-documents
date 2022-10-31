## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Java as an example and helps you better understand the message sending and receiving processes.



## Prerequisites

- You have created the required resources as instructed in [Resource Creation and Preparation](https://www.tencentcloud.com/document/product/1112/51078).
- You have installed [JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html).
- You have installed [Maven 2.5 or later](http://maven.apache.org/download.cgi#).
- You have downloaded the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-java-sdk-demo.zip).

## Directions

### Step 1. Install the Java dependent library

Add the following dependencies to the `pom.xml` file:
<dx-codeblock>
:::  xml
<!-- in your <dependencies> block -->
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>5.13.0</version>
</dependency>
:::
</dx-codeblock>

### Step 2. Produce messages

Compile and run `MessageProducer.java`.
<dx-codeblock>
:::  java
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.tencent.tdmq.demo.cloud.Constant;

/**

 * Message producer
   */
   public class MessageProducer {

   /**

    * Exchange name
      */
      private static final String EXCHANGE_NAME = "exchange_name";

   public static void main(String[] args) throws Exception {
       // Connection factory
       ConnectionFactory factory = new ConnectionFactory();
       // Set the service address (replace with the access point address copied in the console)
       factory.setUri("amqp://***");
       // Set the vhost (copy the vhost name in the open-source RabbitMQ console)
       factory.setVirtualHost(VHOST_NAME);
       // Set the username (use the username in the permission configuration of the vhost in the open-source RabbitMQ console)
       factory.setUsername(USERNAME);
       // Set the password (use the user key)
       factory.setPassword("****");
       // Get the connection address and establish the channel
       try (Connection connection = factory.newConnection(); Channel channel = connection.createChannel()) {
           // Bind the message exchange (`EXCHANGE_NAME` must exist in the TDMQ for RabbitMQ console, and the exchange type must be the same as that in the console)
           channel.exchangeDeclare(EXCHANGE_NAME, "fanout");
           for (int i = 0; i < 10; i++) {
               String message = "this is rabbitmq message " + i;
               // Publish a message to the exchange, which will automatically deliver the message to the corresponding queue
               channel.basicPublish(EXCHANGE_NAME, "", null, message.getBytes());
               System.out.println(" [producer] Sent '" + message + "'");
           }
       } catch (Exception e) {
           e.printStackTrace();
       }
   }
   }
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
<td align="left">EXCHANGE_NAME</td>
<td align="left">Enter the name of the exchange created in the open-source RabbitMQ console.</td>
</tr>
<tr>
<td align="left">factory.setUri</td>
<td align="left">Enter the cluster access address, which can be obtained from the <strong>VPC</strong> section on the <strong>Basic Info</strong> page of the cluster.</td>
</tr>
<tr>
<td align="left">factory.setVirtualHost</td>
<td align="left">Enter the name of the vhost created in the open-source RabbitMQ console.</td>
</tr>
<tr>
<td align="left">factory.setUsername</td>
<td align="left">Enter the name of the user created in the open-source RabbitMQ console.</td>
</tr>
<tr>
<td align="left">factory.setPassword</td>
<td align="left">Enter the password of the user created in the open-source RabbitMQ console.</td>
</tr>
</tbody></table>




### Step 3. Consume messages

Compile and run `MessageConsumer.java`.
<dx-codeblock>
:::  java
import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import com.tencent.tdmq.demo.cloud.Constant;

import java.io.IOException;
import java.nio.charset.StandardCharsets;

/**

 * Message consumer
   */
   public class MessageConsumer1 {

   /**

    * Queue name
      */
      public static final String QUEUE_NAME = "queue_name";

   /**

    * Exchange name
      */
      private static final String EXCHANGE_NAME = "exchange_name";

   public static void main(String[] args) throws Exception {
       // Connection factory
       ConnectionFactory factory = new ConnectionFactory();
       // Set the service address (replace with the access point address copied in the console)
       factory.setUri("amqp://***");
       // Set the vhost (copy the vhost name in the open-source RabbitMQ console)
       factory.setVirtualHost(VHOST_NAME);
       // Set the username (use the username in the permission configuration of the vhost in the open-source RabbitMQ console)
       factory.setUsername(USERNAME);
       // Set the password (use the user key)
       factory.setPassword("****");
       // Get the connection address
       Connection connection = factory.newConnection();
       // Establish a channel
       Channel channel = connection.createChannel();
       // Bind the message exchange
       channel.exchangeDeclare(EXCHANGE_NAME, "fanout");
       // Declare the queue message
       channel.queueDeclare(QUEUE_NAME, true, false, false, null);
       // Bind the message exchange (`EXCHANGE_NAME` must exist in the TDMQ for RabbitMQ console, and the exchange type must be the same as that in the console)
       channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "");
       System.out.println(" [Consumer1] Waiting for messages.");
       // Subscribe to the message
       channel.basicConsume(QUEUE_NAME, false, "ConsumerTag", new DefaultConsumer(channel) {
           @Override
           public void handleDelivery(String consumerTag, Envelope envelope,
                                      AMQP.BasicProperties properties, byte[] body)
                   throws IOException {
               // Received message for business logic processing
               System.out.println("Received: " + new String(body, StandardCharsets.UTF_8) + ", deliveryTag: " + envelope.getDeliveryTag() + ", messageId: " + properties.getMessageId());
               channel.basicAck(envelope.getDeliveryTag(), false);
           }
       });
   }
   }
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
<td align="left">QUEUE_NAME</td>
<td align="left">Enter the name of the queue created in the open-source RabbitMQ console.</td>
</tr>
<tr>
<td align="left">EXCHANGE_NAME</td>
<td align="left">Enter the name of the exchange created in the open-source RabbitMQ console.</td>
</tr>
<tr>
<td align="left">factory.setUri</td>
<td align="left">Enter the cluster access address, which can be obtained from the <strong>VPC</strong> section on the <strong>Basic Info</strong> page of the cluster.</td>
</tr>
<tr>
<td align="left">factory.setVirtualHost</td>
<td align="left">Enter the name of the vhost created in the open-source RabbitMQ console.</td>
</tr>
<tr>
<td align="left">factory.setUsername</td>
<td align="left">Enter the name of the user created in the open-source RabbitMQ console.</td>
</tr>
<tr>
<td align="left">factory.setPassword</td>
<td align="left">Enter the password of the user created in the open-source RabbitMQ console.</td>
</tr>
</tbody></table>




