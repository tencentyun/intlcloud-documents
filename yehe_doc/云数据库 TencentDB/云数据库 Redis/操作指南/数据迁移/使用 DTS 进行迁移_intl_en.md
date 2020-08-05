## DTS Overview
Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs. Currently, DTS for Redis supports data migration on different versions of Redis and in various network scenarios.

| Term | Description |
|---------|---------|
| Source instance | Source instance to be migrated. |
| Target instance | Target instance to be migrated to, i.e., user-purchased TencentDB for Redis. |
| CVM-based self-created database | Redis service deployed on a CVM instance. |
| Public network-based self-created database | Redis service deployed on the public network. |

## Migration Compatibility
>?For compatibility issues with migration from Standalone Edition to Memory Edition (Cluster Architecture), please see [Notes on Migration from Standalone Edition to Cluster Edition](https://intl.cloud.tencent.com/document/product/239/35954).

#### Supported features
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync with the cloud by combining full migration and incremental sync.

#### Supported versions
- DTS supports Redis 2.8, 3.0, 3.2, 4.0, and 5.0.
- DTS supports single-node, Redis cluster, Codis, and twemproxy architectures.
- Migration permission requirements: to migrate data through DTS, the source instance must support SYNC or PSYNC commands.

#### Supported networks
DTS supports data migration and data sync in common scenarios, such as public network-based, CVM-based self-created, Direct Connect-based, VPN-based, and CCN-based databases.

#### Supported scenarios
- Cloudification migration: DTS supports migrating your Redis instance in a traditional IDC to TencentDB for Redis, moving your businesses to the cloud in an efficient and convenient manner.
- Cloud-based self-created service migration: DTS supports migrating your Redis service created with a virtual machine in Tencent Cloud or other clouds to TencentDB for Redis.
- Migration of Redis data from other cloud vendors: DTS supports migrating Redis data from other cloud vendors to Tencent Cloud provided that the SYNC or PSYNC command permission has been granted.
- Migration between cloud instances: DTS supports data migration or real-time sync between cloud instances. The supported versions are as follows:   
<table>
    <caption></caption>
    <tr>
<th style ="width:130px;position:relative;text-align:left;padding:5px px;font-weight:00;" valign="top" ><div style="position:absolute;width:1px;height:140px;top:0;left:0;background-color: #d9d9d9;display:block;transform:rotate(-66deg);transform-origin:top;valign=top;"></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Target Instance<br>Source Instance</th>
    </div>
    </th>
    <th style="background-color:#f2f2f2;">2.8 Memory Edition (Standard Architecture)</th>
    <th style="background-color:#f2f2f2;">4.0 Memory Edition (Standard Architecture)</th>
    <th style="background-color:#f2f2f2;">4.0 Memory Edition (Cluster Architecture)</th>
		<th style="background-color:#f2f2f2;">5.0 Memory Edition (Standard Architecture)</th>
    <th style="background-color:#f2f2f2;">5.0 Memory Edition (Cluster Architecture)</th>
    </tr>
    <tr>
    <td style="background-color:#f2f2f2;">2.8 Memory Edition (Standard Architecture)</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td style="background-color:#f2f2f2;">4.0 Memory Edition (Standard Architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td style="background-color:#f2f2f2;">4.0 Memory Edition (Cluster Architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
	<tr>
    <td style="background-color:#f2f2f2;">5.0 Memory Edition (Standard Architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
	 <td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td style="background-color:#f2f2f2;">5.0 Memory Edition (Cluster Architecture)</td>
    <td>x</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    </table>

#### Migration limitations
- To ensure migration efficiency, cross-region migration of CVM-based self-created instances is not supported.
- To migrate instances over the public network, make sure that the source instance is accessible from the public network.
- Only instances that are running normally can be migrated, while instances with no password initialized or with ongoing tasks cannot.
- The target instance must be empty with no data. During the migration process, it will be set to read-only, and writes will not be allowed.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the target instance.

## Migration Process
### 1. Create a migration task
1) Log in to the [DTS Console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
2) Select the corresponding region in **Linkage Region** and click **Buy at 0 CNY**.

### 2. Configure the task
- Task Name: name the task.
- Scheduled Execution: specify the start time of the migration task.
>?
> - To modify the scheduled task, you must click **Scheduled Start** again after the check is passed, so as to make the task start at the specified time.
> - If the specified time has passed, the task will start immediately. You can also click **Start Now** to start the task immediately.

### 3. Set the source instance and target instance
Redis instances on CVM are used here as an example, and the same is true for migration of instances over the public network.

| Field | Description | Remarks | Required |
|---------|---------|---------|---------|
| Task name | Migration task name | Facilitates task management | Yes |
| CVM instance ID | ID of the CVM instance where the source Redis instance resides | The migration task checks the CVM running conditions based on the CVM instance ID | Yes |
| CVM private IP | Private IP of the CVM instance where the source Redis instance resides | The migration task checks the CVM private IP | Yes |
| Port | Port number of the source instance | The migration task will access the source instance | Yes |
| Password | Source instance password | The password is used for authentication for accessing the source instance | No |
| Instance ID | Target instance ID | Data is synced to the target instance | Yes |

**Notes on migration in the Cluster Edition**
DTS supports migration in the Redis Cluster Edition. For cluster schemes with the Redis Cluster, Codis, or twemproxy architecture, simply enter the addresses and passwords of all shard nodes of the source cluster as the node information when creating the task. It is strongly recommended to perform data migration from a replica node (slave) of the source instance to avoid any impact on business access to the source instance. DTS supports password-free migration. The following is an example for entering relevant information for migration:
![](https://main.qcloudimg.com/raw/513d89660769db2dfd155514bcb38dfc.png)

### 4. Start the migration task
1) After the network connectivity test is successful, click **Save**.
2) DTS begins to verify the migration task, and once the migration requirements are met, the migration task will be started.
3) Upon task start, the task status will change to **Verifying**, indicating that another round of parameter verification is underway. During this process, you are only able to cancel or view the task or check the verification progress.
4) After parameter verification is successful, data migration will start.
During data sync, changes in data offset, source instance, and target instance key will be displayed.

### 5. Configure a migration alarm
DTS supports migration interruption alarming to keep you informed of any exceptions. A migration alarm can be configured as follows:
1) Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/policylist) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2) Click **Create** to create an alarm policy.
 - Policy Type: select **Data Transmission Service** > **Self-Created Migration**.
 - Alarm Object: select the DTS task to be monitored and configure the **trigger condition** and **alarm object** to finish alarm configuration.
![](https://main.qcloudimg.com/raw/120d51cd7bc4b66e3722ae6adcbf9469.png)

### 6. Complete the migration task 
Before disabling data sync, the data can be verified on the target instance, and if everything is correct, the migration task can be completed.
If the keys of the source instance and the target instance are identical, click **Complete** to finish data sync.

