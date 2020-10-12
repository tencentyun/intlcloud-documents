## Overview

Cross-region replication enables the automatic, asynchronous replication of **incremental objects** from a source bucket in one COS region to a destination bucket in another region. During replication, COS can also automatically replicate the operations performed on objects in the source bucket, such as PUT or DELETE, on those in the destination bucket. You can choose to enable or disable this feature as needed. For more information, see [Cross-Region Replication Overview](https://intl.cloud.tencent.com/document/product/436/19237).

## Prerequisites

To enable cross-region replication, you need to make sure that the source and destination buckets are in different regions and that both have enabled [versioning](https://intl.cloud.tencent.com/document/product/436/19881).


## Enabling Cross-Region Replication

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and select the bucket for which to configure cross-origin replication.
   ![](https://main.qcloudimg.com/raw/e7262775af485aa2913b855d6064802d.png)
2. Click **Fault and disaster tolerance management** > **Cross Region Replication** on the left sidebar, scroll down to **Cross Region Replication**, and click **Add Rule**.
   ![](https://main.qcloudimg.com/raw/91b3093cb905751c68799fc9755d0ff6.png)
3. To configure a cross-region replication rule, you need to first enable versioning for both the source and destination buckets. After the rule configuration is complete, click **OK**.
	 ![](https://main.qcloudimg.com/raw/6aeab6e744f70b0928b20d485b5bbe6b.png)

The fields requiring configuration are outlined below:

- **Source Region**: The region where your source bucket resides.
- **Applied to**: Indicates which objects will be replicated from the source bucket; the default configuration for this field is **The whole bucket**. If a prefix is specified, only objects with this prefix will be replicated, such as files prefixed with `logs/`.
- **Resource Path**: The path to your source bucket.
- **Destination Bucket**: The bucket in which to store the replicated objects. The destination bucket cannot be in the same region as the source bucket, nor can it be a bucket that is not owned by the current account.
**Destination Storage Class**: Storage class of the replicated objects. The storage class will be the same as that of the source objects by default. You can also choose a different storage class for the replicated objects. The options are either `STANDARD` or `STANDARD_IA`.
- **Sync Delete Marker**: for a versioning-enabled bucket, COS adds a delete marker for a DELETE operation for which no object version ID was specified. If you select this option, the cross-region replication will copy the delete marker to the destination bucket. Regardless of whether the delete marker is copied, the corresponding object will not be deleted from the destination bucket. You can always access a noncurrent version of an object by specifying its version ID. For more information, see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

>
> - Once the rule is created, you can turn it on/off under **State**, or edit it under **Actions**.
> - If you configure the **Applied to** field as **The whole bucket** in your first cross-region replication rule, you will be unable to add any new rules. In this case, you may edit it, or simply delete it and add a new one.
> - If you configure the **Applied to** field as **Specific resources** in your first cross-region replication rule, you can edit it and change this setting to **The whole bucket** if needed.

## Disabling Cross-Region Replication

You can disable cross-region replication using one of the following 2 options:

- **State**: Turn off this button for a rule, and cross-region replication will be disabled temporarily. Copied data will be retained in the destination bucket but no more incremental data will be copied from the source bucket while replication is suspended. To re-enable cross-region replication, simply turn this button back on.
- **Delete**: Delete an existing rule by clicking **Delete** under **Actions**. Copied data will be be retained in the destination bucket but no more incremental data will be copied from the source bucket. To re-enable cross-region replication, you need to add a new rule.
  ![](https://main.qcloudimg.com/raw/f26250880b0f298531e66a49ccea8dc5.png)

>
> - When cross-region replication is disabled, in-progress cross-region replication operations cannot proceed and will be aborted.
> - When cross-region replication is re-enabled for a bucket, it only applies to objects created after that point; objects created while replication was suspended or deleted will remain unaffected.
