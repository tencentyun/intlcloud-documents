## Overview

Namespace is a resource management concept in TDMQ for Pulsar. Generally, different business scenarios can be isolated by namespace and configured with dedicated settings, such as message retention period. Topics, subscriptions, and role permissions in different namespaces are isolated from each other.

This document describes how to create multiple namespaces in TDMQ for Pulsar so as to use the same TDMQ for Pulsar cluster in different scenarios.

>?Topic and subscription names must be unique in the same namespace.

## Directions

>?
>- If the TDMQ for Pulsar cluster you create is on v2.6.1, a `default` namespace will be created by default with a default message TTL of 7 days, which can be modified but cannot be deleted.
>- If the TDMQ for Pulsar cluster you create is on v2.7.1 or above, no `default` namespace will be automatically created.

### Creating namespace

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and enter the **Namespace** page.
2. On the **Namespace** page, select the region and click **Create** to enter the **Create Namespace** page.
3. In the **Create Namespace** window, configure the namespace attributes:
 - Namespace Name: enter the namespace name, which cannot be modified after creation and can contain only letters, digits, hyphens, and underscores.
 - Message TTL: set the TTL for unconsumed messages. If a message is unacknowledged after this period, it will be skipped. Value range: 60s–15 days.
 - Message Retention Policy
	- Deletion after consumption: messages will be cleared within a certain period of time after being acknowledged successfully to save the storage space.
	- Persistent retention: no matter whether messages are consumed or not, they will be stored persistently within the maximum retention period and maximum storage space and then deleted chronologically after the limit is reached.
 - Remarks: enter the remarks of the namespace.
4. Click **Save**.<br>
 <img src="https://main.qcloudimg.com/raw/1833e5b8b5f3328d778dce5723eb99c7.png" width="500">


Next steps: you can [create a topic](https://intl.cloud.tencent.com/document/product/1110/42930) in the namespace to produce and consume messages.

### Modifying namespace

You can modify a namespace in the following steps:

1. On the [Namespace](https://console.cloud.tencent.com/tdmq/env) list page, click **Edit** in the **Operation** column of the target namespace to enter the editing page.
2. Modify the message retention period or remarks and click **Save**.

### Deleting namespace

You can delete a created namespace in the following steps:

1. On the [Namespace](https://console.cloud.tencent.com/tdmq/env) list page, click **Delete** in the **Operation** column of the target namespace.
2. In the deletion confirmation pop-up window, click **OK**.

>!A namespace with topics cannot be deleted.
