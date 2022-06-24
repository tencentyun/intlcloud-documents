## Background Overview
Tencent Cloud [Data Transmission Service (DTS)](https://cloud.tencent.com/document/product/571) is a data transmission service that integrates such features as data migration, sync, and subscription. It helps you migrate your databases to the cloud without interrupting your business and build a high-availability database disaster recovery architecture through real-time sync channels. Its data subscription feature meets your requirements for commercial data mining and async business decoupling. 

DTS for Redis currently supports the data migration feature for you to migrate data to TencentDB in a non-stop manner at a time. In addition, in its full + incremental data migration mode, historical data in the source database written before migration and incremental data written during migration can be migrated together. 

## Use Cases

DTS for Redis data migration supports source and target databases in the following deployment modes:

| Source Database                                            | Target Database       | Description                                                         |
| ----------------------------------------------- | ------------ | ------------------------------------------------------------ |
| Self-built Redis database, such as self-built databases in IDC and CVM | TencentDB for Redis | -                                                            |
| Third-party Redis                              | TencentDB for Redis | The third-party cloud vendor should grant the `SYNC` or `PSYNC` command permission.            |
| TencentDB for Redis                                    | TencentDB for Redis | Data migration, version upgrade, and cross-region migration are supported between database instances under the same Tencent Cloud account. |

## Migration Support Description
>?For compatibility issues with migration from Standalone Edition to Memory Edition (Cluster Architecture), see [Check on Migration from Standard Architecture to Cluster Architecture](https://intl.cloud.tencent.com/document/product/239/37594).

#### Supported versions
- DTS supports Redis 2.8, 3.0, 3.2, 4.0, and 5.0. We recommend you migrate from an earlier version to a later version; otherwise, compatibility problems may occur.
- Standard architecture and cluster architecture instances can be migrated to each other; however, such heterogeneous migration may has compatibility problems.
- Supported architectures include single-node, Redis cluster, Codis, and twemproxy.
- Migration permission requirements: To migrate data through DTS, the source instance must support `SYNC` or `PSYNC` commands.

#### Supported networks
DTS supports data migration based on the public network, CVM instances, Direct Connect gateways, VPN gateways, and CCN.

- Public Network: The source database can be accessed through a public IP.

- Self-Build on CVM: The source database is deployed in a [CVM](https://intl.cloud.tencent.com/document/product/213) instance.

- Direct Connect: The source database can be interconnected with VPCs through [Direct Connect](https://intl.cloud.tencent.com/document/product/216). 

- VPN Access: The source database can be interconnected with VPCs through [VPN Connections](https://intl.cloud.tencent.com/document/product/1037). 

- CCN: The source database can be interconnected with VPCs through [CCN](https://intl.cloud.tencent.com/document/product/1003).

#### Limitations
- To ensure migration efficiency, cross-region migration of CVM-based self-built instances is not supported.
- To migrate instances over a public network, make sure that the source instance can be accessed over the public network.
- Only instances that are running normally can be migrated, while instances with no password initialized or with ongoing tasks cannot.
- The target instance must be empty. During the migration process, the target instance will be read-only and cannot be written to.
- After the successfully migrated data is verified by your business, you can disconnect the source instance and connect to the target instance.

## Environment Requirements

> ?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. You can also check them in advance.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<li>The source and target databases can be connected.</li><li>The number of databases in the source database must be less than or equal to that in the target database.</li></td></tr>
<tr> 
<td>Requirements for target database</td>
<td>
<li>The target database version should be later than or equal to the source database version; otherwise, an alarm will be triggered for compatibility problems during verification.</li>
<li>The space of the target database must be larger than the volume of the data to be migrated in the source database.</li>
<li>The target database must be empty.</li></td></tr>
</table>

## Migration Directions

#### 1. Create a migration task
(1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
(2) On the **Create Migration Task** page, select the types and regions of the source and target databases and click **Buy Now**.

#### 2. Set the source and target databases

Configure the **Source Database Settings** and **Target Database Settings** and click **Test Connectivity**. After the test is passed, click **Save** to proceed to the next step.

![](https://main.qcloudimg.com/raw/513d89660769db2dfd155514bcb38dfc.png)

<table>
<thead><tr><th width="10%">Setting Type</th><th width="20%">Configuration Item</th><th width="70%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td>You can set <b>Immediate execution</b> or <b>Scheduled execution</b>.<ul><li>If a scheduled task is modified and passes verification, you need to click <b>Scheduled start</b> again to make the task start at the scheduled time.</li><li>If the specified time has passed, the task will be started immediately. You can also click <b>Immediate start</b> to start the task immediately.
</li></ul></td></tr>
<tr>
<td>Tag</td>
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=7>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>For a third-party cloud database, you can select <b>Public Network</b> generally or select <b>VPN Access</b>, <b>Direct Connect</b>, or <b>CCN</b> based on your actual network conditions.<br>In this scenario, select <b>Direct Connect</b> or <b>VPN Access</b> You need to <a href="https://intl.cloud.tencent.com/document/product/571/42651">configure VPN-IDC interconnection</a> in this scenario. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.
<ul><li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li></ul></td></tr>
<tr>
<td>VPC-based Direct Connect Gateway</td><td>Only VPC-based Direct Connect gateway is supported. Confirm the network type associated with the gateway.</td></tr>
<tr>
<td>VPC</td><td>Select a VPC and subnet associated with the VPC-based Direct Connect gateway.</td></tr>
<tr>
<td>Node Type</td><td><b>Single-Node Migration</b> and <b>Cluster Migration</b> are supported. <b>Cluster Migration</b> is used as an example here.<br>Currently, there are no limits on the number of shards and replicas in migration from Cluster Edition Redis to Cluster Edition Redis.</td></tr>
<tr>
<td>Node Info</td><td>Enter the addresses and passwords (IP:port:password or IP:port) of all shards of the source database cluster and separate the information of different nodes with line breaks.<br>We strongly recommend you migrate data from a replica node of the source database to avoid any impact on business access to the source database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this scenario, select <b>Database</b>.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
</tbody></table>


#### 3. Verify and start the task

On the task verification page, verify the task. After the verification is passed, click **Start Task**.

- Failed: It indicates that a check item failed and the task is blocked. You need to fix the problem and run the verification task again.  
- Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.

Return to the data migration task list, and you can see that the task has entered the **Preparing** status. After 1–2 minutes, the data migration task will be started.

#### 4. Complete the migration task 

(1) (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637).

(2) If the keys of the source and target databases are the same, click **Done** in the **Operation** column to stop the data migration task.

(3) After the migration task status becomes **Task successful**, verify the data in the target database. If the verification is passed, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).

## Event Alarming and Metric Monitoring

(1) DTS can automatically report event alarms triggered upon migration interruption to keep you informed of any exceptions. For detailed directions, see [Configuring Alarm Policy for Data Migration](https://intl.cloud.tencent.com/document/product/571/42610).
(2) DTS allows you to view the monitoring data of various metrics during migration to understand the performance metrics of the system. For more information, see [Viewing Monitoring Metric](https://intl.cloud.tencent.com/document/product/571/42606).


