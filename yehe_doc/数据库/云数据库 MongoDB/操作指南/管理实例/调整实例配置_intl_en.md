## Overview

If the configuration of your purchased TencentDB for MongoDB instance isn't suitable for (either below or above) your current business requirements, you can quickly adjust its specifications according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

Instance configuration modification includes adjusting the instance's computing specification, storage capacity, and number of nodes. Sharded clusters also support adjusting the number of shards and the number of nodes per shard. Before adjusting the configuration, understand the [product specifications](https://intl.cloud.tencent.com/document/product/240/31183) supported by TencentDB first, so you can choose the most appropriate specifications for your business. 

## Version Requirement

- Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support adjusting the instance memory and capacity specifications.
- TencentDB for MongoDB 4.2 replica set instances don't support adjusting the number of instance nodes.
- TencentDB for MongoDB 4.2 sharded instances don't support adjusting the number of nodes per shard and the number of shards.
- TencentDB for MongoDB 3.2 sharded instances don't support adjusting the number of shards.

## Billing Description

After the instance configuration is adjusted, the instance will be billed by the new configuration. Make sure that your Tencent Cloud account balance is sufficient. For more information, see [Configuration Adjustment Billing](https://intl.cloud.tencent.com/document/product/240/44174).

## Prerequisites

- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- If your instance is pay-as-you-go, make sure that your Tencent Cloud account balance is sufficient.
- The instance and its associated instances are in **Running** status and are not executing any tasks.

## Adjust Computing Specification and Storage Capacity
>?
>- Instance memory and capacity adjustment involves adding the nodes with selected configurations to the cluster for data sync, during which the service is not affected. After data sync is completed, the old nodes will be removed, and a new primary node will be elected. A momentary disconnection for around 10s will occur with the instance service during election. We recommend you include disaster recovery in your business code and perform the adjustment during off-peak hours.
>- During adjustment, there may be one or two momentary disconnections for around 10s each. We recommend you configure an automatic reconnection feature for your application.
>- During adjustment, if you set the write concern level to `write majority`, there may be a short request delay; therefore, set an appropriate business timeout period.
>- The name, private network address, and port of the instance remain unchanged after configuration adjustment.
>- A started configuration adjustment task cannot be canceled.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**.
   The directions for replica set instances and sharded instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** in the **Adjust Configuration** drop-down list.
6. On the **Adjust Configuration** page, you can adjust the node memory, node capacity, and oplog capacity as shown below (with sharded instance as an example):
![](https://qcloudimg.tencent-cloud.cn/raw/a2bbed28ad4f9bce7038ac0dd67ff4d4.png)
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
<td>The memory and total capacity per node in the current instance. For a sharded cluster, the total node capacity is the node capacity per shard. For how to query the number of CPU cores of an instance, see the mongod specifications in <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>. For example, the instance memory of 4 GB corresponds to 2 CPU cores.</td>   
<td>4 GB/1230 GB</td></tr>
<tr>
<td>Node Memory</td>
<td>Select the new memory per node in the drop-down list, which is the same as the current node memory by default. For how to choose a specification, see the mongod specifications in <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>. For example, the instance memory of 8 GB corresponds to 4 CPU cores.</td>    
<td>8 GB</td></tr>
<tr>
<td>Total Node Capacity</td>
<td>Adjust the total capacity per node on the slider, which is the same as the total capacity of the current node by default. For how to choose a specification, see the mongod specifications in <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>. For example, 4-core 8 GB MEM corresponds to the storage capacity of 20–3000 GB.</td>    
<td>1230 GB</td></tr>
<tr>
<td>Oplog Capacity</td>
<td>We recommend you also adjust the oplog capacity on the slider: <ul><li>The oplog capacity is at least 10% of the instance capacity. </li><li>If the oplog is too small, it is easy to be cleaned up, and rollback will be further affected. </li><li>When the instance is downgraded, the oplog is initialized to 10% of the new storage specification. The first write time of the oplog will be overwritten after the last backup is successfully executed. To prevent rollback from being affected in this case, please manually back up before the downgrade.</li></ul></td>   
<td>123 GB</td></tr>
<tr>
<td>Switch Time</td>
<td><ul><li>If you select <b>Upon modification completion</b>, the instance specification adjustment task will be executed immediately. Instance memory and capacity adjustment may involve node migration or primary-secondary switch. As the switch time point is uncontrollable, disconnection or restart may occur. </li><li>If you select <b>During maintenance time</b>, the task will be executed during the maintenance time. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/31190">Setting Instance Maintenance Period</a>.</li></ul></td>    
<td>Maintenance time</td></tr>
<tr>
<td>Fees</td>
<td><ul><li><b>Pay-as-you-go</b>: Hourly unit price after instance configuration adjustment. You can click <b>Billing Details</b> to view the billable items and billing formula and confirm the fees. </li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44174">Configuration Adjustment Billing</a>.</td>    
<td>xxx.xx USD</td></tr>
</tbody></table>

8. After confirming that everything is correct, click **Submit**.

## Adjusting Node Quantity
>?
>- After new nodes are added to the cluster, data sync will start without affecting the business.
>- Be sure to plan for disaster recovery. We recommend you initiate a configuration adjustment task during the maintenance time. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/240/31190).
>- Do not adjust the node quantity and node computing/storage specifications at the same time.
>- After the node quantity is adjusted, billing will start according to the new specification.
>- The name, private network address, and port of the instance remain unchanged after node quantity adjustment.
>- A started configuration adjustment task cannot be canceled.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** > **Adjust Node Quantity**.
6. In the **Adjust Node Quantity** window, read the notes on node quantity adjustment and confirm the instance name, expiration time, etc. for node quantity adjustment.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c82a5988931996445673c21abbe82eca.png" style="80%;" />
<table class="table-striped">
<tbody>
<tr><th>Parameter</th><th>Description</th><th>Example</th></tr>
<tr>
<td>Instance Name</td>
<td>The name of the instance for which to adjust the node quantity.</td>
<td>test-4dot2-XXXX</td></tr>	
<tr>
<td>Instance Architecture</td>
<td>The description of the instance's cluster architecture. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44173">System Architecture</a>.</td>    
<td>A replica set instance with three storage nodes</td></tr>	
<tr>
<td>Node Specification</td>
<td>The node specification information of the current replica set, including the number of CPU cores, memory, storage capacity, and node quantity.</td>   
<td>2 cores, 4 GB memory, 20 GB storage, three nodes in total</td></tr>
<tr>
<td>Node Quantity</td>
<td>Select a new node quantity for the instance in the drop-down list, which is the same as the current node quantity by default. <ul><li><b>3</b>: The node quantity cannot be decreased but can only be increased to 5 or 7. </li><li><b>5</b>: The node quantity can be decreased to 3 or increased to 7. </li></li><li><b>7</b>: The node quantity can be decreased to 3 or 5.</li></ul></td>    
<td>5</td></tr>
<tr>
<td>Fees</td>
<td><ul><li><b>Pay-as-you-go</b>: Hourly unit price after instance configuration adjustment. You can click <b>Billing Details</b> to view the billable items and billing formula and confirm the fees. </li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44174">Configuration Adjustment Billing</a>.</td>    
<td>x.xx USD/hour</td></tr>
</tbody></table>

7. Confirm the billing information and click **OK**.

## Adjusting Node Quantity per Shard (for Sharded Instance)

>?
>- Be sure to plan for disaster recovery. We recommend you initiate a configuration adjustment task during the maintenance time. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/240/31190).
>- Do not adjust the node quantity per shard, shard quantity, and node computing/storage specifications at the same time.
>- After new nodes are added to the cluster, data sync will start without affecting the business.
>- After the node quantity is adjusted, billing will start according to the new specification.
>- The name, private network address, and port of the instance remain unchanged after node quantity adjustment.
>- A started configuration adjustment task cannot be canceled.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** > **Adjust Node Quantity per Shard**.
6. In the **Adjust Node Quantity per Shard** window, read the notes on node quantity adjustment.
7. In the **Node Quantity** input box, select the desired numbers of primary and secondary nodes as detailed below:
   - **3**: Downgrade is not supported.
   - **5**: Downgrade to **3** nodes is supported.
   - **7**: Downgrade to **3** or **5** nodes is supported.
8. Confirm the billing information and click **OK**.

## Adjusting Shard Quantity (for Sharded Instance)

> ?
> - Be sure to plan for disaster recovery. We recommend you initiate a configuration adjustment task during the maintenance time. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/240/31190).
> - Do not adjust the node quantity per shard, shard quantity, and node computing/storage specifications at the same time.
> - Currently, shards can be only added but not removed for sharded instances. After new shards are added to the cluster, data sync will start without affecting the business.
>- After the shard quantity is adjusted, billing will start according to the new specification.
>- The name, private network address, and port of the instance remain unchanged after shard quantity adjustment.
> - A started configuration adjustment task cannot be canceled.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** > **Adjust Shard Quantity**.
6. In the **Adjust Shard Quantity** window, read the notes on shard quantity adjustment.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/00f3c392d07e9db1da70110fa280aa10.png" style="zoom:80%;" />
<table class="table-striped">
<tbody>
<tr><th>Parameter</th><th>Description</th><th>Example</th></tr>
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
<td>Number of shards</td>
<td>Select a new shard quantity for the instance from the drop-down list, which is the same as the current shard quantity by default. The value range is 2–19.</li></ul></td>   
<td>3</td></tr>
<tr>
<td>Fees</td>
<td><ul><li><b>Pay-as-you-go</b>: Hourly unit price after instance configuration adjustment. You can click <b>Billing Details</b> to view the billable items and billing formula and confirm the fees. </li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44174">Configuration Adjustment Billing</a>.</td>    
<td>x.xx USD/hour</td></tr>
</tbody></table>

7. After confirming that everything is correct, click **Submit**.

## Related APIs

| API | Description |
| ------------------------------------------------------------ | -------------------- |
| [ModifyDBInstanceSpec](https://intl.cloud.tencent.com/document/product/240/34699) | Adjusts TencentDB instance configuration. |


