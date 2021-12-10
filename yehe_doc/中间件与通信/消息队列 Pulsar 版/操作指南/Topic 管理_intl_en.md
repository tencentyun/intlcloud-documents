## Overview

Topic is a core concept in TDMQ for Pulsar. It is usually used to categorize and manage various messages produced by the system in a centralized manner; for example, messages related to transactions can be placed in a topic named "trade" for other consumers to subscribe to.
In actual application scenarios, a topic often represents a business category. You can decide how to design different topics based on your system and data architectures.

This document describes how to use topics to categorize and manage messages in TDMQ for Pulsar.

## Prerequisites

You have created a namespace.

## Directions

### Creating topic

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and click **Topic Management** on the left sidebar.
2. On the **Topic Management** page, click **Create** to pop up the **Create Topic** window.
3. In the **Create Topic** window, enter the following information:
 - Topic Name: it can contain only letters, digits, hyphens, and underscores.
 - Type: select the message type, including general, globally sequential, and partitionally sequential. For more information on message types, see [Message Type](https://intl.cloud.tencent.com/document/product/1110/42957).
 - Number of Partitions: there are only one partition for globally sequential messages and 1–128 partitions for other message types.
 - Remarks: enter the topic remarks of up to 128 characters.
4. Click **Save**, and you can see the created topic in the topic list.
   ![](https://main.qcloudimg.com/raw/3a53fe8fa4ae2e0e1307b8fccf2afc8f.png)

### Querying topic

You can search for topics by topic name in the search box in the top-right corner of the [Topic Management](https://console.cloud.tencent.com/tdmq/topic) page. TDMQ for Pulsar will perform a fuzzy match and display the search results.

### Editing topic

1. In [Topic Management](https://console.cloud.tencent.com/tdmq/topic), click **Edit** in the **Operation** column of the target topic.
2. In the pop-up window, you can edit the number of topic partitions (which is 1 for globally sequential messages and cannot be edited) as well as the remarks.
3. Click **Submit**.

### Sending message

You can manually send a message to the specified topic in the TDMQ for Pulsar console.

1. In [Topic Management](https://console.cloud.tencent.com/tdmq/topic), click **Send Message** in the **Operation** column of the target topic.
2. Enter the message content of up to 64 KB in the pop-up window.
   ![](https://main.qcloudimg.com/raw/2962bfe289ab88a167fb8d94feed37fe.png)
3. Click **Submit** to send the message. After the message is sent, it can be consumed by any subscribers to the topic.

### Creating subscription

You can manually create a subscription in the TDMQ for Pulsar console.
1. In [Topic Management](https://console.cloud.tencent.com/tdmq/topic), click **Create Subscription** in the **Operation** column of the target topic.
2. Enter the subscription name and remarks in the pop-up window.
 - Subscription Name: it can contain only letters, digits, hyphens, and underscores.
 - Auto-Create Retry & Dead Letter Queue: you can choose whether to create a retry queue and a dead letter queue.
 - Remarks: enter remarks of up to 128 characters.
   ![](https://main.qcloudimg.com/raw/bc07c3f60f26b9e5521ec127cb171bea.png)
3. Click **Submit**.
   You can click **View Subscription** in the **Operation** column of a topic to view its subscriptions, and the subscription just created will be displayed in the list.

>?
>
>- If you select **Auto-Create Retry & Dead Letter Queue**, TDMQ for Pulsar will automatically create a retry queue and a dead letter queue, which will be displayed in the topic list as two new topics named "subscription name + RETRY" and "subscription name + DLQ" respectively.
>- For the concepts and usage of retry and dead letter queues, see [Retry Queue and Dead Letter Queue](https://intl.cloud.tencent.com/document/product/1110/42958).

### Deleting topic

>!After a topic is deleted, all unconsumed messages retained in it will be cleared; therefore, proceed with caution.

1. In **Topic Management**, click **More** > **Delete** in the **Operation** column of the target topic. You can also select multiple topics and click **Delete** at the top of the topic list.
2. In the pop-up window, click **Submit**.
Force deletion: after this option is enabled, a topic will be force deleted even if it has subscriptions.
<img src="https://main.qcloudimg.com/raw/017f18e218e06cf617b17ecd4450f113.png" width="600">

