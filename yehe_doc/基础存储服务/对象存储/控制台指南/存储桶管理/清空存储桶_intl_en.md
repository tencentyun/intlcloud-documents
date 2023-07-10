## Overview

You can clear the specified bucket in the COS console. For more information on buckets, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).

>! Clearing a bucket will delete all objects and incomplete multipart uploads in this bucket. The deleted data is unrecoverable and inaccessible. Proceed with caution.
>

## Use Cases

- Clearing a bucket through a [lifecycle rule](https://intl.cloud.tencent.com/document/product/436/17028): This method is applicable to a bucket with more than 10,000 objects. A deletion job will be triggered when the trigger condition of a lifecycle rule is met. The job start and completion time are subject to the lifecycle rule configuration in the console.
- Quickly clearing a bucket in the console: This method is applicable to a bucket with less than 10,000 objects. A bucket clearing job will take effect immediately upon completion.


>? If you have a large amount of data in your bucket, clearing the bucket using the console may be slow or even fail due to network reasons. In this case, we recommend you clear the bucket by setting lifecycle configuration.
>


## Directions


### Quickly clearing a bucket in the console

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Find the target bucket and click **More > Clear Data** on the right.

4. In the pop-up window, enter the name of the bucket you want to clear and click **Confirm**.

5. In the pop-up window, click **OK**.



### Clearing a bucket through a lifecycle rule


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket for which you want to set the lifecycle feature. Click the bucket name to enter its details page.
4. Click **Basic Configurations** > **Lifecycle** and click **Add a Rule**.

5. In the **Add a Rule** pop-up window, set to delete all current and historical versions of files in the entire bucket.
 - Rule name: Enter the name of the lifecycle rule, which is required.
 - Applied to: Select **The whole bucket**.
 - Managing the current version: Set to delete files one day after modification.
 - Managing historical versions: Set to delete files one day after modification.

As bucket data deletion is a high-risk operation, you need to click **OK** to confirm the operation.

6. You can see that the deletion rule has been set successfully in the lifecycle rule list.

7. After the lifecycle rule is executed, you can see that both the number and volume of stored objects are zero on the bucket overview page, indicating that the bucket has been cleared. If you no longer use the bucket, you can delete it.

