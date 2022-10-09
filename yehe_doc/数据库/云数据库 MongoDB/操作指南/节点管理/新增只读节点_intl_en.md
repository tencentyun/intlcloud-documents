## Overview
When your business has a massive number of read requests, it may be difficult for the primary and secondary database nodes to process such requests, causing a high latency, slow response, and severely dropped throughput of business requests. TencentDB for MongoDB provides read-only nodes with an independent connection address. They can sync data from a primary or secondary node with the lowest latency through oplog. You can create one or multiple read-only nodes to implement read/write separation and relieve the access pressure on the primary and secondary nodes.

Two or more nodes can implement load balancing for read requests and guarantee a high availability; that is, when a read-only node fails, the system will automatically switch it with a hidden node. If automatic switch isn't performed, you can switch the node by your own on the **Node Management** tab, and the connection address to the node will remain unchanged. You can directly get the connection string in the **Network** section on the **Instance Details** page.

If a read-only node isn't in the candidate list of the primary node, it won't be elected as the primary node or participate in the election.

## Version requirements
TencentDB for MongoDB 4.0, 4.2 and 4.4 support adding read-only nodes, while 3.6 doesn't.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the **Instance List** on the right, select the region.
4. In the **Instance List**, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. On the **Mongod Node** tab, click **Add Read-only Node**.
![](https://qcloudimg.tencent-cloud.cn/raw/e2abdfcdf60c99e169e4bf3fec1e5669.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance Configuration</td>
<td>Check the current specification of the instance, including the CPU core quantity, memory, disk capacity, total node quantity, and read-only node quantity to evaluate the number of read-only nodes to be added.</td></tr>
<tr>
<td>Add Read-Only Node</td>
<td>The number of new read-only nodes. Value range: 0–5.</td></tr>
<tr>
<td>AZ</td>
<td>The AZ where all read-only nodes are deployed. This parameter will be displayed if the instance nodes are in the same AZ.</td></tr>
<tr>
<td>Compare</td>
<td>Compare the specifications before and after read-only nodes are added to assess whether the new specification meets your needs.<ul><li>The specification of a replica set instance includes mongod specification, disk capacity, number of read-only nodes, and maximum number of connections.</li><li>The specification of a sharded cluster instance includes number of shards, mongod specification, disk capacity, number of read-only nodes, and maximum number of connections.</li></ul></td></tr>
<tr>
<td>Total Fees</td>
<td><ul><li>Pay-as-you-go: Hourly unit price after instance configuration adjustment. You can click <b>Billing Details</b> to view the billable items and billing formula and confirm the fees. </li>For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44174">Configuration Adjustment Billing</a>.</li></ul></td></tr>
</tbody></table>
7. Click **OK**.
8. On the left sidebar, select **Task Management**. In the task list, find the instance by ID or name and wait for **Task Status** of the read-only node adding task to become **Completed**.

