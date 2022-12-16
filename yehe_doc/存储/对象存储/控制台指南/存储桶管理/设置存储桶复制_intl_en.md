## Overview

Cross-bucket replication enables the automatic, asynchronous replication of **incremental objects** from a source bucket to a destination bucket. During replication, COS may also automatically replicate the object operations in the source bucket, such as PUT Object or DELETE Object. You can choose to enable or disable this feature as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/19237).

## Prerequisites

Before enabling cross-bucket replication, make sure that both the source and destination buckets have enabled [versioning](https://intl.cloud.tencent.com/document/product/436/19881).

## Directions

### Enabling cross-bucket replication

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Click the name of the source bucket that you want to set cross-bucket replication for.
4. Click **Fault Tolerance and Disaster Recovery** > **Cross-Bucket Replication** on the left.
5. In the **Cross-Bucket Replication** column, click **Add Rule**.
![](https://main.qcloudimg.com/raw/910b0ddbe6f3bb0093544b5c21a07ca0.png)
6. In the pop-up window, configure the cross-bucket replication rule and click **OK**.
>? If versioning is not enabled for both the source and destination buckets, enable it first and then configure the cross-bucket replication rule.
>
![](https://main.qcloudimg.com/raw/2a167db6422d4de507d3851d9965ab37.png)
The configuration items are described as follows:
<table>
	<tr><th style="width: 18%">Configuration Item</th><th>Description</th></tr>
	<tr><td>Source Region</td><td>The region where your source bucket resides.</td></tr>
	<tr><td>Apply To</td><td>Indicates which objects will be replicated from the source bucket. The default option is **The whole bucket**. If a prefix is specified, only objects with this prefix will be replicated, such as files prefixed with `logs/`.</td></tr>
	<tr><td>Resource Path</td><td>Path of your source bucket.</td></tr>
	<tr><td>Destination Bucket</td><td>The bucket to store the replicated objects. It can be in the same region as the source bucket. You can select only one bucket under the current account in each region.</td></tr>
	<tr><td>Destination Storage Class</td><td>Storage class of the replicas. The storage class will be the same as that of the source objects by default. You can also select a different storage class.</td></tr>
	<tr><td>Sync Delete Marker</td><td>If you try to delete an object from a versioning-enabled bucket without specifying a version ID, COS will add a delete marker to the object. If you select this option, cross-bucket replication will copy this delete marker to the destination bucket. Regardless of whether the delete marker is copied, the object will not be deleted from the destination bucket. You can always access a noncurrent version of the object by specifying its version ID. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/19883">Overview</a>.</td></tr>
</table>


>!
> - Once the rule is created, you can enable/disable it under **Status**, or edit it under **Operation**.
> - If you set **Applied to** to **The whole bucket** in your first rule, you will be unable to add any new rules. In this case, you may choose to edit it, or simply delete it and add a new one.
> - If you set **Applied to** to **Specific resources** in your first rule, you can edit it and change this setting to **The whole bucket** if needed.
> 

### Disabling cross-bucket replication

You can disable a cross-bucket replication rule using either of the following two options:

- **Status**: Switch this button off, and cross-bucket replication will be disabled temporarily. Copied data will be retained in the destination bucket but no more incremental data will be copied from the source bucket as long as replication is suspended. To re-enable cross-bucket replication, switch this button back on.
- **Delete Rule**: Delete an existing rule by clicking **Delete** under **Operation**. Copied data will be retained in the destination bucket but no more incremental data will be copied from the source bucket. To re-enable cross-bucket replication, you need to add a new rule.
![](https://main.qcloudimg.com/raw/f26250880b0f298531e66a49ccea8dc5.png)

>!
> - When cross-bucket replication is disabled, in-progress cross-bucket replication operations cannot proceed and will be aborted.
> - When cross-bucket replication is re-enabled for a bucket, it only applies to objects created after that time point.
> 

