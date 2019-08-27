## Scenario
TencentDB for Redis supports instance specification adjustment to enable flexible scaling. You can elastically adjust the specification of your Redis instance based on your actual business needs so as to better optimize resource utilization and costs in real time. This document describes how to modify instance specification in the TencentDB for Redis Console.

## Directions
### Scaling in the Standard Edition
>
>- When you expand the capacity of the Standard Edition, if the remaining available capacity of the instance is insufficient to meet the capacity expansion requirements, migration will occur, which will not affect the service access. However, there will be a momentary interruption after the migration is completed, and you are recommended to implement a reconnection mechanism for your business.
>- Because the Standard Edition has a maximum capacity of 384 GB, when the capacity reaches 384 GB, it cannot be expanded any further.
>- The minimum value after capacity reduction should be 1.3 times the capacity used by the instance. After the capacity is reduced, the system will automatically make a refund.

1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis).
1. On the instance list page, select the instance you want to scale and click **Change Configuration** > **Expansion** or **Reduction**.
2. In the configuration adjustment window that pops up, select the capacity to be adjusted to and click **OK**.
3. Return to the instance list. After the status of the instance changes to **Running**, it can be used normally.
![](https://main.qcloudimg.com/raw/1c2f2c7b845a9bf55c4f6b9324d1f632.png)
![](https://main.qcloudimg.com/raw/abbd24d0290471dbac886d1b8f2d667e.png)

### Scaling in the Cluster Edition
>
>- After the configuration is adjusted, the instance will be charged at the price of the new specification.
>- To avoid failure in capacity reduction, the capacity after reduction should be at least 1.3 times the amount of existing data.
>- When shards are added or deleted, the system will automatically balance the slot configuration and migrate data which may fail in rare cases. It is recommended to perform such operations during business valleys so as to avoid the impact of migration on business access.

1. On the instance list page, select the instance you want to scale and click **Add Shard**, **Delete Shard**, **Expand Shard Capacity**, **Reduce Shard Capacity**, **Add Replica**, or **Delete Replica** under **Change Configuration** for the corresponding scaling operation.
2. In the configuration adjustment window that pops up, select the specification to be adjusted to and click **OK**.
3. Return to the instance list. After the status of the instance changes to **Running**, it can be used normally.
