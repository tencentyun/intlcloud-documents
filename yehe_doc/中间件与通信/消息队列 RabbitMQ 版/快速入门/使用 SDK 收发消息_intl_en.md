## Overview

This document describes how to use open-source SDK to send and receive messages using the SDK for Java as an example and helps you better understand the message sending and receiving processes.



<dx-alert infotype="explain" title="">
The following takes the Java client as an example. For clients in other languages, see [TDMQ for RabbitMQ](https://intl.cloud.tencent.com/document/product/1112/46391).
</dx-alert>



## Prerequisites

- [You have created the required resources.](https://intl.cloud.tencent.com/document/product/1112/43069)
- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo.](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-java-sdk-demo.zip)

## Directions

### Step 1. Install the Java dependency library

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
        // Set vhost (replace with the vhost name copied in the console)
        factory.setVirtualHost(VHOST_NAME);
        // Set the username (use the role name in the permission configuration of the vhost)
        factory.setUsername(USERNAME);
        // Set the password (use the role key)
        factory.setPassword("eyJh****");
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
<td align="left">Exchange name, which can be obtained from the exchange list in the console.</td>
</tr>
<tr>
<td align="left">factory.setUri</td>
<td align="left">Cluster access address, which can be obtained in the console by clicking <strong>Get Access Address</strong> in the **Operation** column on the <strong>Cluster</strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/5bddcbb6361dad5825aee9015a9049a6.png" alt="img"></td>
</tr>
<tr>
<td align="left">factory.setVirtualHost</td>
<td align="left">Vhost name in the format of <strong>"cluster ID + | + vhost name"</strong>. <img src="https://qcloudimg.tencent-cloud.cn/raw/eb75eb3519cf399d95e7423d1c26c567.png" alt="img"></td>
</tr>
<tr>
<td align="left">factory.setUsername</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">factory.setPassword</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/cd543d9ef835a557c280cf592ca49ab2.png" alt="img"></td>
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
        // Set vhost (replace with the vhost name copied in the console)
        factory.setVirtualHost(VHOST_NAME);
        // Set the username (use the role name in the permission configuration of the vhost)
        factory.setUsername(USERNAME);
        // Set the password (use the role key)
        factory.setPassword("eyJh****");
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
<td align="left">Queue name, which can be obtained from the queue list in the console.</td>
</tr>
<tr>
<td align="left">EXCHANGE_NAME</td>
<td align="left">Exchange name, which can be obtained from the exchange list in the console.</td>
</tr>
<tr>
<td align="left">factory.setUri</td>
<td align="left">Cluster access address, which can be obtained in the console by clicking <strong>Get Access Address</strong> in the **Operation** column on the <strong>Cluster</strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/5bddcbb6361dad5825aee9015a9049a6.png" alt="img"></td>
</tr>
<tr>
<td align="left">factory.setVirtualHost</td>
<td align="left">Vhost name in the format of <strong>"cluster ID + | + vhost name"</strong>. <img src="https://qcloudimg.tencent-cloud.cn/raw/eb75eb3519cf399d95e7423d1c26c567.png" alt="img"></td>
</tr>
<tr>
<td align="left">factory.setUsername</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">factory.setPassword</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/cd543d9ef835a557c280cf592ca49ab2.png" alt="img"></td>
</tr>
</tbody></table>

### Step 4. Query messages

To check whether messages are sent to TDMQ for RabbitMQ successfully, view the connected consumer status on the **[Cluster](https://console.cloud.tencent.com/tdmq/rabbit-cluster)** > **Queue** page in the console.

[](https://qcloudimg.tencent-cloud.cn/raw/4a629126c8cf4adad225289cf981a4a7.png)

>? Above is a sample based on the pub/sub pattern of RabbitMQ. For more samples, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-java-sdk-demo.zip) or [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html).
