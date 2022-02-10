This document describes how to upgrade the node specification and expand shard disk capacity for a TencentDB for Tendis instance in the console.

## Overview
You can elastically scale your TencentDB for Tendis instances as needed to ensure sufficient resources and better resource allocation.
>?Currently, TencentDB for Tendis does not support capacity reduction, and the Storage Edition supports neither capacity expansion nor reduction.

## Directions
1. Log in to the [TencentDB for Tendis console](https://console.cloud.tencent.com/tendis). In the instance list, select a region at the top, locate the instance to be scaled, and click **Configure** > **Expand Cache** or **Expand Disk** in the **Operation** column.
![](https://main.qcloudimg.com/raw/21ebadf2564c20d92a6db3f32eb9a137.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
>?
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- To avoid failure in capacity reduction, the capacity after reduction should be at least 1.3 times the amount of existing data.
>- When shards are added or deleted, the system will automatically balance the slot configuration and migrate data.
>- During capacity expansion and reduction, such blocking commands as `BLPOP`, `BRPOP`, `BRPOPLPUSH`, and `SUBSCRIBE` may fail once or more (which is related to the number of shards). Please assess the impact on your business before starting capacity expansion and reduction.
>- During capacity expansion and reduction, commands executed on an instance with read-only replicas enabled may fail once or more (which is related to the number of shards). Please assess the impact on your business before starting capacity expansion and reduction.
3. Return to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.


