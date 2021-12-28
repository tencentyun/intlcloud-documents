## Overview

In TDMQ for RocketMQ, namespace is a resource management concept. Different business scenarios can generally be isolated by namespace and customized with specific parameters, such as message retention period. Topics, subscriptions, and role permissions are kept isolated in different namespaces.

This document describes how to create multiple namespaces in TDMQ for RocketMQ so as to use the same TDMQ for RocketMQ cluster in different scenarios.

>?Topic and group names must be unique in the same namespace.

## Directions

### Creating namespace

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click **View Namespace** in the **Operation** column of the target cluster to enter the namespace page.
2. On the **Namespace** page, click **Create** to enter the **Create Namespace** page.
3. In the **Create Namespace** window, configure the namespace attributes:
	 ![](https://qcloudimg.tencent-cloud.cn/raw/d39f18ded7ffbc7d0a42195d1a13d007.png)
   - Namespace Name: enter the namespace name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Message TTL: set the retention time of unconsumed messages. Messages will be automatically deleted if not acknowledged after expiration. Value range: 60 seconds–15 days.
   - Message Retention Policy:
    - Deletion after consumption: messages will be cleared within a certain period of time after being acknowledged successfully to save the storage space. 
    - Persistent retention: no matter whether messages are consumed or not, they will be stored persistently within the maximum retention period and maximum storage space and then deleted chronologically after the limit is reached.
   - Remarks: enter the remarks of the namespace.
4. Click **Save**.
> ?Up to 10 namespaces can be created in one cluster.

Next steps: you can [create a topic](https://intl.cloud.tencent.com/document/product/1113/43124) in the namespace to produce and consume messages.

### Modifying namespace

You can modify a namespace in the following steps:

1. On the **Namespace** list page, click **Edit** in the **Operation** column of the target namespace to enter the editing page.
2. Modify the message TTL, message retention period, or remarks and click **Save**.

### Deleting namespace

You can delete a created namespace in the following steps:

1. On the **Namespace** list page, click **Delete** in the **Operation** column of the target namespace.
2. In the deletion confirmation pop-up window, click **OK**.

> !A namespace with topics cannot be deleted.
