## Overview
When cross-region replication is enabled, **new objects** add to the source bucket can be automatically and asynchronously copied to the destination bucket in another region. When you manage the objects in the source bucket (such as adding or deleting objects), COS will automatically replicate those operations to the destination bucket. To enable cross-region replication, the source bucket and the destination bucket should be in different regions and both have versioning enabled. You can choose to enable or disable cross-region replication as needed.

## Directions
### Enabling Cross-Region Replication


1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar to enter the bucket list page, and click the source bucket to be configured to enter the bucket details page.
   ![](https://main.qcloudimg.com/raw/e7262775af485aa2913b855d6064802d.png)
2. Click **Basic Configuration** at the top to enter the basic configuration page, scroll down to **Cross-region Replication**, and click **Add Rule** to configure the cross-region replication rule.
![](https://main.qcloudimg.com/raw/91b3093cb905751c68799fc9755d0ff6.png)
3. To configure a cross-region replication rule, versioning must be enabled in both the source and destination buckets. If it is disabled in the source bucket, please enable it before configuring the rule. After completing the configuration, click **OK**.
![](https://main.qcloudimg.com/raw/6aeab6e744f70b0928b20d485b5bbe6b.png)

The options in the cross-region replication rule configuration box are as follows:

- Source Region: The region where your source bucket resides.
- Scope of Application: The scope of objects in the source bucket that need to be copied. If this is not set, all the objects in the source bucket will be copied by default. If a prefix is specified, only objects with this prefix will be copied. For example, to copy objects prefixed with `logs/`, enter `logs/`.
- Resource Path: Path to your source bucket.
- Destination Bucket: The bucket to which the objects are copied. Its region must be different from that of the source bucket, and it should be a bucket under the current account in the selected region.
- Destination Storage Class: The storage class of the objects after they are copied to the destination bucket, which is the same as that in the source bucket by default. You can also change the destination storage class. Currently, Standard and Standard_IA storage classes are available.

> - After a rule is configured, you can edit it in **Cross-region Replication** on the basic configuration page of the bucket. For example, you can enable or disable it or modify options such as scope of application, destination bucket, and destination storage class.
> - If you set the scope of application to all the objects in the source bucket when configuring the cross-region replication rule for the first time, you cannot add any other rules later or modify the scope of application in the rule to objects with a particular prefix; however, you can make such changes by deleting the current rule and configure a new one.
> - If you set the scope of application to objects with a particular prefix when configuring the cross-region replication rule for the first time, you cannot modify the scope of application to all the objects in the bucket; however, you can delete the rule and configure a new one where you can set the scope of application to all the objects in the source bucket.

### Disabling Cross-Region Replication


You can disable cross-region replication by clicking the Disable button or deleting the rule.

- **Click the Disable button**: You can temporarily disable a rule by clicking its Disable button. By doing so, the cross-region replication feature will be suspended; the copied data will be stored in the destination bucket; and new data added to the source bucket will not be replicated.
- **Delete the rule**: After deleting a rule in **Cross-region Replication**, the corresponding cross-region replication configuration will be invalid. The copied data will be stored in the destination bucket, and new data added to the source bucket will not be replicated. To enable cross-region replication again, you need to configure a rule again.
![](https://main.qcloudimg.com/raw/f26250880b0f298531e66a49ccea8dc5.png)

> - Uncompleted cross-region replication operations will be stopped when cross-region replication is disabled.
> - When cross-region replication is enabled again, it will be performed only on newly added objects after that.

