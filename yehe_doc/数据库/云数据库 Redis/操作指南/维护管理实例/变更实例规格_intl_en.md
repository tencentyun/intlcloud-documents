
## Overview
This document describes how to elastically scale an instance in the TencentDB for Redis console to better optimize resource utilization and costs in real time.

For instance specifications adjustment, an instance can be scaled quickly in the console without having to stop the services. No operations are required at your side. 

- Expand or reduce nodes: This refers to adjusting the memory capacity of instance nodes to meet ever-changing memory needs and avoid lags caused by insufficient memory.
- Add or delete replicas: This refers to adjusting the number of instance replicas. Replicas are nodes other than the master node. All replicas of the Standard Edition play a role in supporting the system's high availability, so the more the replicas, the higher the availability. If the number of replicas is greater than or equal to 1, read/write separation can be enabled to extend the read performance through replica nodes.
- Add or delete shards: This refers to assigning different keys to multiple shard nodes in the sharding mode of instances in cluster architecture to adjust the number of shard nodes, so that the system performance can be horizontally scaled.

## Version Requirement

- Currently, Redis 4.0 and 5.0 Standard Edition instances support expanding and reducing nodes as well as adding and deleting replicas.
- Currently, Redis 4.0 and 5.0 Cluster Edition instances support expanding and reducing nodes as well as adding and deleting replicas and shards.
- Currently, Redis 2.8 Standard Edition instances only support expanding and reducing nodes.
- Multi-AZ deployed instances don't support reducing replicas. For more information on adding replicas, see [Adding Replicas to Multi-AZ Deployed Instance](https://intl.cloud.tencent.com/document/product/239/46556).

## Billing
### Pay-as-You-Go

The instance will be billed hourly based on the new specification on the next hour under tier 1, and fees will be settled on each hour. The pay-as-you-go billing mode adopts tiered pricing in three tiers as detailed in [Billing Overview](https://intl.cloud.tencent.com/document/product/239/31954). For tiered prices, see [Pricing](https://intl.cloud.tencent.com/document/product/239/9894).

## Prerequisites

- You have created a [TencentDB for Redis instance](https://intl.cloud.tencent.com/document/product/239/37712).
- The instance and its associated instances are in **Running** status and are not executing any tasks.
- You have calculated the required specifications and understood the fees. Make sure that your Tencent Cloud account balance is sufficient.

## Scaling Memory Edition Instance in Standard Architecture

>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- To expand the capacity of a Memory Edition instance in standard architecture, if the remaining available capacity of the physical machine is insufficient, a migration will occur, which will not affect your access to the instance. However, if the instance is running on Redis 2.8, a momentary disconnection will occur after the migration is completed, so we recommend that your business have a reconnection mechanism.
>- As the maximum capacity of a Memory Edition instance in standard architecture is 64 GB, you cannot expand its capacity beyond that limit.
>- To avoid failure in capacity reduction, the capacity after reduction must be at least 1.3 times the amount of existing data. After the capacity reduction, you will receive an automatic refund.
>- As a trial version, the 256 MB specification on v4.0 or v5.0 is only suitable for product verification in testing environments but not recommended for use in production environments. It is available only in:
>Guangzhou (Zones 6 and 7), Shanghai (Zones 2, 3, 4 and 5), and Beijing (Zones 1, 2, 3, 4, 5, 6, and 7). Other 1 GB and above specifications can be downgraded to the 256 MB specification.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. In the **Operation** column, expand or reduce nodes or add or delete replicas.
  - Select **Configure** > **Expand Node** to enter the **TencentDB for Redis Configuration Changes** page and select the desired node capacity.
  - Select **Configure** > **Reduce Node** to enter the **TencentDB for Redis Configuration Changes** page and select the desired node capacity. The parameters for node reduction are similar to those for node expansion. **Capacity After Expansion** refers to the capacity specification of each shard after reduction. The instance capacity after reduction must be at least 1.3 times the used capacity. You should compare the capacity specification before and after reduction to check whether this requirement is met.
![](https://qcloudimg.tencent-cloud.cn/raw/4cd856bdb7e45e565d143edaa5ea05bc.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Used Capacity</td><td>Used capacity of the current instance.</td></tr>
<tr>
<td>Min Memory</td><td>Minimum memory specification of the current instance required to prevent the disk space from being used up.</td></tr>
<tr>
<td>Capacity After Expansion</td><td>Capacity specification per shard after scaling.</td></tr>
<tr>
<td>Compare</td>
<td>Compare the current configuration with the new configuration, including **Shard Quantity**, **Shard Specs**, **Replica Quantity**, **Total Capacity**, **Total Connections**, and **Max Traffic**.</td></tr>
<tr>
<td>Configuration Change Fee</td>
<td><ul> <li> <strong>Pay-as-you-go</strong>: Hourly unit price after instance configuration adjustment. You can click <strong>Billing Details</strong> to view the billable items and billing formula and confirm the fees.</li></ul></td></tr>
</tbody></table>

  - Select **Configure** > **Add Replica** to enter the **TencentDB for Redis Configuration Changes** page. Select the desired number of replicas in the drop-down list next to **Replica Quantity**. Other parameters are similar to those during node expansion. For more information on how to add replicas to a multi-AZ deployed instance, see [Adding Replicas to Multi-AZ Deployed Instance](https://intl.cloud.tencent.com/document/product/239/46556).
  - Select **Configure** > **Delete Replica** to enter the **TencentDB for Redis Configuration Changes** page. Select the desired number of replicas in the drop-down list next to **Replica Quantity**. Other parameters are similar to those for node expansion.
![](https://qcloudimg.tencent-cloud.cn/raw/b5976cb9fdb873c586af9a0b41eeee32.png)
5. Confirm the configuration adjustment and click **OK**.
6. Return to the instance list. After the **Instance Status** changes to **Running**, the instance can be used normally.

## Scaling Memory Edition Instance in Cluster Architecture
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- To avoid failure in capacity reduction, the capacity after reduction must be at least 1.3 times the amount of existing data. After the capacity reduction, you will receive an automatic refund.
>- When shards are added or deleted, the system will automatically balance the slot configuration and migrate data, which may fail in rare cases. We recommend you perform such operations during off-peak hours to avoid the impact of migration on business access.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. In the **Operation** column, expand or reduce nodes or add or delete replicas or shards.
   - Select **Configure** > **Expand Node** to enter the **TencentDB for Redis Configuration Changes** page and select the desired node capacity per shard.
   - Select **Configure** > **Reduce Node** to enter the **TencentDB for Redis Configuration Changes** page and select the desired node capacity per shard. The parameters for node reduction are similar to those for node expansion. **Shard Size** refers to the capacity specification of each shard after reduction. The instance capacity after reduction must be at least 1.3 times the used capacity. You should compare the capacity specification before and after reduction to check whether this requirement is met.
![](https://qcloudimg.tencent-cloud.cn/raw/5c40a66daab927dc2695b09c8ba36ab4.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Used Capacity</td><td>Used capacity of the current cluster instance.</td></tr>
<tr>
<td>Min Memory</td><td>Minimum memory specification per shard of the current cluster instance required to prevent the disk space from being used up.</td></tr>
<tr>
<td>Shard Size</td><td>Capacity specification per shard after scaling.</td></tr>
<tr>
<td>Compare</td>
<td>Compare the current configuration with the new configuration, including **Shard Quantity**, **Shard Specs**, **Replica Quantity**, **Total Capacity**, **Total Connections**, and **Max Traffic**.</td></tr>
<tr>
<td>Configuration Change Fee</td>
<td><ul> <li> <strong>Pay-as-you-go</strong>: Hourly unit price after instance configuration adjustment. You can click <strong>Billing Details</strong> to view the billable items and billing formula and confirm the fees.</li></ul></td></tr>
</tbody></table>

   - Select **Configure** > **Add Replica** to enter the **TencentDB for Redis Configuration Changes** page. Select the desired number of replicas in the drop-down list next to **Replica Quantity**. Other parameters are similar to those for node expansion. For more information on how to add replicas to a multi-AZ deployed instance, see [Adding Replicas to Multi-AZ Deployed Instance](https://intl.cloud.tencent.com/document/product/239/46556).
   - Select **Configure** > **Delete Replica** to enter the **TencentDB for Redis Configuration Changes** page. Select the desired number of replicas in the drop-down list next to **Replica Quantity**. Other parameters are similar to those for node expansion.
![](https://qcloudimg.tencent-cloud.cn/raw/801aabcb920a549776c8addeb10981b1.png)
   - Select **Configure** > **Add Shard** to enter the **TencentDB for Redis Configuration Changes** page. Select the desired number of shards in the drop-down list next to **Shard Quantity**. Other parameters are similar to those for node expansion.
   - Select **Configure** > **Delete Shard** to enter the **TencentDB for Redis Configuration Changes** page. Select the desired number of shards in the drop-down list next to **Shard Quantity**. Other parameters are similar to those for node expansion.
![](https://qcloudimg.tencent-cloud.cn/raw/dd96b99885d4faba2d2346fb7bd139af.png)
5. Confirm the configuration adjustment and click **OK**.
6. Return to the instance list. After the **Instance Status** changes to **Running**, the instance can be used normally.

## Related APIs

| API | Description |
| :----------------------------------------------------------- | :------------- |
| [UpgradeInstance](https://intl.cloud.tencent.com/document/product/239/32052) | Upgrades instance configuration |
