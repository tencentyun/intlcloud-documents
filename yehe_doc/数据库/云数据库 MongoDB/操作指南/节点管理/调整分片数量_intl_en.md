## Overview

You can adjust the shard quantity after purchasing a sharded cluster instance to adapt to your changing business scenarios.

## Billing

After the instance configuration is adjusted, the instance will be billed by the new configuration. Make sure that your Tencent Cloud account balance is sufficient. For more information, see [Configuration Adjustment Billing](https://intl.cloud.tencent.com/document/product/240/44174).

## Notes

- After new nodes are added to the cluster, data sync will start without affecting the business.
- Do not adjust the node quantity and node computing/storage specifications at the same time.
- After the node quantity is adjusted, billing will start based on the new specification.
- The name, private network address, and port of the instance remain unchanged after node quantity adjustment.
- A started configuration adjustment task cannot be canceled.

## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- If your instance is pay-as-you-go, make sure that your Tencent Cloud account balance is sufficient.
- The sharded cluster instance and its associated instances are in **Running** status and are not executing any tasks.

## Directions

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Cluster Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. On the **Mongod Node** tab on the **Node Management** tab, click **Adjust Shard Quantity**.
7. In the **Adjust Shard Quantity** window, read the notes on shard quantity adjustment.
![](https://qcloudimg.tencent-cloud.cn/raw/b7915589ca312543d9a9584913ef6d3b.png)
<table class="table-striped">
<tbody>
<thead><tr><th>Parameter</th><th>Description</th><th>Example</th></tr></thead>
<tr>
<td>Instance Name</td>
<td>The name of the instance for which to adjust the node quantity.</td>
<td>test-4dot2-XXX</td></tr>	
<tr>
<td>Instance Architecture</td>
<td>The description of the instance's cluster architecture. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44173">System Architecture</a>.</td>    
<td>Sharded cluster instance with two shards and five storage nodes per shard</td></tr>	
<tr>
<td>Node Specification</td>
<td>The shard node specification information of the current sharded cluster instance, including the number of CPU cores, memory, storage capacity, and node quantity.</td>   
<td>2 cores, 4 GB memory, 250 GB storage, ten nodes in total</td></tr>
<tr>
<td>Added Shards</td>
<td>Select the number of shards to be added to the instance. Value range: [1,18].</li></ul></td>   
<td>3</td></tr>
<tr>
<td>Fees</td>
<td><ul><li><b>Pay-as-you-go</b>: Hourly unit price after instance configuration adjustment. You can click <b>Billing Details</b> to view the billable items and billing formula and confirm the fees. </li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44174">Configuration Adjustment Billing</a>.</td>    
<td>0.99 USD/hour</td></tr>
</tbody></table>
8. After confirming that everything is correct, click **Submit**.

## Related APIs

| API                                                 | Description     |
| ------------------------------------------------------------ | -------------------- |
| [ModifyDBInstanceSpec](https://intl.cloud.tencent.com/document/product/240/34699) | Adjusts TencentDB instance configuration. |

