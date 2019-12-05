## Overview
You can log in to the COS Console to enable log management for a bucket, which records various requests related to **bucket operations**. Log management facilitates  buckets usage and management. For more information on log management, see [Log Management Overview](https://intl.cloud.tencent.com/document/product/436/16920).

>- The log management feature is currently only available in four regions including Beijing, Shanghai, Guangzhou, Chengdu and Toronto.
>- Currently, only the **bucket owner** has permission to set log management, and the **Log Management** configuration item will not be displayed to other users when they log in to the console. 
>- The log data is delivered every 5 minutes. COS does not guarantee 100% accuracy of the log data. It is for reference only and is not used as a basis for measurement and billing.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the source bucket that needs the log management enablement.
![](https://main.qcloudimg.com/raw/2cb54182f933fe1dce75e2199a301bd0.png)
2. Click **Advanced Configuration** on the left, find the **Log Management** configuration item, and click **Edit** to enter the editable state.
![](https://main.qcloudimg.com/raw/242facfd32074aea52a7f694273a9086.png)
3. Click Enable to the right of **Status** and click **Save**.
![](https://main.qcloudimg.com/raw/4f3a62cbc636be16254547a271204096.png)
4. Confirm that the feature is enabled. Select the destination bucket (i.e., the bucket that stores the logs), and set the key prefix for the log object (e.g., `log/`). After confirming that the entered information is correct, click **Save**. The configuration items are as described below:
 - **Destination Bucket**: the **source bucket ** for which log management is enabled and the **destination bucket ** that stores the logs must be in the same region. It is not recommended to use the source bucket itself as the destination bucket.
 - **Target prefix**: enter a custom path prefix that makes it easy for you to find the logs.
![](https://main.qcloudimg.com/raw/d5fa347da09d92b5f757e32c910739e3.png)

## Notes
1. To enable the log management feature, you need to create a log role in the CAM Console and grant it read/write permission to the logs of the source bucket.
2. When the log management feature is disabled, if the role is not deleted, its read/write permission to the logs of the source bucket will not be revoked.
