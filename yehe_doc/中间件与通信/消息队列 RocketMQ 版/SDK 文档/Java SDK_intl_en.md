## Overview

This document describes how to use open-source SDK to send and receive messages using the SDK for Java as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- You have created the required resources as instructed in [Resource Creation and Preparation](https://intl.cloud.tencent.com/document/product/1112/43069).
- You have installed [JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html).
- You have installed [Maven 2.5 or later](http://maven.apache.org/download.cgi#).
- You have downloaded the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip).

## Directions

### Step 1. Install the Java dependency library

Introduce dependencies in a Java project and add the following dependencies to the `pom.xml` file. This document uses a Maven project as an example.
   >?The dependency version must be v4.6.1 or later.
<dx-codeblock>
:::  xml
    <!-- in your <dependencies> block -->
      <dependency>
          <groupId>org.apache.rocketmq</groupId>
          <artifactId>rocketmq-client</artifactId>
          <version>4.6.1</version>
      </dependency>

      <dependency>
          <groupId>org.apache.rocketmq</groupId>
          <artifactId>rocketmq-acl</artifactId>
          <version>4.6.1</version>
      </dependency>
:::
</dx-codeblock>


### Step 2. Produce messages

1. Create message producers.
<dx-codeblock>
:::  java
   // Instantiate the message producer
      DefaultMQProducer producer = new DefaultMQProducer(
          namespace, 
          groupName,
          new AclClientRPCHook(new SessionCredentials(accessKey, secretKey)) // ACL permission
      );
      // Set the NameServer address
      producer.setNamesrvAddr(nameserver);
      // Start the producer instances
      producer.start();
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
<td align="left">namespace</td>
<td align="left">Namespace name, which can be copied under the <strong>Namespace</strong> tab in the console. Its format is <strong>cluster ID + | + namespace</strong>.</td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <code>Group</code> tab on the **Cluster** page in the console.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the **Operation** column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list.</td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/dece05914450403febd5e7ee7547535b.png" alt="img"></td>
</tr>
</tbody></table>
2. Send messages, which can be sent in the sync, async, or one-way mode.
   - Sync sending
   <dx-codeblock>
   :::  java
      for (int i = 0; i < 10; i++) {
                // Create a message instance and set the topic and message content
                Message msg = new Message(topic_name, "TAG", ("Hello RocketMQ " + i).getBytes(RemotingHelper.DEFAULT_CHARSET));
                // Send the message
                SendResult sendResult = producer.send(msg);
                System.out.printf("%s%n", sendResult);
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
<td align="left">topic_name</td>
<td align="left">Topic name, which can be copied under the <strong><code>Topic</code></strong> tab on the **Cluster** page in the console.</td>
</tr>
<tr>
<td align="left">TAG</td>
<td align="left">A parameter used to set the message tag.</td>
</tr>
</tbody></table>
   - Async sending
<dx-codeblock>
:::  java
      // Disable retry upon sending failures
            producer.setRetryTimesWhenSendAsyncFailed(0);
            // Set the number of messages to be sent
            int messageCount = 10;
            final CountDownLatch countDownLatch = new CountDownLatch(messageCount);
            for (int i = 0; i < messageCount; i++) {
                try {
                    final int index = i;
                    // Create a message instance and set the topic and message content
                    Message msg = new Message(topic_name, "TAG", ("Hello rocketMq " + index).getBytes(RemotingHelper.DEFAULT_CHARSET));
                    producer.send(msg, new SendCallback() {
                        @Override
                        public void onSuccess(SendResult sendResult) {
                            // Logic for message sending successes
                            countDownLatch.countDown();
                            System.out.printf("%-10d OK %s %n", index, sendResult.getMsgId());
                        }
            
                        @Override
                        public void onException(Throwable e) {
                            // Logic for message sending failures
                            countDownLatch.countDown();
                            System.out.printf("%-10d Exception %s %n", index, e);
                            e.printStackTrace();
                        }
                    });
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
            countDownLatch.await(5, TimeUnit.SECONDS);
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
<td align="left">topic_name</td>
<td align="left">Topic name, which can be copied under the <strong><code>Topic</code></strong> tab on the **Cluster** page in the console.</td>
</tr>
<tr>
<td align="left">TAG</td>
<td align="left">A parameter used to set the message tag.</td>
</tr>
</tbody></table>
   - One-way sending
<dx-codeblock>
:::  java
       for (int i = 0; i < 10; i++) {
                // Create a message instance and set the topic and message content
                Message msg = new Message(topic_name, "TAG", ("Hello RocketMQ " + i).getBytes(RemotingHelper.DEFAULT_CHARSET));
                // Send one-way messages
                producer.sendOneway(msg);
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
<td align="left">topic_name</td>
<td align="left">Topic name, which can be copied under the <strong><code>Topic</code></strong> tab on the **Cluster** page in the console.</td>
</tr>
<tr>
<td align="left">TAG</td>
<td align="left">A parameter used to set the message tag.</td>
</tr>
</tbody></table>

>?For more information on batch sending or other scenarios, see the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip) or [RocketMQ documentation](https://rocketmq.apache.org/docs/simple-example/).

### Step 3. Consume messages

1. Create a consumer. TDMQ for RocketMQ supports two consumption modes: push and pull.
   - For consumers using the push mode:
   <dx-codeblock>
   :::  java
    // Instantiate the consumer
            DefaultMQPushConsumer pushConsumer = new DefaultMQPushConsumer(
                namespace,                                                  
                groupName,                                              
                new AclClientRPCHook(new SessionCredentials(accessKey, secretKey))); // ACL permission
            // Set the NameServer address
            pushConsumer.setNamesrvAddr(nameserver);
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
<td align="left">namespace</td>
<td align="left">Namespace name, which can be copied on the <strong>Namespace</strong> tab in the console. Its format is <strong>cluster ID + | + namespace</strong>.</td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <code>Group</code> tab on the **Cluster** page in the console.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the **Operation** column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list.</td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/b5ccd3b934f73a392a6b0855496cee10.png" alt="img"></td>
</tr>
</tbody></table>
   - For consumers using the pull mode:
<dx-codeblock>
:::  java
      // Instantiate the consumer
            DefaultLitePullConsumer pullConsumer = new DefaultLitePullConsumer(
                namespace,                                               
                groupName,                                             
                new AclClientRPCHook(new SessionCredentials(accessKey, secretKey)));
            // Set the NameServer address
            pullConsumer.setNamesrvAddr(nameserver);
            // Specify the first offset as the start offset for consumption
            pullConsumer.setConsumeFromWhere(ConsumeFromWhere.CONSUME_FROM_FIRST_OFFSET);
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
<td align="left">namespace</td>
<td align="left">Namespace name, which can be copied on the <strong>Namespace</strong> tab in the console. Its format is <strong>cluster ID + | + namespace</strong>.</td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <code>Group</code> tab on the **Cluster** page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the **Operation** column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list.</td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/709c03c8959d357a49833f87ed457c77.png" alt="img"></td>
</tr>
</tbody></table>
>?For more consumption mode information, see the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip) or [RocketMQ documentation](https://rocketmq.apache.org/docs/simple-example/).
2. Subscribed to messages. The subscription modes vary by consumption mode.
   - Subscription in push mode
   <dx-codeblock>
   :::  java
      // Subscribe to a topic
            pushConsumer.subscribe(topic_name, "*");
            // Register a callback implementation class to process messages pulled from the broker
            pushConsumer.registerMessageListener((MessageListenerConcurrently) (msgs, context) -> {
                // Message processing logic
                System.out.printf("%s Receive New Messages: %s %n", Thread.currentThread().getName(), msgs);
                // Mark the message as being successfully consumed and return the consumption status
                return ConsumeConcurrentlyStatus.CONSUME_SUCCESS;
            });
            // Start the consumer instance
            pushConsumer.start();
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
<td align="left">topic_name</td>
<td align="left">Topic name, which can be copied under the <strong><code>Topic</code></strong> tab on the **Cluster** page in the console.</td>
</tr>
<tr>
<td align="left">"*"</td>
<td align="left">If the subscription expression is left empty or specified as asterisk (*), all messages are subscribed to. `tag1 || tag2 || tag3` means subscribing to multiple types of tags.</td>
</tr>
</tbody></table>
   - Subscription in pull mode
<dx-codeblock>
:::  java
      // Subscribe to a topic
            pullConsumer.subscribe(topic_name, "*");
            // Start the consumer instance
            pullConsumer.start();
            try {
                System.out.printf("Consumer Started.%n");
                while (true) {
                    // Pull the message
                    List<MessageExt> messageExts = pullConsumer.poll();
                    System.out.printf("%s%n", messageExts);
                }
            } finally {
                pullConsumer.shutdown();
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
<td align="left">topic_name</td>
<td align="left">Topic name, which can be copied under the <strong><code>Topic</code></strong> tab on the **Cluster** page in the console.</td>
</tr>
<tr>
<td align="left">"*"</td>
<td align="left">If the subscription expression is left empty or specified as asterisk (*), all messages are subscribed to. `tag1 || tag2 || tag3` means subscribing to multiple types of tags.</td>
</tr>
</tbody></table>


### Step 4. View consumption details

Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
![img](https://qcloudimg.tencent-cloud.cn/raw/671cacbb946883f1777c0417e59fe424.png)



>?Above is a brief introduction to message publishing and subscription. For more information, see the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip) or [RocketMQ documentation](https://rocketmq.apache.org/docs/simple-example/)
