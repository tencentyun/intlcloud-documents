## Overview

COS's object lock feature allows you to set a retention period for your objects to prevent them from being overwritten or deleted for a fixed amount of time and your objects can still be accessed immediately. This document describes how to enable object lock in the COS console.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the bucket list page.
4. Click **Security Management** > **Object Lock** on the left, find the **Object Lock** configuration item, click **Edit**, and toggle the feature on.
5. Enter the retention period in the configuration window and click **Save**.
![](https://main.qcloudimg.com/raw/f932220976adfe110e352bbd04079438.png)
	Retention period: It must be a positive integer and can only be extended but not shortened.
6. In the pop-up window, click **OK**.
After the configuration, you can click **File List** > the desired file > **Details** to view the date (local time) on which the object lock rule will expire.
>?The object lock feature is now only available to customers in the allowlist. To use this feature, [contact us](https://intl.cloud.tencent.com/contact-sales).
