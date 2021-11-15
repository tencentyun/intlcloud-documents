This document describes how to upgrade the node specification and expand shard disk capacity for a TencentDB for Tendis instance in the console.

## Overview
You can elastically scale your TencentDB for Tendis instances as needed to ensure sufficient resources and better resource allocation.
>?Currently, TencentDB for Tendis does not support capacity reduction, and the Storage Edition supports neither capacity expansion nor reduction.

## Directions
1. Log in to the [TencentDB for Tendis console](https://console.cloud.tencent.com/tendis). In the instance list, select a region at the top, locate the instance to be scaled, and click **Configure** > **Expand Node** or **Adjust Disk** in the **Operation** column.
![](https://main.qcloudimg.com/raw/21ebadf2564c20d92a6db3f32eb9a137.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
>?
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- During expansion, such blocking commands as `BLPOP`, `BRPOP`, `BRPOPLPUSH`, and `SUBSCRIBE` may fail once or more. Please assess the impact on your business before starting expansion.
>- Disk capacity expansion has little impact on your business and is usually completed in less than five minutes, but we do not recommend performing this operation during the write request peak.
>
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.


