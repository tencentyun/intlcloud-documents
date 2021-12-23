## Overview

A producer sends a message to an exchange, which subsequently routes the message to one or more queues based on its attributes or content (or discards it). Then, a consumer pulls it from one of these queues and consumes it.

This document describes how to create, delete, and query an exchange in the TDMQ for RabbitMQ console.

## Prerequisites

You have created a vhost as instructed in [Creating Vhost](https://intl.cloud.tencent.com/document/product/1112/43073).

## Directions

### Creating exchange

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Click the **Exchange** tab at the top, select a vhost, and click **Create** to enter the **Create Exchange** page.
3. In the **Create Exchange** window, enter the following information:
   ![](https://main.qcloudimg.com/raw/a05cf17275616133497dd8334e39fd05.png)
   - Exchange Name: enter the exchange name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Route Type: select a route type (direct, fanout, or topic), which cannot be changed after creation. For more information on route types, see [Exchange](https://intl.cloud.tencent.com/document/product/1112/43074).
     - Direct: a direct exchange will route messages to the queue whose binding key exactly matches the routing key.
     - Fanout: a fanout exchange will route messages to all queues bound to it.
     - Topic: a topic exchange supports multi-condition match and fuzzy match; that is, it will route messages to the queues bound to it by using routing key pattern match and string comparison.
   - Exchange Remarks: enter the exchange remarks of up to 128 characters.
4. Click **Submit**, and you can see the created exchange in the exchange list.

### Editing exchange

1. In the exchange list, click **Edit** in the **Operation** column of the target exchange.
2. In the pop-up window, you can edit the exchange remarks.
3. Click **Submit**.

### Deleting exchange

> !After an exchange is deleted, all the configurations under it will be cleared and cannot be recovered.

1. In the exchange list, click **Delete** in the **Operation** column of the target exchange.
2. In the pop-up window, click **Delete**.
