
## Overview
This document describes how to elastically scale an instance in the TencentDB for Redis console to better optimize resource utilization and costs in real time.


## Directions
### Scaling a memory edition instance in standard architecture
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- To expand the capacity of a memory edition instance in standard architecture, if the remaining available capacity of the physical machine is insufficient, a migration will occur, which will not affect your access to the instance. However, if the instance is running Redis 2.8, a flash disconnection will occur after the migration is completed, so we recommend that your business have a reconnection mechanism.
>- As the maximum capacity of a memory edition instance in standard architecture is 64 GB, you cannot expand its capacity to more than 64 GB.
>- To avoid failure in capacity reduction, the capacity after reduction must be at least 1.3 times the amount of existing data. After the capacity reduction, you will receive an automatic refund.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Expand Node**, **Reduce Node**, **Add Replica**, or **Delete Replica** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/55c978523bfe6d8763aa87259ab13fb8.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.


### Scaling a memory edition instance in cluster architecture
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- To avoid failure in capacity reduction, the capacity after reduction must be at least 1.3 times the amount of existing data. After the capacity reduction, you will receive an automatic refund.
>- When shards are added or deleted, the system will automatically balance the slot configuration and migrate data, which may fail in rare cases. It is recommended to perform such operations during off-peak period so as to avoid the impact of migration on business access.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Shard**, **Delete Shard**, **Expand Node**, **Reduce Node**, **Add Replica**, or **Delete Replica** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/81ffa8bb2eec3eb98d8eb590537a12b1.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.

