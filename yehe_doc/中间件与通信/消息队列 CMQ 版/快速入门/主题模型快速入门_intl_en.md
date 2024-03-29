## Overview

This document describes how to create a topic and use the SDK for Java to test message sending and receiving, so as to help you quickly understand the basic operations required for client access to TDMQ for CMQ.

## Prerequisite

You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create a topic
1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Topic Subscription** on the left sidebar, select a region, click **Create**, and enter the topic name.
	![](https://qcloudimg.tencent-cloud.cn/raw/34011988c4d2d43b002da28c732b1208.png)
	- Topic Name: It can contain up to 64 letters, digits, "-", or "_", and must start with a letter. It cannot be modified once created.
	- Message Heap: If this option is enabled, messages that failed to be pushed to or received by the subscriber will be temporarily heaped in the topic.
	- Message Filter Type:
		- Tag: TDMQ for CMQ can match message tags for production and subscription, which can be used for message filtering. For detailed rules, see [Tag Key Matching Feature Description](https://intl.cloud.tencent.com/document/product/1111/43003).
		- Routing matching: The binding key and routing key are used together and are fully compatible with the topic match mode of RabbitMQ. The routing key carried when a message is sent is added by the client, and the binding key carried when a subscription is created is the binding relationship between the topic and the subscriber. For detailed rules, see [Routing Key Matching Feature Description](https://intl.cloud.tencent.com/document/product/1111/43004).
	- Resource Tag: It is optional and can help you easily categorize and manage TDMQ for CMQ resources in many dimensions. For detailed usage, see [Managing Resource with Tag](https://intl.cloud.tencent.com/document/product/1111/43007).
3. Click **Submit**, and you can see the created topic in the topic subscription list.



### Step 2. Create a subscription

A topic can publish messages only if it is subscribed to by at least one subscriber. If there are no subscribers, messages in the topic will not be delivered, and message publishing will be meaningless.

1. On the **[Topic Subscription](https://console.cloud.tencent.com/tdmq/cmq-queue)** page, click the ID of the topic you just created to enter the topic details page.
2. Select the **Subscriber** tab at the top, click **Create**, and enter the subscriber information.
   ![](https://qcloudimg.tencent-cloud.cn/raw/30fd0b2366a0462242dc0fb24886c7a2.png)
   - Subscriber Type
     - Queue service: you can select a queue for the subscriber to receive published messages.
     - URL: Subscribers can process messages on their own without using queues. For more information, see [Delivering Message](https://intl.cloud.tencent.com/document/product/406/7420).
   - Subscriber Tag: When adding a subscriber, you can add filter tags (FilterTag), so that the subscriber can receive only messages with the specified tags. Up to five tags can be added for one subscriber. As long as a tag matches a topic filter tag, the subscriber can receive messages delivered by the topic. If a message does not have any tag, the subscriber cannot receive it.
     - Tag: For detailed rules, see [Tag Key Matching Feature Description](https://intl.cloud.tencent.com/document/product/1111/43003).
     - Routing matching: For detailed rules, see [Routing Key Matching Feature Description](https://intl.cloud.tencent.com/document/product/1111/43004).
   - Retry Policy: After a message is published by a topic, it will automatically be pushed to the subscription. If the push fails, there are two retry policies:
     - **Backoff retry**: An attempt will be retried three times at random intervals between 10 and 20 seconds. After three retries, the message will be discarded for the subscriber and will not be retried again.
     - **Exponential decay retry**: An attempt will be retried 176 times at exponentially increasing intervals: 2^0 second, 2^1 seconds, ..., 512 seconds, 512 seconds, ..., 512 seconds. The total retry duration is 1 day. This is the default retry policy.
3. Click **Submit**, and you can see the created subscriber in the subscriber list.

### Step 3. Use the SDK to send and receive messages

> ?The following takes Java as an example. For clients in other languages, see the [SDK Documentation](https://intl.cloud.tencent.com/document/product/1111/46396).

1. [Download the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip) and decompress it.
2. Import CMQ client dependencies.
<dx-codeblock>
:::  xml
 <!-- cmq sdk -->
<dependency>
​    <groupId>com.qcloud</groupId>
​    <artifactId>cmq-http-client</artifactId>
​    <version>1.0.7</version>
</dependency>

<!-- TencentCloud API SDK -->
<dependency>
​    <groupId>com.tencentcloudapi</groupId>
​    <artifactId>tencentcloud-sdk-java</artifactId>
​    <version>3.1.423</version>
</dependency>

:::
</dx-codeblock>
3. Create a topic object.
<dx-codeblock>
:::  java
 Account account = new Account(SERVER_ENDPOINT, SECRET_ID, SECRET_KEY);
 Topic topic = account.getTopic(topicName);
:::
</dx-codeblock>
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>SERVER_ENDPOINT</td>
<td>API call address, which can be copied from <b>Topic Subscription</b> > <b>API Request Address</b> in the <a href = "https://console.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/910150612a00a6461ff923cd53a1ec97.png">
</td>
</tr>
<tr>
<td>SECRET_ID, SECRET_KEY</td>
<td>TencentCloud API key, which can be copied on the <b>Access Key</b> > <b>Manage API Key</b> page in the <a href = "https://console.intl.cloud.tencent.com/cam/overview">CAM console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/82946cd1e7b1d46a9ccb06ef171137da.png">
</td>
</tr>
<tr>
<td>topicName</td>
<td>Topic subscription name, which can be obtained on the <b>Topic Subscription</b> page in the <a href = "https://console.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.</td>
</tr>
</table>

4. Send tag messages.
<dx-codeblock>
:::  java
      String msg = "hello client, this is a message. tag=TAG1. Time:" + new Date();
      List<String> tags = Collections.singletonList("TAG1");
      String messageId = topic.publishMessage(msg, tags, null);
:::
</dx-codeblock>
5. Send route messages.
<dx-codeblock>
:::  java
      String msg = "hello client, this is a message. route(abc) Time:" + new Date();
      String messageId = topic.publishMessage(msg, "abc");
:::
</dx-codeblock>
6. Consume messages in the queue corresponding to the subscriber.
<dx-codeblock>
:::  java
      Account account = new Account(SERVER_ENDPOINT, SECRET_ID, SECRET_KEY);
      Queue queue = account.getQueue(queueName);
      Message message = queue.receiveMessage();
      // Successfully consumed messages are deleted. Retained messages can be delivered again after a certain period of time
      queue.deleteMessage(message.receiptHandle);
:::
</dx-codeblock>

>?The above is a brief introduction to the message production and consumption in TDMQ for CMQ. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip).
