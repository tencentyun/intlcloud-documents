## Operation Scenarios
TencentDB for Redis supports instance specification adjustment to enable flexible scaling. You can elastically adjust the specification of your Redis instance based on your actual business needs so as to better optimize resource utilization and costs in real time. This document describes how to modify instance specification in the TencentDB for Redis Console.
>Pay-as-you-go instances cannot be scaled in currently.

## Directions
### Scaling the Standard Edition
>
>- When you scale out the Standard Edition, if the remaining available capacity of the instance is insufficient to meet the scale-out requirements, migration will occur, which will not affect the service access. However, there will be a momentary interruption after the migration is completed, and you are recommended to implement a reconnection mechanism for your business.
>- Because the Standard Edition has a maximum capacity of 384 GB, when the capacity reaches 384 GB, it cannot be expanded any further.
>- To avoid failure in capacity reduction, the capacity after reduction should be at least 1.3 times the amount of existing data. The system will refund automatically after capacity reduction.

1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis).
2. On the instance list page, select the instance you want to scale and click **Configure** > **Expansion**, **Reduction**, **Expand Node**, **Reduce Node**, **Add Replica**, or **Delete Replica**.
3. In the configuration adjustment dialog box that pops up, select the capacity to be adjusted to and click **OK**.
4. Return to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.


### Scaling the Cluster Edition
>
>- After the configuration is adjusted, the instance will be charged at the price of the new specification.
>- To avoid failure in capacity reduction, the capacity after reduction should be at least 1.3 times the amount of existing data. The system will refund automatically after capacity reduction.
>- When shards are added or deleted, the system will automatically balance the slot configuration and migrate data, which may fail in rare cases. It is recommended to perform such operations during off-peak period so as to avoid the impact of migration on business access.

1. On the [instance list](https://console.cloud.tencent.com/redis) page, select the instance you want to scale and click **Add Shard**, **Delete Shard**, **Expand Node**, **Reduce Node**, **Add Replica**, or **Delete Replica** under **Configure** for the corresponding cluster scaling operation.
![](https://main.qcloudimg.com/raw/129b79387c1a469e9b7f9cfcb4e1b1b7.png)
2. In the configuration adjustment dialog box that pops up, select the specification to be adjusted to and click **OK**.
3. Return to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.

