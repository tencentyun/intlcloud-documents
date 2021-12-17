## Overview

This document describes how to view the details of a created queue in the TDMQ for CMQ console.

## Directions

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the **region**, and click the ID of the target queue to enter the queue details page.

On the details page, you can query:

- Retained Messages: total number of messages with the active status in the queue (approximate value).
- Delayed Messages: if no consumers are online, the total number of delayed messages will be displayed as 0, and the actual value will be displayed after the consumers get online.
- Basic Information: queue name, ID, region, creation time, and modification time.
- Queue Attributes: you can click **Modify Configuration** in the top-right corner to modify the queue attributes.


  | Attribute | Description |
  | ---------------------- | ------------------------------------------------------------ |
  | Message lifecycle | This is the `msgRetentionSeconds` attribute of the queue. It is measured in seconds and ranges from 1 minute to 15 days. It specifies the period of time during which a message can be retained in the queue. After this period has elapsed since a message is sent to the queue, the message will become deletable (but it will not necessarily be deleted in time). For more information, see [Message Lifecycle](https://intl.cloud.tencent.com/document/product/1111/42987). |
  | Long-Polling waiting time for message receipt | This attribute is the long-polling waiting time. It is measured in seconds and ranges from 0 to 30 seconds. Just like with long polling of Ajax requests, a message consumption request will return a response only after a valid message is fetched or the long-polling time elapses. |
  | Hidden duration of fetched messages | This is the `VisibilityTimeout` attribute of the queue. It is measured in seconds and ranges from 1 to 43,200 seconds (1 second to 12 hours). Each message has a default `VisibilityTImeout`, which starts counting after a worker receives the message. If the worker fails to complete processing the message within the period specified by this attribute, the message will be sent to and processed by another worker. |
  | Maximum message size | This is the `MaxMsgSize` attribute of the queue. It is measured in KB and specifies the maximum length of the message body that can be sent to the queue. |
  | Maximum retained messages | This attribute specifies the maximum number of retained (undeleted) messages in a queue. The maximum number of retained messages in a queue is 100 million, and the minimum number is 1 million. If you need to increase the upper limit, contact technical support. |
  | QPS limit | This attribute indicates the frequency limit of calling the same API. |
  | Traffic limit | This attribute is the maximum throughput bandwidth of message production. If this limit is exceeded, the traffic will be throttled (the response time of production requests will increase). |
  | Dead letter queue | A dead letter queue (DLQ) is used to process messages that cannot be consumed normally. If consumption still fails after the maximum number of retries, it indicates that the consumer cannot consume a message under normal circumstances. At this point, the queue will not immediately discard the message; instead, it will send the message to a special queue of the consumer, i.e., DLQ. |

- Message Rewind: after your business successfully consumes and deletes a message, you can use this feature to consume the message again. For more information, see [Message Rewind](https://intl.cloud.tencent.com/document/product/1111/42997).

![](https://main.qcloudimg.com/raw/5d6a37e0b2c5097f413783eb0de1db6e.png)
