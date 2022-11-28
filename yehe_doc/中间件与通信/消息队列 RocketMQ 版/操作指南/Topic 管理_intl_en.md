## Overview

Topic is a core concept in TDMQ for RocketMQ. It is usually used to categorize and manage various messages produced by the system in a centralized manner; for example, messages related to transactions can be placed in a topic named "trade" for other consumers to subscribe to.
In actual application scenarios, a topic often represents a business category. You can decide how to design different topics based on your system and data architectures.

This document describes how to use topics to categorize and manage messages in TDMQ for RocketMQ.

## Prerequisites

You have created a namespace.

## Directions

### Creating a topic

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Click the **Topic** tab at the top, select a namespace, and click **Create** to enter the **Create Topic** page.
3. In the **Create Topic** window, enter the following information:
   ![](https://qcloudimg.tencent-cloud.cn/raw/2e02cef152b8dc3ecf16d32614c8b1ad.png)
   - Topic Name: Enter the topic name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Type: Select the message type, including general, globally sequential, partitionally sequential, and delayed messages. For more information, see [Message Type](https://www.tencentcloud.com/document/product/1113/43106).
   - Partition Count: Select the number of partitions, which can be up to 32. Using multiple partitions can improve the production/consumption performance of a single topic but cannot guarantee the sequence.
   - Description: Enter the topic description.
4. Click **Submit**, and you can see the created topic in the topic list.

### Viewing subscribed groups

1. In the topic list, click the number under **Number of Subscribed Groups** of the target topic.
2. You will be redirected to the group list, which displays the information of the groups subscribed to the topic.

### Querying a topic

You can search for topics by topic name in the search box in the top-right corner of the **Topic** list page. TDMQ for RocketMQ will perform a fuzzy match and display the search results.

### Editing a topic

1. In the topic list, click **Edit** in the **Operation** column of the target topic.
2. In the pop-up window, you can edit the topic remarks.
3. Click **Submit**.

### Deleting a topic

> !After a topic is deleted, all unconsumed messages retained in it will be cleared; therefore, proceed with caution.

1. In the topic list, click **Delete** in the **Operation** column of the target topic.
2. In the pop-up window, click **Submit**.
