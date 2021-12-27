## Overview

Topic is a core concept in TDMQ for RocketMQ. It is usually used to categorize and manage various messages produced by the system in a centralized manner; for example, messages related to transactions can be placed in a topic named "trade" for other consumers to subscribe to.
In actual application scenarios, a topic often represents a business category. You can decide how to design different topics based on your system and data architectures.

This document describes how to use topics to categorize and manage messages in TDMQ for RocketMQ.

## Prerequisites

You have created a namespace.

## Directions

### Creating topic

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Click the **Topic** tab at the top, select a namespace, and click **Create** to enter the **Create Topic** page.
3. In the **Create Topic** window, enter the following information:
   ![](https://main.qcloudimg.com/raw/51c79615c68090464f867fe76abebe68.png)
   - Topic Name: enter the topic name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Type: select the message type, including general, globally sequential, and partitionally sequential. For more information on message types, see [Message Type](https://intl.cloud.tencent.com/document/product/1110/42957).
   - Remarks: enter the topic remarks.
4. Click **Submit**, and you can see the created topic in the topic list.

### Viewing topic details

1. In the topic list, click the number under **Number of Subscribed Groups** of the target topic.
2. You will be redirected to the group list, which displays the information of the groups subscribed to the topic.

### Querying topic

You can search for topics by topic name in the search box in the top-right corner of the **Topic** list page. TDMQ for RocketMQ will perform a fuzzy match and display the search results.

### Editing topic

1. In the topic list, click **Edit** in the **Operation** column of the target topic.
2. In the pop-up window, you can edit the topic remarks.
3. Click **Submit**.

### Deleting topic

> !After a topic is deleted, all unconsumed messages retained in it will be cleared; therefore, proceed with caution.

1. In the topic list, click **Delete** in the **Operation** column of the target topic.
2. In the pop-up window, click **Submit**.
