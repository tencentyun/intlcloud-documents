## Overview
If the current database specification can‘t sustain massive concurrent application requests due to insufficient connections, **Connection Utilization** may get too high. To handle such access spikes, you can directly increase the number of maximum connections in the console.

## Notes
A single shard can sustain up to 10,000 connections by default, and the maximum number of connections to the entire instance is the maximum number of connections per shard multiplied by the shard quantity. A standard architecture instance has only one shard.

When you adjust the number of connections, the value range per shard is as detailed below:
- **If the read-only replica feature is disabled**
The maximum number of connections to each shard can be 10000–40000.
- **If the read-only replica feature is enabled**
The maximum number of connections to each shard can be 10000–10000 * (replica quantity + 3).

## Notes
- Increasing the maximum number of connections has no impact on the business.
- If the maximum number of connections is decreased, new connections may fail to be established when the number of connections reaches the upper limit. 
- If the problem persists after you increase the maximum number of connections, contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Prerequisites
- You have [created a TencentDB for Redis instance](https://intl.cloud.tencent.com/document/product/239/37712).
- The database instance is in **Running** status, with no ongoing tasks.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the target instance ID to enter the **Instance Details** page.
5. In the **Network Info** section on the **Instance Details** page, you can view the instance's current maximum number of connections after **Max Connections**. Click **Adjust**.
![](https://qcloudimg.tencent-cloud.cn/raw/df69f1409a2e3690997885e438dae06c.png)
6. In the **Adjust Max Connections** window, confirm the instance information and specification and increase the value.
 - **Standard architecture**
![](https://qcloudimg.tencent-cloud.cn/raw/4cddb051b81c846833b46a239b5d10af.png)
<table>
   <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
   <tbody><tr>
   <td>Instance Name</td><td>Instance name information.</td></tr>
   <tr>
   <td>Instance Specs</td><td>Instance specification information, including shard quantity, total memory, and replica quantity. A standard architecture instance has only one shard.</td></tr>
   <tr>
   <td>Read-Only Replica</td><td>Set whether the read-only replica feature (read/write separation) is enabled.</td></tr>
   <tr>
   <td>Max Connections</td><td>Adjust the maximum number of connections on the slider.</td></tr>
</tbody></table>
 - **Cluster architecture**
![](https://qcloudimg.tencent-cloud.cn/raw/08ed7ade2aab7409cba965773e67cda6.png)
<table>
   <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
   <tbody><tr>
   <td>Instance Name</td><td>Instance name information.</td></tr>
   <tr>
   <td>Instance Specs</td><td>Instance specification information, including shard quantity, shard capacity, and replica quantity.</td></tr>
   <tr>
   <td>Read-Only Replica</td><td>Set whether the read-only replica feature (read/write separation) is enabled.</td></tr>
   <tr>
   <td>Max Connections per Shard</td><td>Adjust the maximum number of connections to each shard on the slider.</td></tr>
   <tr>
   <td>Max Cluster Connections</td><td>The maximum number of connections to the entire instance is calculated automatically, which is the maximum number of connections per shard multiplied by the shard quantity.</td></tr>    
</tbody></table>
7. Click **OK**. On the left sidebar, you can click **Task Management** to view the task progress. After the task is executed, you can view the new maximum number of connections to the entire instance after **Max Connections** in the **Network Info** section on the **Instance Details** page.

## Related APIs

| API                   | Description                                                      |
| ------------------------- | ------------------------------------------------------------ |
| describeInstances | [Queries the list of instances](https://intl.cloud.tencent.com/document/product/239/32065). |

## FAQs
If you find that **Connection Utilization** in **System Monitoring** is too high, adjust the maximum number of connections as instructed in [High Connection Utilization](https://intl.cloud.tencent.com/document/product/239/44296).

