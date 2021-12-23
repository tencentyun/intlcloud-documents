## Overview

A queue is used to store messages. Each message will be put into one or more queues. Producers produce messages and deliver them to queues, and consumers pull messages from queues for consumption.

Multiple consumers can subscribe to the same queue. In this case, messages in the queue will be evenly distributed to such consumers for processing, rather than making each consumer receive and process all the messages.

This document describes how to create, delete, and query a queue in the TDMQ for RabbitMQ console.

## Prerequisites

You have created a vhost.

## Directions

### Creating queue

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Click the **Queue** tab at the top, select a vhost, and click **Create** to enter the **Create Queue** page.
3. Enter the queue information.
  ![](https://qcloudimg.tencent-cloud.cn/raw/79a277e65f947a9b2e8c29702bd66a15.png)
   - Queue Name: enter the queue name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Auto-Clear: after this feature is enabled, the queue will be deleted immediately after its last consumer unsubscribes from it.
   - Queue Remarks: enter the queue remarks of up to 128 characters.
4. Click **Submit**.

### Viewing queue details

In the **queue** list, click the right triangle on the left of the target queue to view its details.

You can view:

- Basic information (message retention, automatic deletion, creation time, and online consumers)
- Consumer list: information of consumers subscribed to this queue

![](https://qcloudimg.tencent-cloud.cn/raw/21c4b69fddfe139c03f86f00c5daf38a.png)

### Viewing binding

In the queue list, click **View Binding** in the **Operation** column of the target queue to view its bindings.

### Editing queue

1. In the queue list, click **Edit** in the **Operation** column of the target queue.
2. In the pop-up window, edit the queue information.
3. Click **Submit**.

### Deleting queue

> !After a queue is deleted, all the configurations under it will be cleared and cannot be recovered.

1. In the queue list, click **Delete** in the **Operation** column of the target queue.
2. In the pop-up window, click **Delete**.
