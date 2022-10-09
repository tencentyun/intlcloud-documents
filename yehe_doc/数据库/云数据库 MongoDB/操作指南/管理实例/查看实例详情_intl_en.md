## Overview

After purchasing a TencentDB for MongoDB instance, you can quickly view its details in the console, such as the status, capacity usage, primary/secondary nodes in the cluster, and network status. You can also perform Ops and management operations efficiently.

## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The instance hasn't been terminated or isolated into the recycle bin. For more information, see [Recycle Bin](https://intl.cloud.tencent.com/document/product/240/44553).

## Viewing the Instance List

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
 - In the search box in the top-right corner, you can search for the target instance by instance ID, instance name, private IP, or tag key.
 - If you can't find the target instance in the instance list, select **Recycle Bin** on the left sidebar to check whether it is isolated there due to overdue payments. For more information, see [Recycle Bin](https://intl.cloud.tencent.com/document/product/240/44553).
5. View the target instance information, such as the status, specification, and storage engine.
![](https://qcloudimg.tencent-cloud.cn/raw/0ad37c4c3ebad3a061711bd0ff89579f.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td><strong>Instance ID/Name</strong></td>
<td><ul><li>Instance ID: The instance's unique ID.</li><li>Name: Instance name set during instance creation. You can hover over the instance name and click <img src="https://qcloudimg.tencent-cloud.cn/raw/c3386f46a3b0588a84b3c0bf6f952200.png" style="zoom:66%;"> to rename the instance for easier identification and management.</li></ul></td></tr>
<tr>
<td><strong>Monitoring/Status</strong></td>
<td><ul><li>Monitoring: You can click <img src="https://qcloudimg.tencent-cloud.cn/raw/fdc8f6a0ee6697f45d2497b1a0551f45.png" style="zoom:50%;"> to enter the monitoring panel and view the instance monitoring data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/3564">Viewing Monitoring Data</a>.</li><li>Status: Instance status. The normal status is <b>Running</b>. If a task is being executed in the instance, the task name, such as **Changing configuration**, will be displayed here.</li></ul></td></tr>
<tr>
<td><strong>Configure/Network</strong></td>
<td><ul><li>Configure: The specification configuration of each instance node.</li><li>Replica set: Memory and disk capacity.</li><li>Sharded cluster instance: Memory and disk capacity * shard quantity.</li><li>Network: The network information of the instance.</li></ul></td></tr>
<tr>
<td><strong>Version and Engine</strong></td>
<td><ul><li>Database version information. Supported versions include 4.4, 4.2, 4.0, 3.6, and 3.2. v3.2 is no longer purchasable.</li><li>Storage engine: It is WiredTiger by default.</li></ul></td></tr>
<tr>
<td><strong>Private Network Address</strong></td>
<td>The private IPv4 address and port of all primary and secondary mongod nodes in the TencentDB instance. A TencentDB instance can be accessed only over the private network. When using MongoDB Shell for access, you need to configure the private IP and port. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/240/7092">Connecting to TencentDB for MongoDB Instance</a>.</td></tr>
<tr>
<td><strong>Billing Mode</strong></td>
<td>Instance billing mode, which is pay-as-you-go. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/3550">Billing Overview</a>.</td></tr>
<tr>
<td><strong>Used/Total</strong></td>
<td>The used/total memory of the instance. This parameter helps you quickly check the memory utilization of the current instance.</td></tr>
<tr>
<td><strong>Oplog/Shard Info</strong></td>
<td>You can click <b>View/Adjust</b> to view the capacity reserved for oplog or adjust it based on your business needs. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/240/49158">Adjusting Oplog Capacity</a>.</td></tr>
<tr>
<td><strong>Project</strong></td>
<td>Instance project. You can view the information of all instances in this project. You can also move the instance to another project as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31189">Specifying Project for Instance</a>.</td></tr>
<tr>
<td><strong>Protocol</strong></td>
<td>It is fixed at <b>MongoDB protocol</b>.</td></tr>
<tr>
<td><strong>Operation</strong></td>
<td><ul>
<li>Select <b>Adjust Configuration > Adjust Configuration</b> to adjust the instance's memory and disk capacity as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31192">Adjusting Instance Specification</a>.</li>
<li>Select <b>Adjust Configuration > Node Management</b> to manage the mongod and mongos nodes of the instance as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/49134">Viewing Node Information</a>.</li>
<li>Select <b>More > Security Group</b> to change security group inbound rules.</li>  
<li>Select <b>More > Restart</b> to restart the instance as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31188">Restarting Instance</a>.</li> 
For a pay-as-you-go instance, you can select <b>More > Terminate</b> to return it and isolate it into the recycle bin as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31485">Terminating Instance</a>.</li> 
<li>Select <b>More > Manage</b> to view the instance details. </li><li>Select <b>More > Edit Tag</b> to edit the instance tag keys and values as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/44546">Editing Instance Tag</a>.</li></ul></td></tr>
</tbody></table>

## Viewing Instance Details
In the **Instance ID/Name** column of the target instance, click the instance ID to enter the **Instance Details** page.

<table class="table-striped">
<tbody>
<thead><tr><th>Section</th><th>Parameter</th><th>Description</th></tr></thead>
<tr>
<td rowspan="5"><b>Basic Info</b></td>
<td>Instance Name</td>
<td>Custom instance name.</td></tr>	
<tr>
<td>Instance ID</td>
<td>The instance's unique ID.</td></tr>
<tr>
<td>Instance Status</td><td>The instance's current status. The normal status is **Running**.</td></tr>
<tr>
<td>Region</td><td>Instance region and AZ. You can click <b>Modify AZs</b> to switch to another AZ in the same region. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44182">Modifying Instance AZ</a>.</td></tr>
<tr>
<td>Project</td><td>The project to which the instance belongs. You can click <b>Switch to Another Project</b> to assign the instance to another project as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31189">Specifying Project for Instance</a>.</td></tr>
<tr>
<td rowspan="6"><b>Specs Info</b></td>
<td>Instance Type</td><td>You can set the instance cluster architecture type to **Replica Set** or **Sharded Cluster**. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44173">System Architecture</a>.</td></tr>
<tr>
<td>Configuration Type</td><td>It is fixed at **Ten-Gigabit High IO**.</td></tr>
<tr>
<td>Version and Engine</td><td>The version and the storage engine of the instance. If the current version is 3.6, you can click <b>Upgrade to v4.0</b> to upgrade to v4.0. If the current version is 4.0, you can click <b>Upgrade to v4.2</b> to upgrade to v4.2. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/240/47677">Version Upgrade</a>.</td></tr>
<tr>
<td>Mongod Node Specification</td><td>The specification configuration information of a single mongod node, including the CPU core quantity, memory, disk capacity, and node quantity. For the detailed specifications supported by replica set and sharded cluster instances, see <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>.</td></tr>
<tr>
<td>Mongos Node Specification</td><td>The specification configuration information of a single mongos node, including the CPU core quantity, memory, and node quantity. For the detailed specifications supported by replica set and sharded cluster instances, see <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>.</td></tr>  
<tr>
<td>Disk Capacity</td><td>The total disk capacity of the instance.</td></tr> 
<tr>
<td rowspan="5"><b>Configuration</b></td>
<td>Billing Mode</td><td>Instance billing mode, which is pay-as-you-go.</td></tr>
<tr>
<td>Creation Time</td><td>Instance creation time.</td></tr>
<tr>
<td>Maintenance Time</td><td>Instance maintenance time. To ensure the database stability, the backend system performs maintenance operations on the instance during the maintenance time. You can click <b>Modify</b> to adjust the maintenance time as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31190">Setting Instance Maintenance Time</a>. We recommend you set it to a time during off-peak hours.</td></tr>
<tr><td>Auth-Free Access</td><td>You can view whether auth-free access to databases is enabled. If the status is <b>Not enabled yet</b>, you can click **Enable** to enable this feature as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/39007">Accessing Instance Without Authentication</a>.</td></tr></tr>
<tr>
<td>Tag</td><td>Tags associated with the instance. You can modify them as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/44546">Editing Instance Tag</a>.</td></tr>
<tr>
<td rowspan="4"><b>Network Configuration</b></td>
<td>Network</td><td>Instance VPC name. You can click <b>Switch Network</b> to switch the VPC and subnet as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/44180">Switching Instance Network</a>. If needed, you can also create a VPC as instructed in <a href="https://intl.cloud.tencent.com/document/product/215/31805">Creating VPC</a>.</td></tr>
<tr>
<td>Subnet</td><td>AZ-specific subnet in the instance VPC. A VPC allows for subnets in different AZs, which can communicate with each other over the private network by default. After you <a href="https://intl.cloud.tencent.com/document/product/240/44182">modify the instance AZ</a>, we recommend you also switch the subnet to reduce the access latency.</td></tr>
<tr>
<td>Connection Type</td>
<td>The node type for database access.<ul><li><b>Access Read-Write Primary Node</b>: The database will be accessed on the primary node of the instance. The primary node can be read and written.</li><li><b>Only read read-only node</b>: The database will be accessed only on a read-only node. If you didn't configure read-only nodes during instance creation, this parameter won't be displayed.</li><li><b>Only read secondary node</b>: The database will be accessed only on a replica node.</li><li><b>Only read secondary node and read-only node</b>: The database will be accessed on a secondary node preferentially. If all secondary nodes are abnormal, the database will be accessed on a read-only node.</li></ul></td></tr>
<tr><td>Access address (connection string)</td><td>The URI connection string of each connection type. You can directly copy a string to access the database as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/7092">Connecting to TencentDB for MongoDB Instance</a>.</td></tr>
</tbody></table>

## More Operations
### Renaming an instance
1. In the [instance list](https://console.cloud.tencent.com/mongodb), hover over the instance name to be modified and click <img src="https://qcloudimg.tencent-cloud.cn/raw/c3386f46a3b0588a84b3c0bf6f952200.png" style="zoom:66%;" /> on the right.
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

| API                                                 | Description |
| ------------------------------------------------------------ | -------------------- |
| [DescribeDBInstances](https://Intl.cloud.tencent.com/document/product/240/34702) | Queries the list of TencentDB instances |
| [RenameInstance](https://intl.cloud.tencent.com/document/product/240/34697) | Renames instance         |

