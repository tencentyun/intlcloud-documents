## Overview

The network bandwidth required by different instance specifications differ. If the traffic exceeds the bandwidth cap, it may cause congestion and affect the service performance. For example, to handle business traffic peaks during flash sales, or to eliminate the impact of the bandwidth limit when a lot of big key reads and writes occur temporarily, you can quickly increase the instance bandwidth so as to avoid affecting the business. 

## Billing

Increasing the bandwidth is free of charge currently and will be billed in the future.

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
2. Above the **instance list** on the right, select the region.
3. In the instance list, find the target instance.
4. Open the **Adjust Bandwidth** pop-up window in any of the following ways:
    - In the **Operation** column of the target instance, select **Configure** > **Adjust Bandwidth**. 
    - Click the instance ID and click **Adjust Bandwidth** after **Max Network Throughput** in the **Network Info** section on the **Instance Details** page.
5. In the **Adjust Bandwidth** pop-up window, select the desired additional bandwidth on the slider bar after **Additional Bandwidth**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7929fcd4b6637a686e8282e20d2d2e94.png" style="zoom:80%;" />
<table>
<thead>
<tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td><strong>Instance Name</strong></td>
<td>Instance name.</td></tr>
<tr>
<td><strong>Instance Specs</strong></td>
<td>Instance specification: Shard quantity, memory, and replica quantity.</td></tr>
<tr>
<td><strong>Read-Only Replica</strong></td>
<td>Read-only replica status.</td></tr>
<tr>
<td><strong>Standard Bandwidth</strong></td>
<td>Bandwidth per (master or replica) node in the instance</td></tr>
<tr>
<td><strong>Additional Bandwidth</strong></td>
<td>Select the additional bandwidth on the slider bar.</td></tr>
<tr>
<td><strong>Total Instance Bandwidth</strong></td>
<td>Total instance bandwidth = additional bandwidth x shard quantity + standard bandwidth x shard quantity x replica quantity. The shard quantity under the standard architecture is one, and the replica quantity is the sum of the number of master nodes and the number of replica nodes.</td></tr>
<tr>
<td><strong>Total Fees</strong></td>
<td>Free of charge currently.</td></tr>
</tbody></table>
7. After confirming that the total bandwidth meets your expectations, click **Confirm**.
8. The **instance status** will change to **Processing**. Wait for it to change to **Running**. Then, you can see that the **Max Network Throughput** is the updated total bandwidth in the **Network Info** section on the **Instance Details** page.


## Related APIs

| API | Description |
| :----------------------------------------------------------- | :--------------- |
| [ResetInstancesInternetMaxBandwidth](https://intl.cloud.tencent.com/document/product/213/33241) | Adjusts instance bandwidth cap |

