## Overview
In the TDMQ for Pulsar console, a subscription represents a specific consumer and its subscription to a topic. A consumer can consume all messages in a topic after subscribing to it. One subscription can subscribe to multiple topics; for example, after a subscription is created under a topic, it will subscribe to both the current topic and the automatically created retry queue topic.

This document describes how to manage the subscriptions to a topic in **Subscription Management** in TDMQ for Pulsar.

## Prerequisites

- You have created a namespace and a topic.
- You have created a message producer and consumer based on the SDK provided by TDMQ for Pulsar, and they run properly.

## Directions

### Viewing subscription details

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and click **Topic Management** on the left sidebar.
2. On the **Topic Management** list page, click **View Subscription** in the **Operation** column of the target topic to enter the subscription list.
3. In the subscription list, the first-level list displays all subscriptions to the current topic. After expanding the second-level list, you can see the consumer instances connected to each subscription and the consumption progress of each segment.
![](https://main.qcloudimg.com/raw/9a52b3f6b34eb19905ca3cc8d2d0db4c.png)

### Setting offset
1. In the subscription list, click **Set Offset** in the **Operation** column to manually set the consumer offset for each subscription by time (that is, specify the time point from which the consumers under the subscription start to consume messages).
2. Click **Submit**.
![](https://main.qcloudimg.com/raw/abc24bdebba5c70cbaee0d14ea40ab20.png)

### Recreating retry/dead letter queues

As you can manually delete a topic, if you want the deleted retry/dead letter queues to be created again by the system, you can click **Recreate Retry/Dead Letter Queues** in the **Operation** column of the subscription.

### Deleting subscription
>!When a subscription under a topic is deleted, if it has also subscribed to other topics (including the automatically created retry/dead letter queues), it will not be removed from such topics.

1. In the subscription list, click **More** > **Delete** in the **Operation** column of the target subscription. You can also select multiple subscriptions and click **Delete** at the top of the subscription list.
2. In the pop-up window, click **Submit**.
Force deletion: after this option is enabled, a subscription will be forcibly deleted even if it has active consumer connections.
<img src="https://main.qcloudimg.com/raw/ea9b6196088eee2182ef057d144d93c5.png" width="540px">

