## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Java as an example and helps you better understand the message sending and receiving processes.

<dx-alert infotype="explain" title="">
The following takes the Java client as an example. For clients in other languages, see [TDMQ for RocketMQ](https://intl.cloud.tencent.com/document/product/1113/45953).
</dx-alert>

## Prerequisites

- [You have created the required resources.](https://intl.cloud.tencent.com/document/product/1113/43119)
- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo.](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip)

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

#### 1. Create a message producer
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
<td align="left">Namespace name, which can be copied under the <strong>Namespace</strong> tab on the cluster details page in the console. Its format is <strong>cluster ID + | + namespace</strong>.</td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <strong>Group</strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console.</td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/3151b0fe8307ce8b22891f394a99e630.png" alt="img"></td>
</tr>
</tbody></table>


#### 2. Send messages

Messages can be sent in the sync, async, or one-way mode.

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
<td align="left">Topic name, which can be copied under the <strong> <code>Topic</code></strong> tab on the cluster details page in the console.</td>
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
<td align="left">Topic name, which can be copied under the <strong> <code>Topic</code></strong> tab on the cluster details page in the console.</td>
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
	 Send one-way messages
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
<td align="left">Topic name, which can be copied under the <strong> <code>Topic</code></strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">TAG</td>
<td align="left">A parameter used to set the message tag.</td>
</tr>
</tbody></table>

>?For more information on batch sending or other scenarios, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip) .


### Step 3. Consume messages

#### 1. Create a consumer
TDMQ for RocketMQ supports two consumption modes: push and pull.
- For consumers using the push mode:
<dx-codeblock>
:::  java
// Instantiate the consumer
DefaultMQPushConsumer pushConsumer = new DefaultMQPushConsumer(
	 namespace,                                                  
	 groupName,                                              
	 new AclClientRPCHook(new SessionCredentials(accessKey, secretKey))); //ACL permission
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
<td align="left">Namespace name, which can be copied on the <strong>Namespace</strong> tab on the cluster details page in the console. Its format is <strong>cluster ID + | + namespace</strong>.</td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <strong>Group</strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console.</td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/3151b0fe8307ce8b22891f394a99e630.png" alt="img"></td>
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
<td align="left">Namespace name, which can be copied on the <strong>Namespace</strong> tab on the cluster details page in the console. Its format is <strong>cluster ID + | + namespace</strong>.</td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <strong>Group</strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console.</td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/3151b0fe8307ce8b22891f394a99e630.png" alt="img"></td>
</tr>
</tbody></table>

>?For more consumption mode information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip).

#### 2. Subscribe to messages
The subscription modes vary by consumption mode.

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
<td align="left">Topic name, which can be copied under the <strong> <code>Topic</code></strong> tab on the cluster details page in the console.</td>
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
<td align="left">Topic name, which can be copied under the <strong> <code>Topic</code></strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">"*"</td>
<td align="left">If the subscription expression is left empty or specified as asterisk (*), all messages are subscribed to. `tag1 || tag2 || tag3` means subscribing to multiple types of tags.</td>
</tr>
</tbody></table>



### Step 4. View consumption details

Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
![](https://qcloudimg.tencent-cloud.cn/raw/0edaf07ec7dba3e634fba03f188d308e.png)

>?Above is a brief introduction to message publishing and subscription. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip). 
