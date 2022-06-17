## Overview

This document uses the SDK for Java as an example to describe how to connect the client to TDMQ for CMQ and send/receive messages.

## Prerequisites

- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo.](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip)

## Queue Model
### Directions
1. Create a queue service in the console as instructed in [Queue Management](https://intl.cloud.tencent.com/document/product/1111/42994).
2. Import CMQ client dependencies.
<dx-codeblock>
:::  xml
<!-- cmq sdk -->
<dependency>
    <groupId>com.qcloud</groupId>
    <artifactId>cmq-http-client</artifactId>
    <version>1.0.7</version>
</dependency>

<!-- TencentCloud API sdk -->
<dependency>
    <groupId>com.tencentcloudapi</groupId>
    <artifactId>tencentcloud-sdk-java</artifactId>
    <version>3.1.423</version>
</dependency>

:::
</dx-codeblock>
3. Send messages.
<dx-codeblock>
:::  java
   Account account = new Account(SERVER_ENDPOINT, SECRET_ID, SECRET_KEY);
   Queue queue = account.getQueue(queueName);
   String msg = "hello client, this is a message. Time:" + new Date();
   CmqResponse response = queue.send(msg);
:::
</dx-codeblock>
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>SERVER_ENDPOINT</td>
<td>API call address, which can be copied from <b>Queue Service</b> > <b>API Request Address</b> in the <a href = "https://console.intl.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/282b35a8eeff075cd664d433cb770439.png">
</td>
</tr>
<tr>
<td>SECRET_ID, SECRET_KEY</td>
<td>TencentCloud API key, which can be copied on the <b>Access Key</b> > <b>API Key Management</b> page in the <a href = "https://console.intl.cloud.tencent.com/cam/overview">CAM console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/e256875df075dbb08d6904ff8e12877e.png">
</td>
</tr>
<tr>
<td>queueName </td>
<td>Queue name, which can be obtained on the <b>Queue Service</b> page in the <a href = "https://console.intl.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.</td>
</tr>
</table> 
4. Consume messages.
<dx-codeblock>
:::  java
   Account account = new Account(SERVER_ENDPOINT, SECRET_ID, SECRET_KEY);
   Queue queue = account.getQueue(queueName);
   Message message = queue.receiveMessage();
   // Successfully consumed messages are deleted. Retained messages can be delivered again after a certain period of time
   queue.deleteMessage(message.receiptHandle);
:::
</dx-codeblock>
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>SERVER_ENDPOINT</td>
<td>API call address, which can be copied from <b>Queue Service</b> > <b>API Request Address</b> in the <a href = "https://console.intl.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/03650ee4728ee3a1bcd5a05aadec1af2.png">
</td>
</tr>
<tr>
<td>SECRET_ID, SECRET_KEY</td>
<td>TencentCloud API key, which can be copied on the <b>Access Key</b> > <b>API Key Management</b> page in the <a href = "https://console.intl.cloud.tencent.com/cam/overview">CAM console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/a60335230ab808d18701a3f4b42c4848.png">
</td>
</tr>
<tr>
<td>queueName </td>
<td>Queue name, which can be obtained on the <b>Queue Service</b> page in the <a href = "https://console.intl.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.</td>
</tr>
</table> 
   

## Topic Model
### Directions
1. Create resources in the console.
   1. Create a topic in the console as instructed in [Topic Management](https://intl.cloud.tencent.com/document/product/1111/43000).
   2. Create a subscriber for the topic as instructed in [Subscription Management](https://intl.cloud.tencent.com/document/product/1111/43001).
2. Import CMQ client dependencies.
<dx-codeblock>
:::  xml
<!-- cmq sdk -->
<dependency>
    <groupId>com.qcloud</groupId>
    <artifactId>cmq-http-client</artifactId>
    <version>1.0.7</version>
</dependency>

<!-- TencentCloud API sdk -->
<dependency>
    <groupId>com.tencentcloudapi</groupId>
    <artifactId>tencentcloud-sdk-java</artifactId>
    <version>3.1.423</version>
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
<td>API call address, which can be copied from <b>Queue Service</b> > <b>API Request Address</b> in the <a href = "https://console.intl.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/12c353b93a1d2d13e81ba85ad23bb61e.png">
</td>
</tr>
<tr>
<td>SECRET_ID, SECRET_KEY</td>
<td>TencentCloud API key, which can be copied on the <b>Access Key</b> > <b>API Key Management</b> page in the <a href = "https://console.intl.cloud.tencent.com/cam/overview">CAM console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/01deb72dc6437ec5625775ad0043ac2e.png">
</td>
</tr>
<tr>
<td>topicName </td>
<td>Topic subscription name, which can be obtained on the <b>Topic Subscription</b> page in the <a href = "https://console.intl.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.</td>
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

>?Above is a brief introduction to message production and consumption in two models. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip).
