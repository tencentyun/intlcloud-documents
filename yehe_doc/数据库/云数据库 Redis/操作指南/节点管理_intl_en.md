
## Overview

TencentDB for Redis allows you to view the instance node information, including node ID, role, running status, and used capacity. In addition, it supports node management operations, such as adjusting node specification, promoting replica node to master node, enabling read-only replica, and configuring master/replica failover. You can use node management to efficiently manage instance nodes and locate node exceptions.

## Version Requirements

- All TencentDB for Redis **4.0** and **5.0** **standard architecture** **multi-AZ** instances **support** node management, while **single-AZ** instances **don't**.
- All TencentDB for Redis **4.0** and **5.0** **cluster architecture** single-AZ and multi-AZ instances **support** node management.
- TencentDB for Redis **2.8** instances **don't support** node management.

## Viewing Node Information

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **Instance List** on the right, select the region.
3. In the instance list, find the target instance.
4. Click the **instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
 - **Standard architecture multi-AZ instance**
![](https://qcloudimg.tencent-cloud.cn/raw/ef6412dd2491f70b1860934c5dbf07f5.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Node ID</td><td>Node ID of the database instance.</td></tr>
<tr>
<td>Monitoring</td>
<td>Click <img src="https://qcloudimg.tencent-cloud.cn/raw/dc4a0ccd630c929fcb9095841df8fb0d.png" style="zoom:50%;">, and you can view the monitoring views of various metrics of the node on the monitoring panel on the right. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Monitoring at Five-Second Granularity</a>.</td></tr>
<tr>
<td>Status</td><td>Running status of the current node.</td></tr>
<tr>
<td>AZ</td><td>AZ of the current node.</td></tr>
<tr>
<td>Role</td><td>Role of the current node, which is <b>Master Node</b> or <b>Replica Node</b>.</td></tr>
<tr>
<td>Used Memory</td><td>Node memory usage.</td></tr>
</tbody></table>
 - **Cluster architecture single-AZ instance**
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Node Name</td><td>Node name of the database instance.The node name is concatenated by Instance ID_Shard ID_Replica ID</td></tr>
<tr>
<td>Node ID</td><td>Node ID of the database instance.</td></tr>
<tr>
<td>Role</td><td>Node role, which is <b>Master Node</b> or <b>Replica Node</b>.</td></tr>
<tr>
<td>Key Quantity</td><td>Number of keys stored on the node.</td></tr>
<tr>
<td>Slots</td><td>Value range of the number of slots on the node.</td></tr>
<tr>
<td>Used Capacity</td><td>Node capacity usage.</td></tr>
</tbody></table>
 - **Cluster architecture multi-AZ instance**
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Node ID</td><td>Node ID of the database instance.</td></tr>
<tr>
<td>Role</td><td>Node role, which is <b>Master Node</b> or <b>Replica Node</b>.</td></tr>
<tr>
<td>Monitoring</td>
<td>Click <img src="https://qcloudimg.tencent-cloud.cn/raw/dc4a0ccd630c929fcb9095841df8fb0d.png" style="zoom:50%;">, and you can view the monitoring views of various metrics of the node on the monitoring panel on the right. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Monitoring at Five-Second Granularity</a>.</td></tr>
<tr>
<td>Status</td><td>Running status of the current node.</td></tr>
<tr>
<td>Slots</td><td>Value range of the number of slots on the node.</td></tr>
<tr>
<td>Used Memory</td><td>Node memory usage.</td></tr>
</tbody></table>

## More Operations
### Changing configuration
On the **Node Management** page, you can adjust the instance node specification by performing operations such as expanding/reducing node capacity, adding/deleting replicas, and adding/deleting shards (for cluster architecture). For more information on how to configure parameters, see [Changing Instance Specification](https://intl.cloud.tencent.com/document/product/239/31934).

**Multi-AZ standard architecture**
![](https://qcloudimg.tencent-cloud.cn/raw/9edaa9a8c1a56286ccd7b2e26d1f3979.png)
**Multi-AZ cluster architecture**
![](https://qcloudimg.tencent-cloud.cn/raw/1043c38109ff2f06b3c09d79c26eae16.png)

### Promoting replica node to master node in multi-AZ deployment
For a multi-AZ standard or cluster architecture instance, you can promote a replica node to the master node on the **Node Management** page. For detailed directions, see [Manually Promoting to Master Node (Group)](https://intl.cloud.tencent.com/document/product/239/41050).

### Simulating failure
To help you perform simulated failure testing, TencentDB for Redis offers the failure simulation feature. You can use this feature on the **Node Management** page. For detailed directions, see [Failover](https://intl.cloud.tencent.com/document/product/239/41052).

Failure simulation entry of **cluster architecture** instance:
<img src="https://qcloudimg.tencent-cloud.cn/raw/d2eb51b6c0981a56b9bbd2e2ea28a1b8.png" alt="img" style="zoom:50%;" />
Failure simulation entry of **standard architecture** instance:
<img src="https://qcloudimg.tencent-cloud.cn/raw/95a901a035d5cc8b915229c3f29a1efc.png" alt="img" style="zoom:80%;" /> 

### Read-only replica
On the **Node Management** page, if the instance has at least one replica, you can enable automatic read/write separation to expand the read performance vertically. For detailed directions, see [Enabling/Disabling Read/Write Separation](https://intl.cloud.tencent.com/document/product/239/31935).
![](https://qcloudimg.tencent-cloud.cn/raw/91aa7eb031feaca7b7394b98b332de93.png)

## Related APIs

| API | Description |
| ------------------------------------------------------------ | --------------------- |
| [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) | Queries instance node information      |


