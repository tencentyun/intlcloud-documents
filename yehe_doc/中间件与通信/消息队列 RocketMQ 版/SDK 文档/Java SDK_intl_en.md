## Overview

This document describes how to use open-source SDK to send and receive messages using the SDK for Java as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1112/43069).
- [You have installed JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip)

## Directions

### Step 1. Install the Java dependent library

Introduce dependencies in a Java project and add the following dependencies to the `pom.xml` file. This document uses a Maven project as an example.
>?The dependency version must be v4.6.1 or later.
>
```xml
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
```

### Step 2. Produce messages

#### 1. Create message producers

   ```java
   // Instantiate the message producers
   DefaultMQProducer producer = new DefaultMQProducer(
       namespace, 
       groupName,
       new AclClientRPCHook(new SessionCredentials(accessKey, secretKey)) // ACL permission
   );
   // Set the NameServer address
   producer.setNamesrvAddr(nameserver);
   // Start the producer instances
   producer.start();
   ```

   | Parameter       | Description                                                         |
   | :--------- | :----------------------------------------------------------- |
   | namespace  | Namespace name in the format of **cluster ID + \| + namespace**, which can be copied under the **Namespace** tab on the cluster details page in the console. |
   | groupName  | Producer group name, which can be copied under the `Group` tab on the cluster details page in the console.         |
   | nameserver | Cluster access address, which can be obtained in the console by clicking **Access Address** in the **Operation** column of the cluster list on the **Cluster** page. |
   | secretKey  | Role name, which can be copied on the **[Role Management]](https://console.cloud.tencent.com/tdmq/role)** page. |
   | accessKey  | Role token, which can be copied in the **Token** column on the**[Role Management](https://console.cloud.tencent.com/tdmq/role)** page. ![img](https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png) |

#### 2. Send messages

Messages can be sent in the sync, async, or one-way mode.

- Sync sending

```java
for (int i = 0; i < 10; i++) {
	 // Create a message instance and set the topic and message content
	 Message msg = new Message(topic_name, "TAG", ("Hello RocketMQ " + i).getBytes(RemotingHelper.DEFAULT_CHARSET));
	 // Send the message
	 SendResult sendResult = producer.send(msg);
	 System.out.printf("%s%n", sendResult);
}
```

| Parameter       | Description                                                         |
| :--------- | :-------------------------------------------------------- |
| topic_name | Topic name, which can be copied under the **`Topic`** tab on the cluster details page in the console. |
| TAG        | A parameter used to set the message tag.                                       |

- Async sending

```java
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
```

| Parameter       | Description                                                         |
| :--------- | :-------------------------------------------------------- |
| topic_name | Topic name, which can be copied under the **`Topic`** tab on the cluster details page in the console. |
| TAG        | A parameter used to set the message tag.                                       |

- One-way sending

```java
for (int i = 0; i < 10; i++) {
	 // Create a message instance and set the topic and message content
	 Message msg = new Message(topic_name, "TAG", ("Hello RocketMQ " + i).getBytes(RemotingHelper.DEFAULT_CHARSET));
	 Send one-way messages
	 producer.sendOneway(msg);
}
```

| Parameter       | Description                                                         |
| :--------- | :-------------------------------------------------------- |
| topic_name | Topic name, which can be copied under the **`Topic`** tab on the cluster details page in the console. |
| TAG        | A parameter used to set the message tag.                                       |

>?For more information on batch sending or other scenarios, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip) or [RocketMQ documentation](https://rocketmq.apache.org/docs/simple-example/).


### Step 3. Consume messages

#### 1. Create a consumer
TDMQ for RocketMQ supports two consumption modes: push and pull.

- For consumers using the push mode:

```java
// Instantiate the consumer
DefaultMQPushConsumer pushConsumer = new DefaultMQPushConsumer(
	 namespace,                                                  
	 groupName,                                              
	 new AclClientRPCHook(new SessionCredentials(accessKey, secretKey))); //ACL permission
// Set the NameServer address
pushConsumer.setNamesrvAddr(nameserver);
```

| Parameter       | Description                                                         |
| :--------- | :----------------------------------------------------------- |
| namespace  | Namespace name in the format of **cluster ID + \| + namespace**, which can be copied under the **Namespace** tab on the cluster details page in the console. |
| groupName  | Producer group name, which can be copied under the `Group` tab on the cluster details page in the console.         |
| nameserver | Cluster access address, which can be obtained in the console by clicking **Access Address** in the **Operation** column of the cluster list on the **Cluster** page. |
| secretKey  | Role name, which can be copied on the **[Role Management]](https://console.cloud.tencent.com/tdmq/role)** page. |
| accessKey  | Role token, which can be copied in the **Token** column on the**[Role Management](https://console.cloud.tencent.com/tdmq/role)** page. ![img](https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png) |

- For consumers using the pull mode:

```java
// Instantiate the consumer
DefaultLitePullConsumer pullConsumer = new DefaultLitePullConsumer(
	 namespace,                                               
	 groupName,                                             
	 new AclClientRPCHook(new SessionCredentials(accessKey, secretKey)));
// Set the NameServer address
pullConsumer.setNamesrvAddr(nameserver);
// Specify the first offset as the start offset for consumption
pullConsumer.setConsumeFromWhere(ConsumeFromWhere.CONSUME_FROM_FIRST_OFFSET);
```

| Parameter       | Description                                                         |
| :--------- | :----------------------------------------------------------- |
| namespace  | Namespace name in the format of **cluster ID + \| + namespace**, which can be copied under the **Namespace** tab on the cluster details page in the console. |
| groupName  | Producer group name, which can be copied under the `Group` tab on the cluster details page in the console.         |
| nameserver | Cluster access address, which can be obtained in the console by clicking **Access Address** in the **Operation** column of the cluster list on the **Cluster** page. |
| secretKey  | Role name, which can be copied on the **[Role Management]](https://console.cloud.tencent.com/tdmq/role)** page. |
| accessKey  | Role token, which can be copied in the **Token** column on the**[Role Management](https://console.cloud.tencent.com/tdmq/role)** page. ![img](https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png) |

>?For more consumption mode information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip) or [RocketMQ documentation](https://rocketmq.apache.org/docs/simple-example/).

#### 2. Subscribe to messages
The subscription modes vary by consumption mode.

- Subscription in push mode

```java
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
```

| Parameter       | Description                                                         |
| :--------- | :----------------------------------------------------------- |
| topic_name | Topic name, which can be copied under the **`Topic`** tab on the cluster details page in the console. |
| "*"        | If the subscription expression is left empty or specified as asterisk (*), all messages are subscribed to. `tag1 \|\| tag2 \|\| tag3` means subscribing to multiple types of tags. |

- Subscription in pull mode

```java
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
```

| Parameter       | Description                                                         |
| :--------- | :----------------------------------------------------------- |
| topic_name | Topic name, which can be copied under the **`Topic`** tab on the cluster details page in the console. |
| "*"        | If the subscription expression is left empty or specified as asterisk (*), all messages are subscribed to. `tag1 \|\| tag2 \|\| tag3` means subscribing to multiple types of tags. |



### Step 4. View consumption details

Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
![img](https://main.qcloudimg.com/raw/7187da67219534d767206553e2a383ab.png)

>?Above is a brief introduction to message publishing and subscription. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-java-sdk-demo.zip) or [RocketMQ documentation](https://rocketmq.apache.org/docs/simple-example/)
