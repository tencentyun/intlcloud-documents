## DTS Overview
Tencent Cloud Data Transmission Service (DTS) is a data transmission service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs. Currently, DTS for Redis supports data migration on different versions of Redis and in various network scenarios.

| Term | Description |
|---------|---------|
| Source instance | Source instance to be migrated. |
| Target instance | Target instance to be migrated to, i.e., user-purchased TencentDB for Redis. |
| CVM-based external instance | Redis service you deploy on a CVM instance. |
| Public network-based external instance | Redis service you deploy over a public network. |

## Migration Support Description
>?For more information on compatibility requirements for migration from standalone edition to memory edition (cluster architecture), please see [Notes on Migration from Standalone Edition to Cluster Edition](https://intl.cloud.tencent.com/document/product/239/37594).

#### Supported features
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync to the cloud by combining full migration and incremental sync.

#### Supported versions
- DTS supports Redis 2.8, 3.0, 3.2, 4.0, and 5.0.
- DTS supports single-node, Redis cluster, Codis, and twemproxy architectures.
- Migration permission requirements: to migrate data via DTS, the source instance must support SYNC or PSYNC commands.

#### Supported networks
DTS supports data migration and data sync based on the public network, CVM instances, Direct Connect gateways, VPN gateways, and CCN.

#### Supported scenarios
- Migration to cloud: DTS enables you to migrate your Redis instance in a traditional IDC to TencentDB for Redis, helping you migrate your business to the cloud efficiently and conveniently.
- External cloud service migration: DTS enables you to migrate your Redis service created with a virtual machine on Tencent Cloud or other clouds to Tencent Cloud.
- Migration of Redis data from other cloud vendors: DTS enables you to migrate Redis data from other cloud vendors to Tencent Cloud, provided that cloud vendors have granted the SYNC or PSYNC command permission.
- Migration between Tencent Cloud instances: DTS supports data migration or real-time data sync between instances on Tencent Cloud. The supported versions are as follows:
  
<table>
<caption></caption>
<tr>
<th style="width:130px;position:relative;text-align:left;padding:5px px;font-weight:00;" valign="top">
<div style="position:absolute;width:1px;height:140px;top:0;left:0;background-color: #d9d9d9;display:block;transform:rotate(-66deg);transform-origin:top;valign=top;"></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Target Instance<br>Source Instance
</th>
</div>
</th>
<th style="background-color:#f2f2f2;">2.8 Memory Edition (standard architecture)</th>
<th style="background-color:#f2f2f2;">4.0 Memory Edition (standard architecture)</th>
<th style="background-color:#f2f2f2;">4.0 Memory Edition (cluster architecture)</th>
<th style="background-color:#f2f2f2;">5.0 Memory Edition (standard architecture)</th>
<th style="background-color:#f2f2f2;">5.0 Memory Edition (cluster architecture)</th>
</tr>
<tr>
<td style="background-color:#f2f2f2;">2.8 Memory Edition (standard architecture)</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">4.0 Memory Edition (standard architecture)</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">4.0 Memory Edition (cluster architecture)</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">5.0 Memory Edition (standard architecture)</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">5.0 Memory Edition (cluster architecture)</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
</table>

#### Limitations
- To ensure migration efficiency, cross-region migration is not supported for CVM-based external instances.
- To migrate instances over a public network, make sure that the source instance can be accessed from the public network.
- Only instances that are running normally can be migrated, while instances with no password initialized or with ongoing tasks cannot be migrated.
- The target instance must be empty. During the migration process, the target instance will be read-only and cannot be written to.
- After the successfully migrated data is verified by your business, you can disconnect the source instance and connect to the target instance.

## Migration Process
### 1. Create a migration task
1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
2) Select the corresponding region in the “Linkage Region” section and click **Free Trial**.

### 2. Configure the task
- Task name: specify a name for the task.
- Scheduled execution: specify the start time of the migration task.
>?
> - To modify the scheduled task, you must click **Scheduled start** again after the verification is passed, so as to make the task start at the specified time.
> - If the specified time has passed, the task will be started immediately. You can also click **Immediate start** to start the task immediately.

### 3. Set the source instance and target instance
Redis instances on CVM are used here as an example, and the same is true for migration of instances over a public network.

| Field | Description | Remarks | Required |
|---------|---------|---------|---------|
| Task name | Name of the migration task | Used by users for task management | Yes |
| CVM instance (instance ID/private IP) | The ID and private IP of the CVM instance where the source Redis instance resides | The migration task checks the CVM running conditions and the CVM private IP based on the CVM instance ID | Yes |
| Port | Source instance port number | The migration task will access the source instance service | Yes |
| Password | Source instance password | The password is used for the authentication for accessing the source instance | No |
| TencentDB instance ID | Target instance ID | Data is synchronized to the target instance | Yes |

**Notes on migration of the cluster edition**
DTS supports the migration of the Redis Cluster Edition. For cluster schemes with the Redis Cluster, Codis, or twemproxy architecture, you only need to enter the addresses and passwords of all shard nodes of the source cluster as the node information when creating the migration task. We strongly recommend that you migrate data from a replica node of the source instance (from a node) to avoid any impact on business access to the source instance. DTS supports password-free migration. Possible information entered for migration is shown below:
![](https://main.qcloudimg.com/raw/c08aad1d17a1cc39b1ae4cf978c4194b.png)

### 4. Start the migration task
1) After the network connectivity test is successful, click **Save**.
2) DTS begins to verify the migration task, and once the migration requirements are met, the migration task will start.
3) After the task starts, the task status will switch to **Checking**, indicating that another round of parameter verification is underway. During this process, you can only cancel or view the task or check the verification progress.
4) After parameter verification is successful, data migration will start.
During data sync, changes in data offset, source instance, and target instance key will be displayed.

### 5. Configure a migration alarm
DTS supports migration interruption alarming to inform you of any exceptions. You can configure a migration alarm with the following steps:
1) Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/policylist) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2) Click **Create** to create an alarm policy.
 - Policy type: select **Data Transmission Service** > **Data Migrate**.
 - Alarm object: select the DTS task to be monitored and configure the **Trigger Condition** and **Alarm Object** to finish alarm configuration.
![](https://main.qcloudimg.com/raw/7b3769a436ce417c9ff6b34c9b56eb4d.png)

### 6. Complete the migration task 
Before disabling data sync, you can verify data on the target instance. If everything is correct, the migration task can be completed.
If the keys of the source instance and the target instance are identical, click **Complete** to finish data sync.

