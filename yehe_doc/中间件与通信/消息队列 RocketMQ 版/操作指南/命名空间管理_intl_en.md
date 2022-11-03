## Overview

In TDMQ for RocketMQ, namespace is a resource management concept. It can generally be used to isolate different businesses via customized configurations such as message retention period. Topics, subscriptions, and role permissions in one namespace are all kept separate from those in another.

This document describes how to create multiple namespaces in TDMQ for RocketMQ to use the same TDMQ for RocketMQ cluster in different scenarios.

>?Topic and group names must be unique in the same namespace.

## Directions

### Creating a namespace

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Select the **Namespace** tab at the top of the page and click **Create** to enter the namespace creation page.
3. In the **Create Namespace** dialog box, configure the namespace attributes:
![](https://qcloudimg.tencent-cloud.cn/raw/d39f18ded7ffbc7d0a42195d1a13d007.png)
 - Namespace Name: Enter the namespace name, which cannot be modified after creation and can contain 3–32 letters, digits, backslashes, and underscores.
 - Message Retention Period: Set the retention period (0 seconds to 3 days) of unconsumed messages. After a message is successfully produced, it will be stored for a period of time no matter whether it is consumed or not. It will be automatically deleted upon expiration.
 - Namespace Description: Enter the namespace descriptions.
4. Click **Save**.
> ?Up to 10 namespaces can be created in one cluster.

After the above steps, you can create a topic in the namespace to produce and consume messages as instructed in [Topic Management](https://intl.cloud.tencent.com/document/product/1113/43124).



### Getting access address

On the **Namespace** list page, you can get the namespace access addresses in the **VPC Access Address** and **Public Network Access Address** columns.

### Modifying a namespace

You can modify a namespace in the following steps:

1. On the **Namespace** list page, click **Edit** in the **Operation** column of the target namespace to enter the editing page.
2. Modify the message TTL, message retention period, or namespace description and click **Save**.

### Deleting a namespace

You can delete a created namespace in the following steps:

1. On the **Namespace** list page, click **Delete** in the **Operation** column of the target namespace.
2. In the deletion confirmation pop-up window, click **OK**.

> !A namespace with topics cannot be deleted.
