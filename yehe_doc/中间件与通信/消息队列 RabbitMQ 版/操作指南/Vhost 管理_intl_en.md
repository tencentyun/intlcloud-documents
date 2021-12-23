## Overview

Virtual host (vhost) is a resource management concept in TDMQ for RabbitMQ. It is used for logical isolation. Exchanges and queues of different vhosts are isolated from each other.

Generally, different business scenarios can be isolated by vhost and configured with dedicated settings, such as message retention period.

This document describes how to create multiple vhosts in TDMQ for RabbitMQ so as to use the same TDMQ for RabbitMQ cluster in different scenarios.

> ?Exchange and queue names must be unique in the same vhost.

## Prerequisites

You have [created a cluster](https://intl.cloud.tencent.com/document/product/1112/43072).

## Directions

### Creating vhost

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Select the **Vhost** tab at the top and click **Create** to enter the **Create Vhost** page.
3. In the **Create Vhost** window, configure the vhost attributes:
   ![](https://main.qcloudimg.com/raw/c87ba46c5d7e458f392c41579964be9a.png)
   - Vhost Name: enter the vhost name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Message TTL: set the retention time of unconsumed messages. Messages will be automatically deleted if not acknowledged after expiration. Value range: 60 seconds–15 days.
   - Remarks: enter the vhost remarks.
4. Click **Submit**.

Next steps: you can [create an exchange](https://intl.cloud.tencent.com/document/product/1112/43074) and [queue](https://intl.cloud.tencent.com/document/product/1112/43075) in the vhost to produce and consume messages.

### Configuring permissions

**Prerequisite**: you have [created a role](https://console.cloud.tencent.com/tdmq/role).

1. On the **Vhost** list page, click **Configure Permissions** in the **Operation** column of the target vhost.
2. On the **Configure Permissions** page, click **Create** to add production and consumption permissions to the vhost you just created.
<img src="https://main.qcloudimg.com/raw/515644356c3ec5d005f61ea19fa6e807.png" width="536">

 



### Modifying vhost

You can modify a vhost in the following steps:

1. On the **Vhost** list page, click **Edit** in the **Operation** column of the target vhost to enter the editing page.
2. Modify the message TTL or remarks and click **Save**.

### Deleting vhost

You can delete a created vhost in the following steps:

1. On the **Vhost** list page, click **Delete** in the **Operation** column.
2. In the deletion confirmation pop-up window, click **OK**.

> !After a vhost is deleted, all the configurations under it will be cleared and cannot be recovered.
