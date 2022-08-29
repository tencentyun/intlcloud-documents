## Overview

 When you purchase the instance, the oplog capacity is 10% of the instance capacity by default. It can be expanded to 90% of the instance capacity. Capacity reduction is not supported now.

## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- If your instance is pay-as-you-go, make sure that your Tencent Cloud account balance is sufficient.
- The instance and its associated instances are in **Running** status and are not executing any tasks.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Oplog/Shard Info** column, click **View/Adjust**.
![](https://qcloudimg.tencent-cloud.cn/raw/c6f8a9125efd8e0d8a4473e9ac73379a.png)
6. In the **Adjust Oplog** pop-up window, confirm the instance information and evaluate the target oplog capacity based on the current capacity.

<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Shard ID</td><td>Instance ID.</td></tr>
<tr>
<td>Storage Node Quantity</td><td>The number of primary and secondary mongod nodes in the instance.</td></tr>
<tr>
<td>Total capacity of shard</td><td>The mongod node disk capacity per shard.</td></tr>
<tr>
<td>Occupied shard capacity</td><td>The occupied mongod node capacity per shard.</td></tr>
<tr>
<td>Oplog Capacity</td><td>The mongod node oplog storage capacity per shard.</td></tr>
</tbody></table>
7. Click **Next** to adjust the oplog capacity.
![](https://qcloudimg.tencent-cloud.cn/raw/48fefb34c1644bf5dd38a055e648f055.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Resource ID</td><td>Instance ID.</td></tr>
<tr>
<td>Time taken for remaining capacity to be fully occupied</td><td>The time it will take for the remaining capacity to be fully occupied.</td></tr>
<tr>
<td>Current Total Capacity</td><td>The mongod node oplog storage capacity per shard.</td></tr>
<tr>
<td>Capacity after Expansion</td><td>Expand the oplog capacity on the slider.</td></tr>
</tbody></table>
8. Click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/d16e35c170a2ba14e5ac72603496f1c9.png)
