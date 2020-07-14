## Overview

Cross-region replication enables automatic, asynchronous replication of **incremental objects** from a source bucket in one COS region to a destination bucket in another region. During the replication, COS also automatically copies your operations on the objects in the source bucket, such as PUT or DELETE an object. You can choose to enable or disable this feature as needed. For more information, see [Cross-Region Replication Overview](https://intl.cloud.tencent.com/document/product/436/19237).

## Prerequisites

To enable cross-region replication, you need to make sure that the source and destination buckets are in different regions and both have [versioning enabled](https://intl.cloud.tencent.com/document/product/436/19881).


## Enabling Cross-Region Replication

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List**, and select the bucket for which to configure cross-origin replication.
   ![](https://main.qcloudimg.com/raw/e7262775af485aa2913b855d6064802d.png)
2. Click **Advanced Configuration** on the left sidebar to open the configuration page, scroll down to **Cross Region Replication**, and click **Add Rule**.
   ![](https://main.qcloudimg.com/raw/91b3093cb905751c68799fc9755d0ff6.png)
3. To configure a cross-region replication rule, you need to first enable versioning for both the source and destination buckets. After the rule configuration, click **OK**.
	 ![](https://main.qcloudimg.com/raw/6aeab6e744f70b0928b20d485b5bbe6b.png)

The fields are described as follows:

- **Source Region**: the region where your source bucket resides.
- **Applied to**: indicates which objects will be replicated from the source bucket; defaults to **The whole bucket**. If a prefix is specified, only objects with this prefix are replicated, for example, files prefixed with `logs/`.
- **Resource Path**: the path to your source bucket.
- **Destination Bucket**: the bucket that stores the replicated objects. It cannot be in the same region as the source bucket, nor be a bucket not owned by the current account.
- **Destination Storage Class**: storage class of the object for the replication. It is the same as that of the source object by default. You may choose to replicate it into another storage class, i.e. `STANDARD` or `STANDARD_IA`.
- **Sync Delete Marker**: for a versioned bucket, COS adds a delete marker for a DELETE operation with no object version ID specified. If you select this option, the cross-region replication will copy the delete marker to the destination bucket. Whether the delete marker is copied or not, the object is not deleted from the destination bucket. You can always access a noncurrent version of the object by specifying its version ID. For more information, see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

>
> - Once the rule is created, you can turn it on/off under **State**, or edit it under **Actions**.
> - If you configure **Applied to** to **The whole bucket** in your first cross-region replication rule, you will be unable to add any new rules. In this case, you may edit it, or simply delete it and add a new one.
> - If you configure **Applied to** to **Specific resources** in your first cross-region replication rule, you will be able to edit it and change this setting to **The whole bucket**.

## Disabling Cross-Region Replication

You can disable cross-region replication using one of the following 2 options:

- **State**: toggle off this button for a rule, and cross-region replication will be disabled temporarily. Copied data then will be retained in the destination bucket while no more incremental data is copied from the source bucket. To enable the cross-region replication again, simply toggle this button on.
- **Delete**: delete an existing rule by clicking **Delete** under **Actions**. Copied data will then be retained in the destination bucket while no more incremental data is copied from the source bucket. To enable the cross-region replication again, add a new rule.
  ![](https://main.qcloudimg.com/raw/f26250880b0f298531e66a49ccea8dc5.png)

>
> - When cross-region replication is disabled, in-progress cross-region replication operations will be aborted and cannot proceed.
> - After cross-region replication is enabled again for a bucket, it applies to only newly created objects after that time point.