## Overview

The network bandwidth required varies depending on the instance specifications. If the traffic exceeds the bandwidth cap, it may cause congestion and affect the service performance. For example, to handle business traffic peaks during flash sales, or to eliminate the impact of the bandwidth limit when a lot of big key reads and writes occur temporarily, you can quickly increase the instance bandwidth to avoid affecting the business. 

## Billing

Increasing the bandwidth is free of charge currently but will be billed in the future.

## Concepts

- **Standard bandwidth**: It is the bandwidth per (master or replica) node in the instance.
- **Read-only replica bandwidth**: Each read-only replica has the same bandwidth as that of the master.
- **Additional bandwidth**: If the standard bandwidth cannot meet your needs, you can add additional bandwidth.

## Notes

Increasing the bandwidth will not affect your business, but reducing the bandwidth may cause throttling of the traffic that exceeds the bandwidth.

## Prerequisites

- The database instance is on v4.0 or later.
- The database instance is in **Running** status.
- The bandwidth of the database instance isn't suitable for the current business.

## Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **Instance List** on the right, select the region.
3. In the instance list, find the target instance.
4. Open the **Adjust Bandwidth** pop-up window in any of the following ways:
    - In the **Operation** column of the target instance, select **Configure** > **Adjust Bandwidth**. 
    - Click the instance ID and click **Adjust Bandwidth** after **Max Network Throughput** in the **Network Info** section on the **Instance Details** page.
5. In the **Adjust Bandwidth** pop-up window, select the desired additional bandwidth on the slider bar after **Additional Bandwidth**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/64ae0838ff5d2444e4c96f7ed741ca2e.png" style="zoom:50%;" />
<table>
<thead>
<tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td><strong>Instance Name</strong></td>
<td>The instance name.</td></tr>
<tr>
<td><strong>Instance Specs</strong></td>
<td>The instance specification: Shard quantity, memory, and replica quantity.</td></tr>
<tr>
<td><strong>Read-Only Replica</strong></td>
<td>The read-only replica status.</td></tr>
<tr>
<td><strong>Standard Bandwidth</strong></td>
<td>The bandwidth per (master or replica) node in the instance.</td></tr>
<tr>
<td><strong>Additional Bandwidth</strong></td>
<td>Select the additional bandwidth on the slider bar.</td></tr>
<tr>
<td><strong>Total Instance Bandwidth</strong></td>
<td><ul><li>If read-only replica is enabled, the total instance bandwidth = additional bandwidth * shard quantity + standard bandwidth * shard quantity * Max ([read-only replica quantity, 1]). The shard quantity in the standard architecture is 1. <li>If read-only replica is not enabled, the total instance bandwidth = additional bandwidth * shard quantity + standard bandwidth * shard quantity. The shard quantity in the standard architecture is 1.</li></ul></td></tr>
<tr>
<td><strong>Fees</strong></td>
<td>Free of charge currently.</td></tr>
</tbody></table>
7. After confirming that the total bandwidth meets your expectations, click **Confirm**.
8. **Instance Status** will change to **Processing**. Wait for it to change to **Running**. Then, you can see that the **Max Network Throughput** is the updated total bandwidth in the **Network Info** section on the **Instance Details** page.


## Related APIs

| API | Description |
| :----------------------------------------------------------- | :--------------- |
| [ModifyNetworkConfig](https://intl.cloud.tencent.com/document/product/239/32056) | Modifies the network configuration of an instance to change its bandwidth. |


