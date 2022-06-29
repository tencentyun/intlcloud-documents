## Overview

This document describes how to create a queue service and send a message in the TDMQ for CMQ console.

## Directions

### Creating queue

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the region, click **Create**, and configure the queue service attributes.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cfaf3be14bef7b8768c1940daf7b7cb5.png" width="550px">
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
        <td>Message Lifecycle</td>
        <td>It is the `msgRetentionSeconds` attribute of the queue. <b>It is merged with the message rewindable time parameter in TDMQ for CMQ and can take effect only after message rewind is enabled.</b> It specifies the period of time during which a message can be retained in the queue. After this period has elapsed since a message is sent to the queue, the message will become deletable (but it will not necessarily be deleted in time).
        </td>
        <td>It is measured in seconds and ranges from 60 to 1,296,000 seconds (i.e., 1 minute to 15 days).</td>
    </tr>
    <tr>
        <td>Maximum Message Unacknowledged Time</td>
        <td>It ranges from 30 seconds to 12 hours. If the consumer client fails to acknowledge a received message within this time period, the server will automatically acknowledge the message.</td>
        <td>It is measured in seconds and ranges from 30 to 43,200 seconds (i.e., 30 seconds to 12 hours).</td>
    </tr>
    <tr>
        <td>Long Polling Wait Time for Message Receipt</td>
        <td>It is the `PollingWaitSeconds` attribute of the queue. Just like with long polling of Ajax requests, a message consumption request will return a response only after a valid message is fetched or the long-polling time elapses.</td>
        <td>It is measured in seconds and ranges from 0 to 30 seconds.</td>
    </tr>
    <tr>
        <td>Hidden Duration of Fetched Message</td>
        <td>
            It is the `VisibilityTimeout` attribute of the queue. Each message has a default `VisibilityTImeout`, which starts counting after a worker receives a message. If the worker fails to complete processing the message within the period specified by this attribute, the message will be sent to and processed by another worker.
        </td>
        <td>It is measured in seconds and ranges from 1 to 43,200 seconds (i.e., 1 second to 12 hours). </td>
    </tr>
    <tr>
        <td>Dead Letter Queue</td>
        <td>A dead letter queue (DLQ) is used to process messages that cannot be consumed normally. If consumption still fails after the maximum number of retries, the consumer cannot consume a message under normal circumstances.
            At this point, the queue will not immediately discard the message; instead, it will send the message to a special queue of the consumer, i.e., DLQ.
        </td>
        <td>-</td>
    </tr>
    <tr>
        <td>Max Heaped Messages</td>
        <td>It specifies the maximum number of heaped (undeleted) messages in a queue.</td>
        <td>The maximum number of heaped messages in a queue is 100 million, and the minimum number is 1 million. If you need to increase the upper limit, contact technical support. </td>
    </tr>
    <tr>
        <td>Message Rewind</td>
        <td>If the message rewind feature is not enabled, a message consumed by a consumer and confirmed for deletion will be deleted immediately. When enabling this feature, you need to specify the rewindable time range.</td>
        <td>The rewindable time range must be equal to or shorter than the message lifecycle. We recommend you make it the same as the message lifecycle to facilitate troubleshooting.</td>
    </tr>
    <tr>
        <td>Rewindable Time Range</td>
        <td>The time range can be configured after message rewind is enabled. Within this time range, as long as the message storage space is not used up, messages will be retained persistently.</td>
        <td>It ranges from 1 second to 15 days. The maximum rewindable time point is the current time minus the configured rewindable time range. Messages cannot be rewound if produced before this time.</td>
    </tr>
    <tr>
        <td>Rewindable Storage Space</td>
        <td>The storage space can be configured to save storage costs after message rewind is enabled. After the volume of rewindable messages reaches the specified size, the messages will be deleted by production time.</td>
        <td>It ranges from 1 to 10 GB. The maximum rewindable time point is the current time minus the configured rewindable time range. Messages cannot be rewound if produced before this time.</td>
    </tr>
    </tbody>
</table>

> ? To help you use TDMQ for CMQ more reasonably, we made the following adjustments on April 12, 2022 (which don't affect your ongoing production and consumption behaviors):
> 
>- The limitation on the message lifecycle in the queue attributes was removed. For newly created queues, the length of the original message lifecycle is the same as the rewindable time. This means that no matter whether a message is confirmed for deletion by the client, it will be retained persistently for rewind in case of exceptions.
>- The configuration item of maximum message unacknowledged time was added. If the consumer client fails to acknowledge a received message within this time period, the server will automatically acknowledge the message.

3. Click **Submit**, and you can see the created queue service in the queue service list

> ?
> - Visible Messages: A general message (non-delayed message) is visible at first when it is sent to a general message queue. After being fetched, if the message has not been deleted after the visibility timeout, it will become visible again. There is a 30–60s delay in data refresh.
> - Invisible Messages: After a visible message is fetched, it will be made invisible in its hidden duration. There is a 30–60s delay in data refresh.
>
> For the definitions of visible and invisible messages in TDMQ for CMQ, see [Message Lifecycle](https://intl.cloud.tencent.com/document/product/1111/42987).

### Sending message

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Queue Service** on the left sidebar, select the **region**, and click **Send Message** in the **Operation** column of the target queue.
3. Enter the message content and click **Send** to send a testing message to the recipient.
   ![](https://qcloudimg.tencent-cloud.cn/raw/cda9f906a152a8fb6e98a3c47d3f9d8b.png)
> ? Message Content: Enter the content to be sent of at least 1 byte. The maximum length is subject to the configured **Max Message Size** attribute.

  
