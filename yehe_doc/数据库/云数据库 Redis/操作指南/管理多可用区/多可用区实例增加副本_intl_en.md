## Overview

A multi-AZ deployed instance uses the one-replica architecture by default. One master node and two replica nodes are recommended, with the master node and one replica node deployed in the master AZ and the other replica node deployed in the replica AZ. This deployment mode maximizes the service availability and greatly reduces the delay caused by failures of the master node. If the master node fails, the replica node in the master AZ can be first elected as the new master node, ensuring that the access latency in the master AZ will not be affected by the switch of the master node to the replica AZ otherwise. For more information, see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/239/39812). We recommend you select the number of replicas based on your business needs.

## Billing Description

- Pay-as-you-go: The instance will be billed based on the new specification on the next hour under tier 1, and fees will be settled on each hour. For pricing details, see [Pricing](https://intl.cloud.tencent.com/document/product/239/9894).

## Notes

- If the number of replicas is increased, the instance will be charged at the price of the new specification.
- Increasing the number of replicas will not cause momentary disconnections or command execution failures or affect existing connections.

## Prerequisites

- The instance has been [configured with multi-AZ deployment](https://intl.cloud.tencent.com/document/product/239/39799).
- The database is on v4.0 or later.
- The instance is in **Running** status.

## Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **instance list** on the right, select the region.
3. In the instance list, find the target instance.
4. In the **Operation** column of the target instance, select **Configure** > **Add Replica**.
5. In the **TencentDB for Redis Configuration Changes** pop-up window, select the number of replicas to be added from the **Add Replica** drop-down list. Then, select AZs for them in the **AZ** drop-down list. The parameters are as described below.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td><strong>Used Capacity</strong></td>
<td>Capacity used by the current instance.</td></tr>
<tr>
<td><strong>Min Memory</strong></td>
<td>Minimum memory specification of the current instance required to prevent the disk space from being used up.</td></tr>
<tr>
<td><strong>Add Replica</strong></td>
<td>Specify the number of replicas to be added based on the required security level of your business data.</td></tr>
<tr>
<td><strong>AZ</strong></td>
<td>Specify AZs for the added replicas. For more information on how to configure this parameter, see <a href="https://intl.cloud.tencent.com/document/product/239/39812">Multi-AZ Deployment</a>.</td></tr>
<tr>
<td><strong>Compare</strong></td>
<td>Comparison of the specification before and after adding replicas. Check whether the new configuration meets your expectations.</td></tr>
<tr>
<td><strong>Configuration Change Fee</strong></td>
<td>Make sure that you understand the billing information of the new configuration. The hourly rate of the new configuration will be displayed for pay-as-you-go instances.</td></tr>
</tbody></table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/99d0b3d7415c2003e0994d2dec039874.png"  style="zoom: 80%;" />

6. After completing the configuration, click **OK**. Then, the **instance status** will change to **Processing**. Wait for the status to become **Running**.

## Related APIs

| API                                                 | Description |
| :----------------------------------------------------------- | :----------------------------------------------- |
| [UpgradeInstance](https://intl.cloud.tencent.com/zh/document/product/239/32052) | Upgrades instance specification, including the shard size, shard quantity, and replica quantity. |

