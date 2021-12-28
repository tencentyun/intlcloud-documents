## Overview

A group is used to identify a type of consumers, which usually consume the same type of messages and use the same message subscription logic.

This document describes how to create, delete, and query a queue in the TDMQ for RocketMQ console.

## Prerequisites

- You have created a namespace.
- You have created a message producer and consumer based on the SDK provided by TDMQ, and they run properly.

## Directions

### Creating group

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Click the **Group** tab at the top, select a namespace, and click **Create** to enter the **Create Group** page.
3. Enter the group information.
   ![](https://qcloudimg.tencent-cloud.cn/raw/dc78e98d36b3abb703ac4181c3036d28.png)
   - Group Name: enter the group name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Group Remarks: enter the group remarks.
   - Advanced Settings:
     - Enable Consumption: all consumers under the group will be paused if this option is disabled and will be resumed after it is enabled.
     - Enable Broadcast Mode: all consumers declared to be in broadcast mode under the group will be paused if this option is disabled and will be resumed after it is enabled.
4. Click **Submit**.

### Viewing consumer details

1. In the **group** list, click **View Consumer Details** in the **Operation** column to enter the subscription list.
2. After expanding the list, you can see the basic information of the group and the information of the connected client.
   - Consumption Mode: cluster mode or broadcast mode.
     - Cluster Consumption: if the cluster consumption mode is used, any message only needs to be processed by any consumer in the cluster.
     - Broadcast Consumption: if the broadcast consumption mode is used, each message will be pushed to all registered consumers in the cluster to ensure that the message is consumed by each consumer at least once.
   - Client Protocol: currently, only TCP is supported.
   - Message Retention: total number of retained messages.
   - Consumer Type: ACTIVELY or PASSIVELY.  
		![](https://qcloudimg.tencent-cloud.cn/raw/3e5c4720e67673ac1eee8249b7cfe2ea.png)
3. Click **View Details** in the **Operation** column of the client to view consumer details.

### Setting offset

1. In the group list, click **Reset offset** in the **Operation** column of the target group.
2. In the pop-up window, you can choose **the latest offset** or **the specified time point** to set the topic's **consumption offset** (that is, specify from where the consumers under the subscription start to consume messages).
3. Click **Submit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/dafe15859968f9b7c0dbbe4adfb2dda8.png)

### Editing group

1. In the group list, click **Edit** in the **Operation** column of the target group.
2. In the pop-up window, edit the group information.
3. Click **Submit**.

### Deleting group

> !After a group is deleted, consumers identified by the group will immediately stop receiving messages, and all the configurations under it will be cleared and cannot be recovered; therefore, caution should be exercised with this operation.

1. In the group list, click **Delete** in the **Operation** column of the target group.
2. In the pop-up window, click **Submit**.
