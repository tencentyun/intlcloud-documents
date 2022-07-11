## Overview
After purchasing a TencentDB for Redis instance, you can quickly view its details in the console, such as the status, capacity usage, master/replica nodes in the cluster, and network status. You can also perform Ops and management operations efficiently.

## Prerequisites
- You have [created a TencentDB for Redis instance](https://intl.cloud.tencent.com/document/product/239/37712).
- The instance hasn't been terminated or isolated into the recycle bin. For more information, see [Recycle Bin](https://intl.cloud.tencent.com/document/product/239/46561).

## Viewing the Instance List
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
 - In the search box in the top-right corner, you can search for the target instance by instance ID, instance name, private IP, or tag key.
 - If you can't find the target instance in the instance list, select **Recycle Bin** on the left sidebar to check whether it is isolated there due to overdue payments. For more information, see [Recycle Bin](https://intl.cloud.tencent.com/document/product/239/46561).
4. View the target instance information, such as the status, specification, and storage engine.
![](https://qcloudimg.tencent-cloud.cn/raw/b972716f14f23e4f4502ba651db6eae7.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td><strong>Instance ID/Name</strong></td>
<td><ul><li>Instance ID: The instance's unique ID.</li><li>Name: Instance name set during instance creation. You can hover over the instance name and click <img src="https://qcloudimg.tencent-cloud.cn/raw/c3386f46a3b0588a84b3c0bf6f952200.png" style="zoom:66%;"> to rename the instance for easier identification and management.</li></ul></td></tr>
<tr>
<td><strong>Monitoring/Status/Task</strong></td>
<td><ul><li>Monitoring: You can click <img src="https://qcloudimg.tencent-cloud.cn/raw/fdc8f6a0ee6697f45d2497b1a0551f45.png" style="zoom:50%;"> to enter the monitoring panel and view the instance monitoring data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/34589">Monitoring at One-Second Granularity</a>.</li><li>Status: Instance status. The normal status is <b>Running</b>.</li><li>Task: If a task is being executed in the instance, the task name, such as **Changing configuration**, will be displayed here.</li></ul></td></tr>
<tr>
<td><strong>Project</strong></td>
<td>The project to which the instance belongs. You can create and manage multiple projects and view their billing details in <strong>Account Center</strong> > <strong>Project Management</strong> under your account. You can also move the instance to another project as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/31933">Assigning Instance to Project</a>.</td></tr>
<tr>
<td><strong>AZ</strong></td>
<td>The AZ where the instance resides. If <img src="https://qcloudimg.tencent-cloud.cn/raw/181252ff7be12ed247b08b5f3300af53.png" style="zoom: 50%;"> is displayed on the right of the AZ, the instance is deployed across AZs. You can hover over the icon to view the information of such AZs.</td></tr>
<tr>
<td><strong>Network</strong></td>
<td>The instance's VPC name, subnet name, and private IPv4 address. You can click the VPC name in blue font to view the network details. You can also configure the private IPv4 address for database access as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/9897">Connecting to TencentDB for Redis Instance</a>.</td></tr>
<tr>
<td><strong>Billing Mode</strong></td>
<td>Instance billing mode, which is pay-as-you-go. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/31954">Billing Overview</a>.</td></tr>
<tr>
<td><strong>Architecture</strong></td>
<td>Database version information and architecture. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/31959">Memory Edition (Standard Architecture)</a>.</td></tr>
<tr>
<td><strong>Instance Edition</strong></td>
<td>Currently, only <strong>Memory Edition</strong> is supported.</td></tr>
<tr>
<td><strong>Used/Total</strong></td>
<td>The instance's currently used memory and total memory.</td></tr>
<tr>
<td><strong>Creation Time</strong></td>
<td>Specific date and time of instance creation.</td></tr>
<tr>
<td><strong>Tag</strong></td>
<td>Instance tag information. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/46559">Editing Instance Tag</a>.</td></tr>
<tr>
<td><strong>Operation</strong></td>
<td><ul><li>You can click <b>Log In</b> to access the database in the DMS console as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/9897">Connecting to TencentDB for Redis Instance</a>.</li> 
<li>You can click <b>Configure</b> and then select an operation as needed. Specifically, you can select **Expand Node** or **Reduce Node** to expand or reduce the instance node memory, select **Add Replica** or **Delete Replica** to add or delete instance replicas, or select **Add Shard** or **Delete Shard** to add or delete shards in the cluster architecture respectively. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/239/31934">Changing Instance Specification</a>.</li>
<li>You can select <b>More > Performance/Security</b> to view the instance performance diagnosis report as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/47581">Overview</a>.</li><li>You can select <b>More > Security Group</b> to change security group inbound rules as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/31945">Configuring Security Group</a>.</li>
<li>For a pay-as-you-go instance, you can click <b>More > Terminate</b> to return it and isolate it into the recycle bin as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/31937">Terminating Instance</a>.</li>
<li>You can select <b>More > Edit Tag</b> to edit the instance tag keys and values as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/46559">Editing Instance Tag</a>.</li></ul></td></tr>
</tbody></table>

## Viewing Instance Details
In the **Instance ID/Name** column of the target instance, click the instance ID in blue font to enter the **Instance Details** page.
![](https://qcloudimg.tencent-cloud.cn/raw/05cd91bc77d6ceac2278223fd4b0d98e.png)

<table class="table-striped">
<tbody>
<tr><th>Section</th><th>Parameter</th><th>Description</th></tr>
<tr>
<td rowspan="6"><b>Basic Info</b></td>
<td>Instance Name</td>
<td>The instance name set during instance creation. You can hover over the instance name and click <img src="https://qcloudimg.tencent-cloud.cn/raw/c3386f46a3b0588a84b3c0bf6f952200.png" style="zoom:66%;" /> to rename the instance for easier identification and management.</td></tr>	
<tr>
<td>Instance ID</td>
<td>The instance's unique ID.</td></tr>
<tr>
<td>Instance Status</td><td>The instance's current status. The normal status is **Running**.</td></tr>
<tr>
<td>AZ</td><td>The region and AZ where the instance resides. If the instance is deployed in one single AZ, you can click <b>Upgrade to Support Multi-AZ Deployment</b> to upgrade it to a multi-AZ deployed instance as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/39982">Upgrading to Multi-AZ Deployment</a>.</td></tr>
<tr>
<td>Project</td><td>The project to which the instance belongs. You can click <b>Assign to Project</b> to assign the instance to another project as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/31933">Assigning Instance to Project</a>.</td></tr>
<tr>
<td>Read/Write Status</td><td>Current database read/write status.</td></tr>    
<tr>
<td rowspan="7"><b>Specs Info</b></td>
<td>Instance Edition</td><td>Currently, only Memory Edition is supported.</td></tr>
<tr>
<td>Compatible Version</td><td>Information of the version compatible with the Redis protocol. If <b>Upgrade Minor Version</b> is grayed out, the current version is the latest version. If it is in blue font, you can click it to upgrade to a later version and try out new features of the kernel as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/37710">Upgrading Instance Version</a>.</td></tr>
<tr>
<td>Proxy Version</td><td>Redis proxy version information. If <b>Upgrade Proxy</b> is grayed out, the proxy is already on the latest version. If it is in blue font, you can click it to upgrade to a later version as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/47582">Upgrading Proxy</a>.</td></tr>
<tr>
<td>Architecture</td><td>Instance deployment architecture information. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/31959">Memory Edition (Standard Architecture)</a>. If the instance is in standard architecture, you can click <b>Upgrade Architecture</b> to upgrade to the cluster architecture as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/37860">Upgrading Instance Architecture</a>.</td></tr>
<tr>
<td>Memory</td><td>The instance's current total memory, used memory, and memory utilization. You can click <b>Memory Analysis</b> to enter the **Memory Analysis** tab on the <b>Performance Optimization</b> page. You can view the memory overheads of big keys in the database there, so as to identify big keys quickly and then analyze, split, or clear them. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/47576">Memory Analysis</a>.</td></tr>  
<tr>
<td>Memory Configuration</td><td>The purchased instance memory specification, including number of shards and memory of each shard node. You can click <b>Configure</b> to adjust the instance's memory, number of shards, and number of replica nodes as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/31934">Changing Instance Specification</a>.</td></tr> 
<tr>
<td>Read-Only Replica</td><td>Read/write separation status.</td></tr> 
<tr>
<td rowspan="6"><b>Network Info</b></td>
<td>Network</td><td>Instance VPC name. You can click <b>Switch Network</b> to switch the VPC and subnet as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/31944">Configuring Network</a>. If needed, you can also create a VPC as instructed in <a href="https://intl.cloud.tencent.com/document/product/215/31805">Creating VPC</a>.</td></tr>
<tr>
<td>Subnet</td><td>AZ-specific subnet in the instance VPC. A VPC allows for subnets in different AZs, which communicate with each other over the private network by default.</td></tr>
<tr>
<td>Private IPv4 Address</td>
<td>The private IP address assigned to the database instance. You need to configure it for database access as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/9897">Connecting to TencentDB for Redis Instance</a>.</td></tr><tr>
<td>Public Network Address</td>
<td>Address for database access over the public network, which is disabled by default. You can click <b>Enable</b> to enable public network access for easier daily testing and management as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/43452">Configuring Public Network Address</a>.</td></tr>
<tr>
<td>Max Connections</td>
<td>The current maximum number of client connections allowed to the database.<li>You can click <b>Adjust</b> to adjust the value as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/47922">Adjusting the Number of Connections</a>.</li><li>You can also click <b>Real-Time Session</b> to view the instance's current statistics such as sources of real-time sessions and number of active connections. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/47578">Real-Time Session</a>.</li></td></tr><tr>
<td>Max Network Throughput</td>
<td>Maximum network throughput for database access, which is also the trigger threshold for inbound/outbound traffic throttling. You can click <b>Adjust Bandwidth</b> to increase the bandwidth as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/46560">Bandwidth Adjustment</a>.</td></tr>
<tr>
<td rowspan="5"><b>Configuration</b></td>
<td>Billing Mode</td><td>Instance billing mode, which is pay-as-you-go.</td></tr>
<tr>
<td>Creation Time</td><td>Instance creation time.</td></tr>
<tr>
<td>Maintenance Time</td><td>Instance maintenance time. To ensure the database stability, the backend system performs maintenance operations on the instance during the maintenance time. You can click <b>Modify</b> to adjust the maintenance time as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/46558">Setting Maintenance Time</a>. We recommend you set it to a time during off-peak hours.</td></tr>
<tr><td>Connection Password</td><td>The password configured for database connection. You can click <b>Reset Password</b> to reset the password as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/46557">Resetting Password</a>. You can set configure password exemption access.</td></tr></tr>
<tr>
<td>Tag</td><td>Tags associated with the instance. You can modify them as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/46559">Editing Instance Tag</a>.</td></tr>
<tr>
<td rowspan="6"><b>Data Sync</b></td>
<td>Sync Mode</td><td>The data sync mode currently used by the instance, such as DTS.</td></tr>
<tr>
<td>Sync Task</td><td>Sync task ID.</td></tr>
<tr><td>Sync Status</td><td>Task execution status.</td></tr>
<tr>
<td>Sync Delay</td><td>Number of data bytes delayed to be synced.</td></tr>
<tr><td>Instance Role</td><td>Instance role for data sync, which can be the source or target instance.</td></tr></tr>
<tr>
<td>Sync Instance</td><td>ID and name of the peer instance for data sync.</td></tr>
<tr>
<td rowspan="4"><b>Global Replication</b></td>
<td>Create or Join Global Replication Group</td>
<td>If the instance hasn't joined a global replication group, click <b>Create or Join Global Replication Group</b> to join a group as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/45603">Creating Global Replication Group</a>. Before doing so, you should understand <a href="https://intl.cloud.tencent.com/document/product/239/45602">how it works</a> and the <a href="https://intl.cloud.tencent.com/document/product/239/46563">use limits</a> first.</td></tr>
<tr>
<td>Replication Group ID</td><td>Global replication group ID. This parameter will be displayed after the instance joins a global replication group.</td></tr>
<tr>
<td>Replication Group Name</td><td>Custom name of the global replication group. This parameter will be displayed after the instance joins a global replication group.</td></tr>
<tr>
<td>Instance Role</td><td>The role assigned to the instance in the global replication group, which is either master or read-only instance. This parameter will be displayed after the instance joins a global replication group.</td></tr>
<tr>
<td><b>Architecture Diagram</b></td>
<td colspan="2">The database instance's deployment architecture diagram.</td></tr>
</tbody></table>

## More Operations
### Renaming an instance
1. In the **Instance List**, hover over the name of the target instance and click <img src="https://qcloudimg.tencent-cloud.cn/raw/c3386f46a3b0588a84b3c0bf6f952200.png" style="zoom:75%;" /> on the right.
2. In the instance name input box, enter a new name, which must meet the following requirements:
   - It can contain 1–60 characters.
   - It can contain letters, digits, underscores, and hyphens.
   - A letter, digit, or special symbol is counted as one character.

### Setting fields in the instance list
1. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/770577c6c61c1f3066210d6345e09b6f.png" style="zoom:67%;" /> in the top-right corner of the instance list.
2. On the **Display Settings** page, select the fields to be displayed.
3. Click **OK**, and you can see the set fields in the instance list.

### Exporting the instance list
You can click <img src="https://qcloudimg.tencent-cloud.cn/raw/99ee5bb1067d04d1661ef02be39e2caf.png" style="zoom:50%;" /> in the top-right corner of the instance list to export the entire list.

## Related APIs
| API | Description |
| ----------------- | ------------------------------------------------------------ |
| describeInstances | [Queries the list of instances](https://intl.cloud.tencent.com/document/product/239/32065). |

