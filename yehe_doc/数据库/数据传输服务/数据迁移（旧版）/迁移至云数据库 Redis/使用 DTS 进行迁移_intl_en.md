## Background Overview
[DTS](https://intl.cloud.tencent.com/document/product/571) is a data transmission service that integrates such features as data migration, sync, and subscription. It helps you migrate your databases to the cloud without interrupting your business and build a high-availability database disaster recovery architecture through real-time sync channels. Its data subscription feature meets your requirements for commercial data mining and async business decoupling. 

DTS for Redis currently supports the data migration feature for you to migrate data to TencentDB in a non-stop manner at a time. In addition, in its full + incremental data migration mode, historical data in the source database written before migration and incremental data written during migration can be migrated together. 

## Use Cases

DTS for Redis data migration supports source and target databases in the following deployment modes:

| Source Database                                            | Target Database       | Description                                                         |
| ----------------------------------------------- | ------------ | ------------------------------------------------------------ |
| Self-built Redis database, such as self-built databases in IDC and CVM | TencentDB for Redis | -                                                            |
| Third-party Redis                              | TencentDB for Redis | The third-party cloud vendor must grant the `SYNC` or `PSYNC` command permission.            |
| TencentDB for Redis                                    | TencentDB for Redis | Data migration, version upgrade, and cross-region migration are supported between database instances under the same Tencent Cloud account. |

## Migration Support Description
>?For compatibility issues with migration from Standalone Edition to Memory Edition (Cluster Architecture), see [Check on Migration from Standard Architecture to Cluster Architecture](https://intl.cloud.tencent.com/document/product/239/37594).

#### Supported versions
- DTS supports Redis 2.8, 3.0, 3.2, 4.0, 5.0, and 6.0. To use it for v6.0, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. We recommend you migrate from an earlier version to a later version; otherwise, compatibility problems may occur.
- Standard architecture and cluster architecture instances can be migrated to each other; however, such heterogeneous migration may has compatibility problems.
- Supported architectures include single-node, Redis cluster, Codis, and twemproxy.
- Migration permission requirements: To migrate data through DTS, the source instance must support `SYNC` or `PSYNC` commands.

#### Supported networks
DTS supports data migration based on the public network, CVM instances, Direct Connect gateways, VPN, and CCN.

- Public Network: The source database can be accessed through a public IP.
- Self-Build on CVM: The source database is deployed in a [CVM](https://intl.cloud.tencent.com/document/product/213) instance.
- Direct Connect: The source database can be interconnected with VPCs through [Direct Connect](https://intl.cloud.tencent.com/document/product/216). 
- VPN Access: The source database can be interconnected with VPCs through [VPN Connections](https://intl.cloud.tencent.com/document/product/1037). 
- CCN: The source database can be interconnected with VPCs through [CCN](https://intl.cloud.tencent.com/document/product/1003).

#### Limitations
- To ensure migration efficiency, cross-region migration of CVM-based self-built instances is not supported.
- To migrate instances over the public network, make sure that the source instance can be accessed over the public network.
- Only instances that are running normally can be migrated, while instances with no password initialized or with ongoing tasks cannot.
- The target instance must be empty. During the migration process, the target instance will be read-only and cannot be written to.
- After the successfully migrated data is verified by your business, you can disconnect the source instance and connect to the target instance.

## Environment Requirements
### System check
> ?The DTS system will check the following environment requirements before starting a migration task and report an error if a requirement is not met. You can also check them in advance. For more information on error handling, see [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551).

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<li>The source and target databases can be connected.</li><li>The number of databases in the source database must be less than or equal to that in the target database.</li><li>The source instance must be on v2.2.6 or later.</li><li>The source database must be a replica node.</li></td></tr>
<tr> 
<td>Requirements for target database</td>
<td>
<li>The target database version must be later than or equal to the source instance version; otherwise, an alarm will be triggered for compatibility problems during verification.</li><li>The target database must have the latest proxy.</li>
<li>The space of the target database must be at least 1.5 times the volume of the data to be migrated in the source database.</li>
<li>The target database must be empty.</li></td></tr>
</table>

### [Manual check](id:zxjc)
You should check and make sure that the following items are passed before the migration; otherwise, the migration may fail.

#### Big keys in the source database
Before the migration, check whether there are big keys in the source database. They may cause the buffer (client-output-buffer-limit) to overflow during the migration, leading to a migration failure.
- For TencentDB databases, you can use the performance optimization feature of TencentDB for DBbrain to quickly analyze big keys. For more information, see [Memory Analysis](https://intl.cloud.tencent.com/document/product/239/47576).
- For non-TencentDB databases, use RDBTools to analyze big keys in Redis.

Evaluate large keys for splitting or cleaning. If you need to retain them, set the source buffer size (client-output-buffer-limit) to infinite.
```
config set client-output-buffer-limit 'slave 0 0 0' 
```

#### Limit on the number of TCP connections in the source Linux kernel
If the number of concurrent business requests is high, check the limit on the number of connections in the Linux kernel before the migration. If this value is exceeded, the Linux server will actively disconnect from DTS.
```
echo "net.ipv4.tcp_max_syn_backlog=4096" >> /etc/sysctl.conf
echo "net.core.somaxconn=4096" >> /etc/sysctl.conf
echo "net.ipv4.tcp_abort_on_overflow=0" /etc/sysctl.conf
sysctl -p
```

#### Access permission of the source RDB file directory
Before the migration, check and make sure that the directory where RDB files are stored in the source database is readable; otherwise, the migration will fail.

If the RDB file directory is not readable, run the following command in the source database to set "diskless replication". Then, RDB files will be directly sent to DTS for storage, with no need to be stored in the source database first and then sent. 
```
config set repl-diskless-sync yes
```

#### Command compatibility (for migration from standard architecture to cluster architecture)
The most challenging problem in migrating data from Standard Edition to Memory Edition (Cluster Architecture) is the command compatibility with usage specifications of Memory Edition (Cluster Architecture).

- Multi-key operations
  TencentDB for Redis Memory Edition (Cluster Architecture) only supports cross-slot multi-key access for `mget`, `mset`, `del`, and `exists` commands. In the source database, keys that need to engage in multi-key computing can be aggregated into the same slot through a hash tag. For more information on how to use hash tags, see [Redis cluster specification](https://redis.io/topics/cluster-spec). 
- Transactional operations
  Memory Edition (Cluster Architecture) supports transactions, but cross-slot access to keys in transactions is not supported.

Perform static and dynamic evaluations as instructed in [Check on Migration from Standard Architecture to Cluster Architecture](https://intl.cloud.tencent.com/document/product/239/37594).

## Migration Directions
#### 1. Create a migration task
(1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
(2) On the **Create Migration Task** page, select the types and regions of the source and target databases and click **Buy Now**.

#### 2. Set source and target databases
Configure the **Source Database Settings** and **Target Database Settings** and click **Test Connectivity**. After the test is passed, click **Save** to proceed to the next step.
![](https://main.qcloudimg.com/raw/c08aad1d17a1cc39b1ae4cf978c4194b.png)

<table>
<thead><tr><th width="10%">Setting Type</th><th width="20%">Configuration Item</th><th width="70%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a task name that is easy to identify.</td></tr>
<tr>
<td>Running Mode</td>
<td>You can set **Immediate execution** or **Scheduled execution**.<ul><li>If a scheduled task is modified and passes verification, you need to click <b>Scheduled start</b> again to make the task start at the scheduled time.</li><li>If the specified time has passed, the task will be started immediately. You can also click <b>Immediate start</b> to start the task immediately.
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
<td>Access Type</td><td>For a third-party cloud database, you can select **Public Network** generally or select **VPN Access**, **Direct Connect**, or **CCN** based on your actual network conditions.<br>In this scenario, select **Direct Connect** or **VPN Access**. You need to <a href="https://intl.cloud.tencent.com/document/product/571/42651">configure VPN-IDC interconnection</a> in this scenario. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.
<ul><li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li>
<tr>
<td>VPC-based Direct Connect Gateway</td><td>Only VPC-based Direct Connect gateway is supported. Confirm the network type associated with the gateway.</td></tr>
<tr>
<td>VPC</td><td>Select a VPC and subnet associated with the VPC-based Direct Connect gateway.</td></tr>
<tr>
<td>Node Type</td><td>**Single-Node Migration** and **Cluster Migration** are supported. **Cluster Migration** is used as an example here.<br>Currently, there are no limits on the number of shards and replicas in migration from Cluster Edition Redis to Cluster Edition Redis.</td></tr>
<tr>
<td>Node Info</td><td>Enter the addresses and passwords (IP:port:password or IP:port) of all shards of the source database cluster and separate the information of different nodes with line breaks.<br>We strongly recommend you migrate data from a replica node of the source database to avoid any impact on business access to the source database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, select **Database**.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
</tbody></table>

#### 3. Verify and start the task
On the task verification page, verify the task. After the verification is passed, click **Start Task**.

- Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.  
- Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.

Return to the data migration task list, and you can see that the task has entered the **Preparing** status. After 1–2 minutes, the data migration task will be started.

#### 4. Complete the migration task 
(1) (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637).
(2) If the keys of the source and target databases are the same, click **Done** in the **Operation** column to stop the data migration task.
(3) After the migration task status becomes **Task successful**, verify the data in the target database. If the verification is passed, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).

## Event Alarming and Metric Monitoring
(1) DTS can automatically report event alarms triggered upon migration interruption to keep you informed of any exceptions. For detailed directions, see [Configuring Alarm Policy for Data Migration](https://intl.cloud.tencent.com/document/product/571/42610).
(2) DTS allows you to view the monitoring data of various metrics during migration to understand the performance metrics of the system. For more information, see [Viewing Monitoring Metric](https://intl.cloud.tencent.com/document/product/571/42606).


