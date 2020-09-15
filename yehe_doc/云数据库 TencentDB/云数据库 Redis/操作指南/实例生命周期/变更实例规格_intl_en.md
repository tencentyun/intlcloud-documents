## Operation Scenarios
TencentDB for Redis supports instance specification adjustment to enable flexible scaling. You can elastically adjust the specification of your Redis instance based on your actual business needs so as to better optimize resource utilization and costs in real time. This document describes how to modify instance specification in the TencentDB for Redis Console.
>?Pay-as-you-go instances cannot be scaled in currently.

## Directions
### Scaling the memory edition (standard architecture)
>!
>- When you expand the capacity of the memory edition (standard architecture), if the remaining available capacity of the instance is insufficient to meet the capacity expansion requirements, migration will occur, which will not affect the service access. However, there will be a momentary interruption after the migration is completed, and we recommend that you implement a reconnection mechanism for your business.
>- Because the memory edition (standard architecture) has a maximum capacity of 384 GB, when the capacity reaches 384 GB, it cannot be expanded any further.
>- To avoid failure in capacity reduction, the capacity after reduction should be at least 1.3 times the amount of existing data. The system will refund automatically after capacity reduction.

1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis). In the instance list, locate the instance you want to scale and click **Configure** > **Expand Node**, **Reduce Node**, **Add Replica**, or **Delete Replica** in the "Operation" column.
![](https://main.qcloudimg.com/raw/9b8e7bf10a2848977ee274a3425cfb14.png)
2. On the instance list page, select the instance you want to scale and click **Configure** > **Expansion**, **Reduction**, **Expand Node**, **Reduce Node**, **Add Replica**, or **Delete Replica**.
3. In the configuration adjustment dialog box that pops up, select the capacity to be adjusted to and click **OK**.
4. Return to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.


### Scaling the memory edition (cluster architecture)
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new specification.
>- To avoid failure in capacity reduction, the capacity after reduction should be at least 1.3 times the amount of existing data. The system will refund automatically after capacity reduction.
>- When shards are added or deleted, the system will automatically balance the slot configuration and migrate data, which may fail in rare cases. It is recommended to perform such operations during off-peak period so as to avoid the impact of migration on business access.

1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis). In the instance list, locate the instance you want to scale and click **Configure** > **Add Shard**, **Delete Shard**, **Expand Node**, **Reduce Node**, **Add Replica**, or **Delete Replica** in the "Operation" column.
![](https://main.qcloudimg.com/raw/129b79387c1a469e9b7f9cfcb4e1b1b7.png)
2. In the configuration adjustment dialog box that pops up, select the specification to be adjusted to and click **OK**.
3. Return to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.

