## Overview

This document describes how to create a queue service from scratch and use the SDK for TCP to test message sending and receiving, so as to help you quickly understand the basic operations required for client access to TDMQ for CMQ.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create a queue service

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the region, click **Create**, and configure the queue service attributes.
<img src="https://qcloudimg.tencent-cloud.cn/raw/bca2e55dcc0172d192894f345fcfc291.png" width="550px">
 
 
   | Attribute | Description | Value |
   | :--------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
   | <nobr>Queue name</nobr> | This is the `QueueName` attribute of the queue. | It is a unique identifier of a resource and is used to specify a queue when APIs are called for operations. It cannot be modified after the queue is created. To avoid confusion, queues that have the same name in the same letter case cannot be created. When entering the name, pay attention to the letter case and do not end it with `-retry` or `-dlq`. |
   | Message lifecycle | This is the `msgRetentionSeconds` attribute of the queue. It specifies the period of time during which a message can be retained in the queue. After this period has elapsed since a message is sent to the queue, the message will become deletable (but it will not necessarily be deleted in time). | It is measured in seconds and ranges from 60 to 1296000 seconds (i.e., 1 minute to 15 days). |
   | Long-Polling waiting time for message receipt | This is the `PollingWaitSeconds` attribute of the queue. Just like with long polling of Ajax requests, a message consumption request will return a response only after a valid message is fetched or the long-polling time elapses. | It is measured in seconds and ranges from 0 to 30 seconds. |
   | Hidden duration of fetched messages | This is the `VisibilityTimeout` attribute of the queue. Each message has a default `VisibilityTImeout`, which starts counting after a worker receives the message. If the worker fails to complete processing the message within the period specified by this attribute, the message will be sent to and processed by another worker. | It is measured in seconds and ranges from 1 to 43,200 seconds (i.e., 1 second to 12 hours). |
   | Dead letter queue | A dead letter queue (DLQ) is used to process messages that cannot be consumed normally. If consumption still fails after the maximum number of retries, it indicates that the consumer cannot consume a message under normal circumstances. At this point, the queue will not immediately discard the message; instead, it will send the message to a special queue of the consumer, i.e., DLQ. | -                                                            |
   | Maximum retained messages | This attribute specifies the maximum number of retained (undeleted) messages in a queue. | The maximum number of retained messages in a queue is 100 million, and the minimum number is 1 million. If you need to increase the upper limit, contact technical support. |
   | Message rewind | If the "message rewind" feature is not enabled, a message consumed by a consumer and confirmed for deletion will be deleted immediately. When enabling this feature, you need to specify the "rewind time range". | The rewindable time range must be equal to or shorter than the message lifecycle. You are recommended to set it to the same as the message lifecycle to facilitate troubleshooting. |
   | Specified time range | You can configure this item after enabling message rewind, which is disabled by default in the console. After it is enabled, the default value will be the same as the message lifecycle value. | It ranges from 1 second to 15 days. The maximum rewindable time point is the current time minus the configured rewindable time range. The messages cannot be rewound if produced before this time. |

3. Click **Submit**, and you can see the created queue service in the queue service list.

### Step 2. Use the SDK to send and receive messages

1. [Download the demo](https://github.com/tencentyun/cmq-java-tcp-sdk) and decompress it.
2. Configure the parameters of the message producing program `ProducerDemo.java`.
   ```java
    Producer producer = new Producer();
           // Private network address: http://{region}.mqadapter.cmq.tencentyun.com. Access from CVM in VPC is supported
           // Public network address: https://cmq-{region}.public.tencenttdmq.com
           producer.setNameServerAddress("https://cmq-****");
           // Set "SecretId" obtained in the console (required)
           producer.setSecretId("****");
           // Set "SecretKey" obtained in the console (required)
           producer.setSecretKey("****");
           // Set the signing method (optional and SHA1 by default)
           producer.setSignMethod(ClientConfig.SIGN_METHOD_SHA256);
           // Set the number of retries upon message sending failure (0: no retry; default value: 2)
           producer.setRetryTimesWhenSendFailed(3);
           // Set the request timeout time (default value: 3000ms)
           producer.setRequestTimeoutMS(5000);
           // Target queue created in the console
           String queue = "****";
   ```
   
	 
   | Parameter | Description |
   | ------------------- | ------------------------------------------------------------ |
   | NameServerAddress | API call address, which can be copied from **Queue Service** > **API Request Address** in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq). <img src="https://qcloudimg.tencent-cloud.cn/raw/fc16b1951c00d63b0f86cf8f4c25691c.png" width="400px"> |
   | SecretId, SecretKey | TencentCloud API key, which can be copied from **Access Key** > **API Key Management** in the [CAM console](https://console.cloud.tencent.com/cam/overview). ![](https://qcloudimg.tencent-cloud.cn/raw/0def1c292b3dc79a320e3fc9921a979e.png) |
   | queue | Queue name, which can be obtained on the **Queue Service** list page in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq). |
   
3. Configure the parameters of the message consuming program `SubscribeDemo.java`.

   ```java
   Consumer consumer = new Consumer();
           // Private network address: http://{region}.mqadapter.cmq.tencentyun.com. Access from CVM in VPC is supported
           // Public network address: https://cmq-{region}.public.tencenttdmq.com
           consumer.setNameServerAddress("http://cmq-****");
           // Set "SecretId" obtained in the console (required)
           consumer.setSecretId("****");
           // Set "SecretKey" obtained in the console (required)
           consumer.setSecretKey("****");
           // Set the signing method (optional and SHA1 by default)
           consumer.setSignMethod(ClientConfig.SIGN_METHOD_SHA256);
           // Maximum number of messages to be pulled in batches. The value range is 1–16
           consumer.setBatchPullNumber(16);
           // Set the waiting time when there is no message (default value: 10s). The specific waiting time can be passed in the `consumer.receiveMsg` and other methods
           consumer.setPollingWaitSeconds(6);
           // Set the request timeout time (default value: 3000ms)
           // If the waiting time is set to 6s and the timeout period is 5000 ms, the final timeout period will be (6*1000+5000) ms
           consumer.setRequestTimeoutMS(5000);
   
           // Name of the queue from which to pull messages
           final String queue = "****";
   ```
   
   The parameter configuration is the same as that of the message producing program.
   
4. Run the message producing program `ProducerDemo.java`, and the result of successful execution is as follows.

	 ![](https://main.qcloudimg.com/raw/60deede4bafd476e6883f21a943f8fad.png)

5. Run the message consuming program `ConsumerDemo.java`, and the result of successful execution is as follows.

	 ![](https://main.qcloudimg.com/raw/91bfa8685a3ba390a117398a8e969095.png)

6. Observe the monitoring data on the **Queue Service** > **Monitoring** page in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq).



