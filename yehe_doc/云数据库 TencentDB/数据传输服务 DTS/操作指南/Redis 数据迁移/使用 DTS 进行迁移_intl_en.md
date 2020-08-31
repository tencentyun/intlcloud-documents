## DTS Overview
Tencent Cloud Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs. Currently, DTS for Redis supports data migration on different versions of Redis and in various network scenarios.

| Term | Description |
|---------|---------|
| Source instance | Source instance of the migration. |
| Target instance | Target instance to be migrated to, i.e., user-purchased TencentDB for Redis. |
| Self-built instance on CVM | Redis service deployed on a CVM instance. |
| Self-built instance on public network | Redis service deployed on a public network. |

## Migration Support Description
>?For more information on compatibility requirements for migration from standalone edition to memory edition (cluster architecture), please see [Notes on Migration from Standalone Edition to Cluster Edition](https://intl.cloud.tencent.com/document/product/239/35954).

#### Supported features
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync with the cloud by combining full migration and incremental sync.

#### Supported versions
- DTS supports Redis 2.8, 3.0, 3.2, 4.0, and 5.0.
- DTS supports single-node, Redis cluster, Codis, and twemproxy architectures.
- Migration permission requirements: to migrate data via DTS, the source instance must support SYNC or PSYNC commands.

#### Supported networks
DTS supports data migration and data sync across a public network, CVM-created instances, Direct Connect gateways, VPN gateways, and CCN.

#### Supported scenarios
- Cloudification migration: DTS supports migrating your Redis instance in a traditional IDC to TencentDB for Redis, moving your businesses to the cloud in an efficient and convenient manner.
- Self-built service migration: DTS supports migrating your Redis service created with a virtual machine in Tencent Cloud or other clouds to TencentDB for Redis.
- Migration of Redis data from other cloud vendors: DTS supports migrating Redis data from other cloud vendors to Tencent Cloud provided that the SYNC or PSYNC command permission has been granted.
- Migration between instances on Tencent Cloud: DTS supports data migration or real-time sync between instances on Tencent Cloud. The supported versions are as follows:   
<table>
    <caption></caption>
    <tr>
<th style ="width:130px;position:relative;text-align:left;padding:5px px;font-weight:00;" valign="top" ><div style="position:absolute;width:1px;height:140px;top:0;left:0;background-color: #d9d9d9;display:block;transform:rotate(-66deg);transform-origin:top;valign=top;"></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Target Instance<br>Source Instance</th>
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
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td style="background-color:#f2f2f2;">4.0 Memory Edition (standard architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td style="background-color:#f2f2f2;">4.0 Memory Edition (cluster architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
	<tr>
    <td style="background-color:#f2f2f2;">5.0 Memory Edition (standard architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
	 <td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td style="background-color:#f2f2f2;">5.0 Memory Edition (cluster architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    </table>

#### Migration limitations
- To ensure migration efficiency, cross-region migration is not supported for self-built instances on CVM.
- To migrate instances over a public network, make sure that the source instance is accessible from the public network.
- Only instances that are running normally can be migrated, while instances with no password initialized or with ongoing tasks cannot be migrated.
- The target instance must be empty with no data. During the migration process, the target instance will be read-only and cannot be written to.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the destination instance.

## Migration Process
### 1. Create a migration task
1) Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew), go to the **Data Migration** page, and click **Create Migration Task**.
2) Select the corresponding region in the "Linkage Region" section and click **Buy at 0 USD**.

### 2. Configure the task
- Task name: specify a name for the task.
- Scheduled execution: specify the start time of the migration task.
>?
> - To modify the scheduled task, you must click **Scheduled start** again after the verification is passed, so as to make the task start at the specified time.
> - If the specified time has passed, the task will start immediately. You can also click **Immediate start** to start the task immediately.

### 3. Set the source instance and target instance
Redis instances on CVM are used here as an example, and the same is true for migration of instances over a public network.

| Field | Description | Remarks | Required |
|---------|---------|---------|---------|
| Task name | Name of the migration task | Used by users for their management of tasks | Yes |
| CVM instance ID | ID of the CVM instance where the source Redis instance resides | The migration task checks the CVM running conditions based on the CVM instance ID | Yes |
| CVM private IP | Private IP of the CVM instance where the source Redis instance resides | The migration task checks the CVM private IP | Yes |
| Port | Port number of source instance | The migration task will access the source instance service | Yes |
| Password | Source instance password | The password is used for the authentication for accessing the source instance | No |
| Instance ID | Target instance ID | Data is synchronized to the target instance | Yes |

**Notes on migration in the cluster edition**
DTS supports migration in the Redis Cluster Edition. For cluster schemes with the Redis Cluster, Codis, or twemproxy architecture, simply enter the addresses and passwords of all shard nodes of the source cluster as the node information when creating the task. It is strongly recommended to perform data migration from a replica node (slave) of the source instance to avoid any impact on business access to the source instance. DTS supports password-free migration. The following is an example for entering relevant information for migration:
![](https://main.qcloudimg.com/raw/c08aad1d17a1cc39b1ae4cf978c4194b.png)

### 4. Start the migration task
1) After the network connectivity test is successful, click **Save**.
2) DTS begins to verify the migration task, and once the migration requirements are met, the migration task will be started.
3) Upon task start, the task status will change to **Verifying**, indicating that another round of parameter verification is underway. During this process, you are only able to cancel or view the task or check the verification progress.
4) After parameter verification succeeds, data migration will start.
During data sync, changes in data offset, source instance, and target instance key will be displayed.

### 5. Configure a migration alarm
DTS supports migration interruption alarming to keep you informed of any exceptions. A migration alarm can be configured as follows:
1) Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/policylist) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2) Click **Add** to create an alarm policy.
 - Policy type: select **Data Transmission Service** > **Self-built Migration**.
 - Alarm object: select the DTS task to be monitored and configure the **Trigger Condition** and **Alarm Object** to finish alarm configuration.
![](https://main.qcloudimg.com/raw/7b3769a436ce417c9ff6b34c9b56eb4d.png)

### 6. Complete the migration task 
Before disabling data sync, the data can be verified on the target instance, and if everything is correct, the migration task can be completed.
If the keys of the source instance and the target instance are identical, click **Complete** to finish data sync.

