## Overview

This document describes how to create a queue service and send a message in the TDMQ for CMQ console.

## Directions

### Creating queue

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the region, click **Create**, and configure the queue service attributes.
<img src="https://main.qcloudimg.com/raw/d7998a58a3e670943331bbd82f06794d.png" width="550px">


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

### Sending message

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the **region**, and click **Send Message** in the **Operation** column of the target queue.
3. Enter the message content and click **Send** to send a testing message to the recipient.
<img src="https://main.qcloudimg.com/raw/eca781dd9477419c66f8374488532a85.png" width="500px"><br> Message Content: enter the content to be sent of at least 1 byte. The maximum length is subject to the set `MaxMsgSize` attribute.

  
