## Overview

This document describes how to create a queue service from scratch and use the SDK for Java to test message sending and receiving. It helps you quickly understand the basic operations required for client access to TDMQ for CMQ.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create a queue service

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the region, click **Create**, and configure the queue service attributes.
   <img src="https://qcloudimg.tencent-cloud.cn/raw/bca2e55dcc0172d192894f345fcfc291.png" width="550px">
<table>
    <thead>
    <tr>
        <th>Attribute</th>
        <th>Description</th>
        <th>Value</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Queue Name</td>
        <td>It is the `QueueName` attribute of the queue.</td>
        <td>It is the unique identifier of a resource and can be used to differentiate API calls.
            It cannot be changed once the queue is created. It is case-insensitive and cannot end with `-retry` or `-dlq`.
        </td>
    </tr>
    <tr>
        <td>
            <nobr>Resource Tag</nobr>
        </td>
				<td>It is optional and can help you easily categorize and manage TDMQ for CMQ resources in many dimensions. For detailed usage, see <a href = "https://intl.cloud.tencent.com/document/product/1111/43007">Managing Resource with Tag</a>.</td>
        <td>-</td>
    </tr>		
    <tr>
        <td>Maximum Message Unacknowledged Time</td>
        <td>If the consumer client fails to acknowledge a received message within this time period, the server will automatically acknowledge the message.</td>
        <td>It ranges from 30 seconds to 12 hours.</td>
    </tr>
    <tr>
        <td>Long Polling Wait Time for Message Receipt</td>
        <td>It is the `PollingWaitSeconds` attribute of the queue. Just like with long polling of Ajax requests, a message consumption request will return a response only after a valid message is fetched or the long-polling time elapses.</td>
        <td>It ranges from 0 to 30 seconds. We recommend you set it to 3 seconds. A higher value may cause more duplicated messages.</td>
    </tr>
    <tr>
        <td>Hidden Duration of Fetched Message</td>
        <td>
            It is the `VisibilityTimeout` attribute of the queue. Each message has a default `VisibilityTImeout`, which starts counting after a worker receives a message. If the worker fails to complete processing the message within the period specified by this attribute, the message will be sent to and processed by another worker.
        </td>
        <td>It ranges from 1 second to 12 hours.</td>
    </tr>
    <tr>
        <td>Max Invisible Messages</td>
        <td>If the client fails to acknowledge messages in a timely manner, an excessive number of invisible messages are generated. The generation of invisible messages will consume the memory; therefore, a capacity upper limit is set for each queue.</td>
        <td>It is 100,000. If you need to increase the upper limit, contact technical support. </td>
    </tr>
     <tr>
        <td>Max Capacity for Heaped Messages</td>
        <td>Message heap is generally caused by the production speed being greater than the consumption speed or the consumption being blocked. The heap will use disk space; therefore, a capacity upper limit is set for each queue.</td>
        <td>It is 10 GB. If you need to increase the upper limit, contact technical support. </td>
    </tr>
    <tr>
        <td>Dead Letter Queue</td>
        <td>A dead letter queue is used to handle messages that cannot be consumed successfully after their retry limit has been reached. Rather than being discarded immediately, such messages will be sent to the consumer's specified dead letter queue.
        </td>
        <td>-</td>
    </tr>
    <tr>
        <td>Message Rewind</td>
        <td>If the message rewind feature is not enabled, a message consumed by a consumer and confirmed for deletion will be deleted immediately. When enabling this feature, you need to specify the rewindable time range.</td>
        <td>The rewindable time range must be equal to or shorter than the message lifecycle. We recommend you make it the same as the message lifecycle to facilitate troubleshooting.</td>
    </tr>
    <tr>
        <td>Rewindable Time Range</td>
        <td>If the message rewind feature is enabled, messages confirmed for deletion by the consumer will not be deleted immediately; instead, they will be stored for the maximum time configured here.</td>
        <td>It ranges from 1 to 15 days. A higher value may cause higher storage fees. The maximum rewindable time point is the current time minus the configured rewindable time range. Messages cannot be rewound if produced before this time.</td>
    </tr>
    <tr>
        <td>Rewindable Storage Space</td>
        <td>After the message rewind feature is enabled, if the volume of persistently stored messages exceeds this maximum storage space, messages will be deleted by time (the oldest data will be deleted first). </td>
        <td>It ranges from 1 to 10 GB. A higher value may cause higher storage fees.</td>
    </tr>
    </tbody>
</table>
3. Click **Submit**, and you can see the created queue service in the queue service list.

### Step 2. Use the SDK to send and receive messages

> ?The following takes Java as an example. For clients in other languages, see [API Overview](https://intl.cloud.tencent.com/document/product/1111/46396).

1. [Download the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip) and decompress it.
2. Import CMQ client dependencies.
<dx-codeblock>
:::  xml
<!-- cmq sdk --><!-- cmq sdk -->
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
<td>API call address, which can be copied from <b>Queue Service</b> > <b>API Request Address</b> in the <a href = "https://console.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fc16b1951c00d63b0f86cf8f4c25691c.png">
</td>
</tr>
<tr>
<td>SECRET_ID, SECRET_KEY</td>
<td>TencentCloud API key, which can be copied on the <b>Access Key</b> > <b>API Key Management</b> page in the <a href = "https://console.cloud.tencent.com/cam/overview">CAM console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/0def1c292b3dc79a320e3fc9921a979e.png">
</td>
</tr>
<tr>
<td>queueName</td>
<td>Queue name, which can be obtained on the <b>Queue Service</b> page in the <a href = "https://console.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.</td>
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
<td>API call address, which can be copied from <b>Queue Service</b> > <b>API Request Address</b> in the <a href = "https://console.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/fc16b1951c00d63b0f86cf8f4c25691c.png">
</td>
</tr>
<tr>
<td>SECRET_ID, SECRET_KEY</td>
<td>TencentCloud API key, which can be copied on the <b>Access Key</b> > <b>API Key Management</b> page in the <a href = "https://console.cloud.tencent.com/cam/overview">CAM console</a>.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/0def1c292b3dc79a320e3fc9921a979e.png">
</td>
</tr>
<tr>
<td>queueName</td>
<td>Queue name, which can be obtained on the <b>Queue Service</b> page in the <a href = "https://console.cloud.tencent.com/tdmq">TDMQ for CMQ console</a>.</td>
</tr>
</table>


>?Above is a brief introduction to message production and consumption. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip).
