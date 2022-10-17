## Overview

If your purchased TencentDB for MongoDB instance is overprovisioned or underprovisioned, your business needs cannot be best met, and you can quickly adjust its specifications as needed (at the start, during rapid development, or during peak/off-peak hours), so you can fully utilize resources and reduce unnecessary costs in real time.

You can change the mongod computing specification and disk capacity for mongod nodes. In order to choose the specifications that best suit your needs, we recommend that you first check TencentDB [Product Specifications](https://intl.cloud.tencent.com/document/product/240/31183) before making a choice.

## Billing

The instance will be billed by the new configurations after its configurations are changed. Make sure that your Tencent Cloud account balance is sufficient. For more information, see [Configuration Adjustment Billing](https://intl.cloud.tencent.com/document/product/240/44174).

## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- If your instance is pay-as-you-go, make sure that your Tencent Cloud account balance is sufficient.
- The instance and its associated instances are in **Running** status and are not executing any tasks.

## Notes
- Instance memory and capacity adjustment involves adding the nodes with selected configurations to the cluster for data sync, during which the service is not affected. After data sync is completed, the old nodes will be removed, and a new primary node will be elected. A momentary disconnection for around 10s will occur with the instance service during election. We recommend you include disaster recovery in your business code and perform the adjustment during off-peak hours.
- During adjustment, there may be one or two momentary disconnections for about 10s each. We recommend you configure an automatic reconnection feature for your application.
- During adjustment, if you set the write concern level to `write majority`, there may be a short request delay; therefore, set an appropriate business timeout period.
- The name, private network address, and port of the instance remain unchanged after configuration adjustment.
- A started configuration adjustment task cannot be canceled.

## Directions

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** in the **Adjust Configuration** drop-down list.
6. On the **Adjust Configuration** page, you can adjust the node memory, total disk capacity, and oplog capacity (with sharded instance as an example):
![](https://qcloudimg.tencent-cloud.cn/raw/bd4711cf6531dde88e57077f952a05f0.png)
<table class="table-striped">
<tbody>
<tr><th>Parameter</th><th>Description</th><th>Example</th></tr>
<tr>
<td>Instance Name</td>
<td>The name of the instance for which to adjust the configuration.</td>
<td>test-4dot2-XXX</td></tr>	
<tr>
<td>Instance Architecture</td>
<td>The description of the instance's cluster architecture. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44173">System Architecture</a>.</td>    
<td>A sharded cluster instance has two shards, each shard consists of three storage nodes to form a replica set, and the entire instance has six storage nodes in total</td></tr>	
<tr>
<td>Node Memory/Total Capacity</td>
<td>The mongod node memory and total capacity per node in the current instance. For a sharded cluster, the total node capacity is the node capacity per shard. For how to query the number of CPU cores of an instance, see the mongod specifications in <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>.</td>   
<td>4 GB/100 GB</td></tr>
<tr>
<td>Node Memory</td>
<td>Select the new memory per mongod node in the drop-down list. For how to choose a specification, see the mongod specifications in <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>.</td>    
<td>8 GB</td></tr>
<tr>
<td>Total Node Capacity</td>
<td>Adjust the total disk capacity per mongod node on the slider, which is the same as the total capacity of the current node by default. For how to choose a specification, see the mongod specifications in <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>.</td>    
<td>500 GB</td></tr>
<tr>
<td>Oplog Capacity</td>
<td>We recommend you also adjust the oplog capacity on the slider: <ul><li>The oplog capacity is at least 10% of the instance capacity. </li><li>If the oplog is too small, it is easy to be cleaned up, and rollback will be further affected. </li><li>When the instance is downgraded, the oplog is initialized to 10% of the new storage specification. The first write time of the oplog will be overwritten after the last backup is successfully executed. To prevent rollback from being affected in this case, manually back up before the downgrade.</li></ul></td>   
<td>50 GB</td></tr>
<tr>
<td>Switch Time</td>
<td><ul><li>If you select <b>Upon modification completion</b>, the instance specification adjustment task will be executed immediately. Instance memory and capacity adjustment may involve node migration or primary-secondary switch. As the switch time point is uncontrollable, disconnection or restart may occur. </li><li>If you select <b>During maintenance time</b>, the task will be executed during the maintenance time. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/31190">Setting Instance Maintenance Time</a>.</li></ul></td>    
<td>During maintenance time</td></tr>
<tr>
<td>Fees</td>
<td><ul><li><b>Pay-as-you-go</b>: Hourly unit price after instance configuration adjustment. You can click <b>Billing Details</b> to view the billable items and billing formula and confirm the fees. </li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44174">Configuration Adjustment Billing</a>.</td>    
<td>177.991 USD</td></tr>
</tbody></table>
7. After confirming that everything is correct, click **Submit**.

## Related APIs

| API                                                 | Description     |
| ------------------------------------------------------------ | -------------------- |
| [ModifyDBInstanceSpec](https://intl.cloud.tencent.com/document/product/240/34699) | Adjusts TencentDB instance configuration. |

