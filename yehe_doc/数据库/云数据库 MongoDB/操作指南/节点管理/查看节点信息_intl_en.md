## Overview

TencentDB for MongoDB allows you to view the instance node information, including node ID, role, running status, and used capacity. In addition, it supports node management operations, such as adjusting node specification, promoting replica node to primary node, enabling read-only replica, and configuring primary/replica failover. You can use node management to efficiently manage instance nodes and locate node exceptions.

## Directions

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the **Instance List** on the right, select the region.
4. In the **Instance List**, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. View the mongod and mongos node information.
 - **Mongod node**
![](https://qcloudimg.tencent-cloud.cn/raw/62f4825dcb8431e543617e49c6b46afd.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Node ID</td>
<td>Mongod node ID.</td></tr>
<tr>
<td>Monitoring</td>
<td>Click <img src="https://qcloudimg.tencent-cloud.cn/raw/dc4a0ccd630c929fcb9095841df8fb0d.png" style="zoom:40%;">, and you can view the monitoring views of various metrics of the node on the monitoring panel on the right. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/3564">Viewing Monitoring Data</a>.</td></tr>
<tr>
<td>Status</td><td>Running status of the current node.</td></tr>
<tr>
<td>AZ</td><td>AZ of the current node.</td></tr>
<tr>
<td>Role</td>
<td>Role of the current node. <ul><li>PRIMARY: Primary node. </li><li>SECONDARY: Replica node. </li><li>READONLY: Read-only node.</li></ul></td></tr>
<tr>
<td>Priority</td>
<td>The priority of a node for being elected as the primary node. The greater the value, the higher the priority.</td></tr>
<tr>
<td>Hidden</td>
<td>Whether the node is hidden. Default value: `false`.</td></tr>
<tr>
<td>Primary/Replica Delay (sec)</td>
<td>The latency in syncing data from the primary node to the replica node in seconds.</td></tr>
<tr>
<td>Disk Utilization</td><td>Utilization of the node disk.</td></tr>
</tbody></table>
 - **Mongos node**
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Node ID</td><td>Mongos node ID.</td></tr>
<tr>
<td>Monitoring</td>
<td>Click <img src="https://qcloudimg.tencent-cloud.cn/raw/dc4a0ccd630c929fcb9095841df8fb0d.png" style="zoom:40%;">, and you can view the monitoring views of various metrics of the node on the monitoring panel on the right. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/3564">Viewing Monitoring Data</a>.</td></tr>
<tr>
<td>Status</td><td>Status of the node.</td></tr>
<tr>
<td>AZ</td><td>AZ of the mongos node.</td></tr>
</tbody></table>

