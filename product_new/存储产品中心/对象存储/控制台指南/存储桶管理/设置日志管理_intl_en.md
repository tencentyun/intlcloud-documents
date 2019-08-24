## Overview
You can log in to the COS Console to enable log management for a bucket, which records various requests related to **bucket operations**. Log management facilitates  buckets usage and management. For more information, see [Log Management Overview](https://cloud.tencent.com/document/product/436/16920).

>!
> - The log management feature is currently only available in four regions including Beijing, Shanghai, Guangzhou, and Chengdu.
>- Currently, only the **bucket owner** has permission to set log management, and the **Log Management** configuration item will not be displayed to other users when they log in to the console. 

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the source bucket that needs the log management enablement.
![](https://main.qcloudimg.com/raw/8a4ceacd4892f0f9f660a6f6fa9dacd0.png)
2. Click **Basic Configuration** on the bucket details page, find the **Log Management** configuration item, and click **Edit** to enter the editable state.
![](https://main.qcloudimg.com/raw/f1452ed875265093ce0c611c02055ecc.png)
3. Click Enable to the right of **Status** and click **Save**.
![](https://main.qcloudimg.com/raw/de951a4accb0b0a5880a3dd995c1cb22.png)
4. Confirm that the feature is enabled. Select the destination bucket (i.e., the bucket that stores the logs), and set the key prefix for the log object (e.g., `log/`). After confirming that the entered information is correct, click **Save**. The configuration items are as described below:
 - **Destination Bucket**: the **source bucket ** for which log management is enabled and the **destination bucket ** that stores the logs must be in the same region. It is not recommended to use the source bucket itself as the destination bucket.
 - **Path Prefix**: enter a custom path prefix that makes it easy for you to find the logs.
![](https://main.qcloudimg.com/raw/1554b91a9737ec73e6e06246e00686b5.png)

## Notes
1. To enable the log management feature, you need to create a log role in the CAM Console and grant it read/write permission to the logs of the source bucket.
2. When the log management feature is disabled, if the role is not deleted, its read/write permission to the logs of the source bucket will not be revoked.
