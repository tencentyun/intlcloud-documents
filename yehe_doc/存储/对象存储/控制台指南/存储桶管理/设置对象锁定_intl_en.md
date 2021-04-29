## Overview

COS’s Object Lock allows you to set a retention period for your objects to prevent them from being overwritten or deleted for a fixed amount of time and your objects can still be assessed immediately. This document describes how to enable Object Lock via the COS console.


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List** in the left sidebar, and click the bucket for which you want to enable Object Lock.
2. Click **Security Management** > **Object Lock**, find the **Object Lock** configuration item, and click **Edit** to enable it.
3. Set the retention period and click **Save**. Then, on the page that is displayed, click **Confirm**.
 - Retention period: It must be a positive integer and can only be extended but not shortened.
![](https://main.qcloudimg.com/raw/ce97b907b05577d7803ba6e5a1822957.png)
4. After the configuration, you can click **File List** > the desired file > **Details** to view the date (Beijing Time) on which the Object Lock rule will expire.

 
