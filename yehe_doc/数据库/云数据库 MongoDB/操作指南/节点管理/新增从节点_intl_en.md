## Overview

All secondary nodes of an instance contribute to the system's high availability. When the primary node fails, each secondary node may be elected as the new primary node to execute data write requests. Therefore, the more the replicas, the higher the availability. In scenarios with a high number of concurrent requests with more reads and less writes, if read/write separation is enabled, you can add secondary nodes to improve the read performance and greatly relieve the read pressure on the primary node. 

A TencentDB for MongoDB cluster can have three (one-primary-two-replica), five (one-primary-four-replica), or seven (one-primary-six-replica) nodes in total. You can add secondary nodes appropriately based on the surge in the concurrent requests to your business and remove secondary nodes when the business load drops. This helps you better utilize resources and reduce unnecessary costs in real time.

## Billing

The instance will be billed by the new configurations after its configurations are changed. Make sure that your Tencent Cloud account balance is sufficient. For more information, see [Configuration Adjustment Billing](https://intl.cloud.tencent.com/document/product/240/44174).

## Notes
- After new nodes are added to the cluster, data sync will start without affecting the business.
- Be sure to plan for disaster recovery. We recommend you initiate a configuration adjustment task during the maintenance time. For more information, see [Setting Instance Maintenance Time](https://intl.cloud.tencent.com/document/product/240/31190).
- Do not adjust the node quantity and node computing/storage specifications at the same time.
- After the node quantity is adjusted, billing will start based on the new specification.
- The name, private network address, and port of the instance remain unchanged after node quantity adjustment.
- A started configuration adjustment task cannot be canceled.

## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- If your instance is pay-as-you-go, make sure that your Tencent Cloud account balance is sufficient.
- The instance and its associated instances are in **Running** status and are not executing any tasks.

## Adding a secondary node (replica set)

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. On the **Mongod Node** tab on the **Node Management** tab, click **Add Secondary Node**.
7. In the ***Adjust Node Quantity* pop-up window, read the notes on node quantity adjustment and confirm and configure the parameters as detailed below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/5061df9badcd8abe9fbb49845aea6d24.png" style="zoom:60%;" />
<table class="table-striped">
<tbody>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tr>
<td>Instance ID/Name</td>
<td>The name of the instance for which to adjust the node quantity.</td></tr>	
<tr>
<td>Instance Configuration</td>
<td>Check the current specification of the instance, including the CPU core quantity, memory, disk capacity, and node quantity. The node quantity includes all primary and secondary nodes. You should determine the number of nodes to be added based on the current specification.</td>    </tr>	
<tr>
<td>Nodes to Add</td>
<td>Select the number of secondary nodes to be added from the drop-down list.</td>   </tr>
<tr>
<td>Deployment AZ</td>
<td>This parameter will be displayed if the instance nodes are in the same AZ. It indicates the AZ where all instance nodes are deployed.</td>    </tr>
<tr>
<td>Secondary Node-n</td>
<td>This parameter will be displayed if the instance nodes are in different AZs. It indicates the AZs of different nodes and ranges from 0 to 6. Select the AZs for the new secondary nodes from the drop-down list.</td>    </tr>
<tr>
<td>Fees</td>
<td><ul><li><b>Pay-as-you-go</b>: Hourly unit price after instance configuration adjustment. You can click <b>Billing Details</b> to view the billable items and billing formula and confirm the fees. </li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44174">Configuration Adjustment Billing</a>.</td></tr>
</tbody></table>
8. Confirm the fees and click **OK**.
9. On the left sidebar, select **Task Management**, and you can view the ongoing task. Wait until **Task Progress** becomes **100%** and **Task Status** becomes **Completed**.

## Increasing the node quantity per shard (for sharded cluster instance)

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Cluster Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. On the **Mongod Node** tab on the **Node Management** tab, click **Add Secondary Node**.
7. In the ***Adjust Node Quantity per Shard* pop-up window, read the notes on node quantity adjustment and confirm and configure the parameters as detailed below:
 - **The instance nodes are deployed in the same AZ:**
   <img src="https://qcloudimg.tencent-cloud.cn/raw/b72ba798b7bfef78992af5fcfe58bc28.png" style="zoom: 90%;" />
 - **The instance nodes are deployed in different AZs:**<br>
   <img src="https://qcloudimg.tencent-cloud.cn/raw/139f5fcee966d2ea40d8322786ede1ab.png" style="zoom: 100%;" />
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance ID/Name</td>
<td>Confirm the name of the instance for which to adjust the node quantity per shard.</td></tr>
<tr>
<td>Instance Configuration</td>
<td>Check the current specification of the instance, including the CPU core quantity, memory, disk capacity, and node quantity. The node quantity includes all primary and secondary nodes. The nodes are evenly distributed to shards; for example, if there are two shards and eight nodes, each shard will have four nodes. You should determine the number of nodes to be added based on the current specification.</td></tr>
<tr>
<td>Nodes to Add</td>
<td>Select the number of secondary nodes to be added per shard from the drop-down list.</td></tr>
<tr>
<td>Deployment AZ</td>
<td>This parameter will be displayed if the instance nodes are in the same AZ. It indicates the AZ where all instance nodes are deployed.</td>
</tr>
<tr>
<td>Secondary Node-n</td>
<td>This parameter will be displayed if the instance shard nodes are in different AZs. It indicates the AZs of different nodes and ranges from 0 to 6. Select the AZs for the new secondary nodes from the drop-down list.</td></tr>
<tr>
<td>Fees</td>
<td><ul><li>Pay-as-you-go: Hourly unit price after instance configuration adjustment. You can click **Billing Details** to view the billable items and billing formula and confirm the fees.</li></ul></td></tr>
</tbody></table>
7. Conform the fees and click **OK**.
8. On the left sidebar, select **Task Management**, and you can view the ongoing task. Wait until **Task Progress** becomes **100%** and **Task Status** becomes **Completed**.

## Related APIs

| API                                                 | Description     |
| ------------------------------------------------------------ | -------------------- |
| [ModifyDBInstanceSpec](https://intl.cloud.tencent.com/document/product/240/34699) | Adjusts TencentDB instance configuration. |
