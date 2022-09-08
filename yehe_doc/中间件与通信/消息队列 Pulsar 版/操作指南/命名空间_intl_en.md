## Overview

Namespace is a resource management concept in TDMQ for Pulsar. Generally, different business scenarios can be isolated by namespace and configured with dedicated settings, such as message retention period. Topics, subscriptions, and role permissions in different namespaces are isolated from each other.

This document describes how to create multiple namespaces in TDMQ for Pulsar to use the same TDMQ for Pulsar cluster in different scenarios.

>?Topic and subscription names must be unique in the same namespace.

## Directions

>?
>
>- If the TDMQ for Pulsar cluster you create is on v2.6.1, a `default` namespace will be created by default with a default message TTL of 7 days, which can be modified but not deleted.
>- If the TDMQ for Pulsar cluster you create is on v2.7.1 or later, no `default` namespace will be automatically created.

### Creating a namespace

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and enter the **Namespace** page.
2. On the **Namespace** page, select the region and click **Create** to enter the **Create Namespace** page.
3. In the **Create Namespace** window, configure the namespace attributes:
   - Namespace Name: Enter the namespace name, which is required and cannot be modified after creation. The name can contain up to 128 letters, digits, and special symbols (-\_=:.).
   - Message TTL: Set the ACK timeout of an unconsumed message. The message will not be processed if it is not acknowledged within the ACK timeout. Value range: 60 seconds ~ 24 hours.
   - Message Retention Policy
     - Deletion after consumption: Messages will be cleared within a certain period of time after being acknowledged successfully to save the storage space. If there is no subscription to the topic, async clearing will be directly applied to the messages just produced.
     - Persistent retention: No matter whether messages are consumed or not, they will be stored persistently within the maximum retention period and maximum storage space and then deleted chronologically after the limit is reached.
   - Description: Enter the remarks of the namespace.
4. Click **Save**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d2157b367f36b52b76aaf2163a5190b9.png)




<dx-alert infotype="explain" title="Next steps:">
After the above steps, you can create a topic as instructed in [Topic Management](https://intl.cloud.tencent.com/document/product/1110/42930) in the namespace to produce and consume messages.
</dx-alert>



### Modifying a namespace

You can modify a namespace in the following steps:

1. On the [Namespace](https://console.cloud.tencent.com/tdmq/env) list page, click **Edit** in the **Operation** column of the target namespace to enter the editing page.
2. Modify the message retention period or description and click **Save**.

### Deleting a namespace

You can delete a created namespace in the following steps:

1. On the [Namespace](https://console.cloud.tencent.com/tdmq/env) list page, click **Delete** in the **Operation** column of the target namespace.
2. In the deletion confirmation pop-up window, click **OK**.

>!
>- A namespace with topics cannot be deleted.
>- A namespace with permissions configured for roles cannot be deleted.
>- A namespace associated with VPCs cannot be deleted.
