## Overview

You can use the lifecycle management feature when you need to change the storage class or delete specified objects regularly to reduce costs. COS will automatically change the storage class or delete specified objects within the specified time frame according to the rules you set. For more information, see [Lifecycle Overview](https://intl.cloud.tencent.com/document/product/436/17028).

>? A lifecycle can be set to as long as 3,650 days.
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket for which you want to enable the lifecycle feature. Click the bucket name to enter its details page.
4. Click **Basic Configurations** > **Lifecycle** and click **Add a Rule**.

5. Add lifecycle rules as needed. The configuration items are described as follows:
 - **Rule name**: name of the lifecycle rule
 - **Apply to**: range of the lifecycle rule. The rule can apply to the whole bucket or a specified range. The range is described as follows:
    - Prefix: The lifecycle rule applies to objects with a specified prefix (e.g., prefix/).
    - Object Tag: The lifecycle rule applies to objects with a specified tag. You can set multiple tags (case-sensitive).
>!The object prefix and object tag can be specified at the same time. The relationships between object prefix and object tag and between object tags are "AND".
>
 - **Managing the current version**: transitions or deletes the current object version. Objects in your bucket can be transitioned from STANDARD to STANDARD_IA, ARCHIVE, or DEEP ARCHIVE, or deleted upon expiration.
   COS storage classes include **STANDARD**, **STANDARD_IA**, **INTELLIGENT TIERING**, **ARCHIVE**, and **DEEP ARCHIVE** (from hot storage to cold storage). You can transition objects only from a hot storage class to a colder one, not vice versa. The number of days is measured according to the time an object is modified, that is, if you modify an object, the days will be remeasured as if you uploaded the object again.
>? For buckets with multi-AZ configuration enabled, the lifecycle transition order can only be **MAZ_STANDARD** > **MAZ_STANDARD_IA** > **INTELLIGENT TIERING (MAZ)**.
>
 - **Managing historical versions**: you can transition or delete previous versions of an object using this option. If it is not enabled, only the latest version of an object is processed by default.
 - **Remove Delete Markers from objects with no noncurrent versions**: If the latest version of an object is a delete marker and all of its noncurrent versions have been deleted, the delete marker will also be deleted if you enable this option. Note that you cannot enable this option if you have selected the delete upon expiration option under **Managing the current version**.
 - **Deleting incomplete multipart uploads**: allows you to delete expired incomplete multipart uploads that have failed due to any reason.


6. Click **OK**.

7. To disable a lifecycle rule, click **Edit** and change the rule status to **Off**, or simply delete the rule.
8. To delete all lifecycle rules in the bucket, click **Clear all rules**.



