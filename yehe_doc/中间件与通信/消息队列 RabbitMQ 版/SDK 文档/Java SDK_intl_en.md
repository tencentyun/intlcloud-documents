## Overview

This document describes how to use open-source SDK to send and receive messages using the SDK for Java as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources.](https://intl.cloud.tencent.com/document/product/1112/43069)
- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-java-sdk-demo.zip)

## Directions

### Step 1. Install the Java dependency library

Add the following dependencies to the `pom.xml` file:

```xml
<!-- in your <dependencies> block -->
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>5.13.0</version>
</dependency>
```

### Step 2. Produce messages

Create, compile, and run `MessageProducer.java`.

```java
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
```

| Parameter                     | Description                                                         |
| :--------------------- | :----------------------------------------------------------- |
| EXCHANGE_NAME    | Exchange name, which can be obtained from the exchange list in the console.                  |
| factory.setUri              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://main.qcloudimg.com/raw/0238d2d64bd896704ebef400fc08a7f1.png) |
| factory.setVirtualHost  | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://main.qcloudimg.com/raw/ae6ec1a5a94c9befea289ad7f5b46aed.png) |
| factory.setUsername        | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
| factory.setPassword          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png) |

### Step 3. Consume messages

Create, compile, and run `MessageConsumer.java`.

```java
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
```

| Parameter                     | Description                                                         |
| :--------------------- | :----------------------------------------------------------- |
| QUEUE_NAME      | Queue name, which can be obtained from the queue list in the console.                         |
| EXCHANGE_NAME    | Exchange name, which can be obtained from the exchange list in the console.                  |
| factory.setUri              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://main.qcloudimg.com/raw/0238d2d64bd896704ebef400fc08a7f1.png) |
| factory.setVirtualHost  | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://main.qcloudimg.com/raw/ae6ec1a5a94c9befea289ad7f5b46aed.png) |
| factory.setUsername        | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
| factory.setPassword          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png) |

### Step 4. Query messages

To check whether messages are sent to TDMQ for RabbitMQ successfully, view the connected consumer status on the **[Cluster](https://console.cloud.tencent.com/tdmq/rabbit-cluster)** > **Queue** page in the console.

![](https://main.qcloudimg.com/raw/a7d78cc58efadfb614b890cc33d08632.png)

>? Above is a sample based on the pub/sub pattern of RabbitMQ. For more samples, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-java-sdk-demo.zip) or [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html).

