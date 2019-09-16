## Overview
When cross-region replication is enabled, **new objects** in the source bucket can be automatically and asynchronously replicated to the destination bucket in another region. When you manage the objects in the source bucket (such as adding or deleting objects), COS will automatically replicate those operations to the objects in the destination bucket. To enable cross-region replication, you need to make sure that the source and destination buckets are in different regions and both have versioning enabled. You can enable or disable cross-region replication as needed.

## Directions
### Enabling Cross-Region Replication


1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar to enter the bucket list page, and click the source bucket to be configured to enter the bucket details page.
   ![](https://main.qcloudimg.com/raw/8a4ceacd4892f0f9f660a6f6fa9dacd0.png)
2. Click **Basic Configuration** at the top to enter the basic configuration page, scroll down to **Cross-region Replication**, and click **Add Rule** to configure a cross-region replication rule.
![](https://main.qcloudimg.com/raw/13d53d3f81bedf08734a8f2b153665ca.png)
3. To configure a cross-region replication rule, you need to enable versioning for both the source and destination buckets. If it is disabled in the source bucket, please enable it before configuring the rule. After completing the configuration, click **OK**.
![](https://main.qcloudimg.com/raw/c53f807a202baea40bcf9599a669f1da.png)

The options in the cross-region replication rule configuration box are as follows:

- Source Region: the region where your source bucket resides.
- **Applied to**: the objects in the source bucket that need to be replicated. If you leave it blank, all the objects in the source bucket will be replicated by default. If a prefix is specified, only objects with this prefix will be replicated. For example, to replicate objects prefixed with `logs/`, enter `logs/`.
- **Resource Path**: the path to your source bucket.
- **Destination Bucket**: Refers to the bucket to which the objects are replicated. The bucket should be in a different region from the source bucket and should be one under the current account in the selected region.
- **Destination Storage Class**: the storage class of the objects after they are replicated to the destination bucket, which is by default the same as that in the source bucket. You can also change the destination storage class. Currently, Standard and IA storage classes are available.

> !
> - After a rule is configured, you can edit it in **Cross-region Replication** on the basic configuration page of the bucket. For example, you can enable or disable it or modify options such as **Applied to**, **Destination Bucket*, and **Destination Storage Class**.
> - If you set to apply the cross-region replication rule to all the objects in the source bucket during configuration, you will not be able to add any other rules, or edit the rule to apply it only to objects with a particular prefix. To make such changes, you will need to delete the current rule and add a new one.
> - If you set to apply the cross-region replication rule only to objects with a particular prefix during configuration, you will not be able to edit the rule to apply it to all the objects in the bucket. You will need to delete the rule and configure a new one where you can set the scope of application to all the objects in the source bucket.

### Disabling Cross-Region Replication


You can disable cross-region replication by clicking the Disable button or deleting the rule.

- **Click the Disable button**: you can suspend a rule by clicking its Disable button. By doing so, the cross region replication feature will be suspended. The replicated data will be retained in the destination bucket, and new data added to the source bucket will not be replicated.
- **Delete the rule**: after you delete a rule in **Cross-region Replication**, the rule will be invalid. The replicated data will be retained in the destination bucket, and new data added to the source bucket will not be replicated. To enable cross-region replication again, you need to configure a rule again.
![](https://main.qcloudimg.com/raw/0f37a91ab6e5b91f06ecb5d4d047c65d.png)

> !
> - Ongoing cross-region replication will be stopped when cross-region replication is disabled.
> - When cross-region replication is enabled again, it will be only applied to objects added after that.
