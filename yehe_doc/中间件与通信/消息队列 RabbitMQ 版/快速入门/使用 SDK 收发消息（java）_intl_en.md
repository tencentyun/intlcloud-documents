## Overview

This document describes how to download the demo, perform a simple test, and run a Java client after you create cluster, vhost, exchange, and other resources in the console.

## Prerequisites

- [Install JDK 1.8 or above](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Install Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [Download the demo](https://tdmq-1300957330.cos.ap-guangzhou.myqcloud.com/TDMQ-demo/tdmq-rabbitmq-client-demo.zip)

## Directions

1. Add the following Java dependency library information to the `pom.xml` file:
   ```xml
   <dependency>
       <groupId>com.rabbitmq</groupId>
       <artifactId>amqp-client</artifactId>
       <version>5.13.0</version>
   </dependency>
   ```

2. Create a messaging program AoPTest.java and configure related parameters.
   ```java
   package com.qcloud.tdmq.aop.client.test;
   
   import com.rabbitmq.client.AMQP;
   import com.rabbitmq.client.BuiltinExchangeType;
   import com.rabbitmq.client.Channel;
   import com.rabbitmq.client.Connection;
   import com.rabbitmq.client.ConnectionFactory;
   import com.rabbitmq.client.DefaultConsumer;
   import com.rabbitmq.client.Envelope;
   import com.rabbitmq.client.RecoveryDelayHandler;
   
   import java.io.IOException;
   import java.text.SimpleDateFormat;
   import java.util.Date;
   import java.util.concurrent.TimeoutException;
   
   public class AoPTest {
   
       // Enter your username and key, which can be obtained on the **Role Management** page in the console
       private static final String username = "role";
       private static final String password = "eyJr****";
       // Cluster access address, which can be obtained in the **Operation** column on the **Cluster Management** page
       private static final String uri = "amqp://amqp-****.com:5***";
       // Vhost name in the format of "cluster ID + | + vhost name", which can be copied on the **Vhost** page in the console
       private static final String vhostname = "amqp-****|vhost";
       // Exchange name, which can be copied in the console after creation
       private static final String exchange = "exchange";
       // Queue name, which can be copied in the console after creation
       private static final String queue = "queue";
   
       private ConnectionFactory connectionFactory;
       private Connection connection;
       private Channel channel;
   
       public AoPTest(String uri, String vhost) throws Exception {
           connectionFactory = new ConnectionFactory();
           connectionFactory.setUri(uri);
           connectionFactory.setVirtualHost(vhost);
           connectionFactory.setUsername(username);
           connectionFactory.setPassword(password);
           connectionFactory.setAutomaticRecoveryEnabled(true);
           connectionFactory.setRecoveryDelayHandler(new RecoveryDelayHandler.ExponentialBackoffDelayHandler());
           connection = connectionFactory.newConnection();
           channel = connection.createChannel();
           channel.basicQos(1);
       }
   
       public void close() throws IOException, TimeoutException {
           if (channel != null) {
               channel.close();
           }
           if (connection != null) {
               connection.close();
           }
       }
   
       public void publish(String exchange, String routingKey, int count) throws InterruptedException {
           SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
           for (int i = 0; i < count; i++) {
               try {
                   AMQP.BasicProperties properties = new AMQP.BasicProperties.Builder()
                           .appId("rabbitmq-client")
                           .contentType("text/plain")
                           .messageId("messageId-" + i)
                           .priority(2)
                           .build();
                   channel.basicPublish(exchange, routingKey, properties, ("hello - " + format.format(new Date()) + " - " + i).getBytes());
               } catch (Exception e) {
                   e.printStackTrace();
               }
               Thread.sleep(100);
           }
           System.out.println("publish ok...");
       }
   
       public void consume(String queue) throws IOException {
           channel.basicConsume(queue, false, "clientTag", new DefaultConsumer(channel) {
               @Override
               public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                          byte[] body) throws IOException {
                   System.out.println("properties: " + properties.toString());
                   System.out.println("consumerTag: " + consumerTag + ", deliveryTag: " + envelope.getDeliveryTag() +
                           ", receive msg: " + new String(body));
                   channel.basicAck(envelope.getDeliveryTag(), false);
               }
           });
       }
     
       public static void main(String[] args) throws Exception {
           
           AoPTest aopTest = new AoPTest(uri, vhostname);
	   // Enable continuous consumption
           aopTest.consume(queue);
	   // Start producing messages
           aopTest.publish(exchange, "routingKey", 10);
   
           Thread.sleep(10_000);
           aopTest.close();
       }
   }  
   ```
   
	 
   | Parameter | Description |
   | ---------- | ------------------------------------------------------------ |
   | username | Role name, which can be copied on the **[Role Management](https://console.cloud.tencent.com/tdmq/role)** page. |
   | password | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.cloud.tencent.com/tdmq/role)** page. ![](https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png) |
   | exchange | Exchange name, which can be obtained from the exchange list in the console. |
   | qu1 | Queue name, which can be obtained from the queue list in the console. |
   | uri | Cluster access address, which can be obtained from **Get Access Address** in the **Operation** column on the **Cluster Management** page. ![](https://main.qcloudimg.com/raw/0238d2d64bd896704ebef400fc08a7f1.png) |
   | vhostname | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![](https://main.qcloudimg.com/raw/ae6ec1a5a94c9befea289ad7f5b46aed.png) |
   | routingKey | Message routing rule, which can be obtained in the **Binding Key** column in the binding list in the console. ![](https://main.qcloudimg.com/raw/66d31e7d7ec8519843a8fc67bff87265.png) |
   
3. Compile and run the AoPTest.java program. The result of successful execution is as follows.

   ![](https://main.qcloudimg.com/raw/c7f33820fecd715a977276bbcdfc2aba.png)

4. On the **[Cluster Management](https://console.cloud.tencent.com/tdmq/rocket-cluster)**> **Queue** page in the console, you can view the status of connected consumers.
   ![](https://main.qcloudimg.com/raw/a7d78cc58efadfb614b890cc33d08632.png)

