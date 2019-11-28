
## DTS for Redis Overview
Tencent Cloud Data Transmission Service (DTS) is a database data transmission service that integrates such features as data migration, sync, and subscription, helping you migrate your database without interrupting your businesses and build a high-availability database architecture for remote disaster recovery through real-time sync channels. DTS for Redis currently supports data migration between different editions of Redis and in various network scenarios.

| Term | Description |
|---------|---------|
| Source instance | Source instance to be migrated. |
| Destination instance | Destination instance to be migrated to, i.e., user-purchased TencentDB for Redis. |
| Instance created by CVM | Redis service deployed on a CVM instance. |
| Instance created by a public network | Redis service deployed on a public network. |

## Migration Compatibility

#### Supported Features
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync with the cloud by combining full migration and incremental sync.

#### Supported Versions
- DTS supports Redis 2.8, 3.0, 3.2, and 4.0.
- DTS supports single-node, Redis cluster, Codis, and tewmproxy architectures.
- Migration permission requirements: To migrate data via DTS, the source instance must support SYNC or PSYNC commands.

#### Supported Networks
DTS supports data migration and data sync across a public network, CVM-created instances, Direct Connect gateways, VPN gateways, and CCN.

#### Supported Scenarios
- Cloudification migration: DTS supports migrating your Redis instance in a traditional IDC to TencentDB for Redis, moving your businesses to the cloud in an efficient and convenient manner.
- Self-built service migration: DTS supports migrating your Redis service created with a virtual machine in Tencent Cloud or other clouds to TencentDB for Redis.
- Migration of Redis data from other cloud vendors: DTS supports migrating Redis data from other cloud vendors to Tencent Cloud provided that the SYNC or PSYNC command permission has been granted.
- Migration between cloud instances: DTS supports data migration or real-time sync between cloud instances. The supported versions are as follows:
    <table>
    <tr>
    <td colspan=3 align=center>Source instance</td>
    <td rowspan=2 align=cente>Destination instance</td>
    </tr>
    <tr>
    <td>2.8 Standard Edition</td>
    <td>4.0 Standard Edition</td>
    <td>4.0 Cluster Edition</td>
    </tr>
    <tr>
    <td>✓</td>
    <td>x</td>
    <td>x</td>
    <td>2.8 Standard Edition</td>
    </tr>
    <tr>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>4.0 Standard Edition</td>
    </tr>
    <tr>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>4.0 Cluster Edition</td>
    </tr>
    </table>

#### Migration Limitations
- To ensure migration efficiency, cross-region migration of instances created by CVM is not supported.
- To migrate instances over a public network, make sure that the source instance is accessible from the public network.
- Only instances that are running normally can be migrated, while instances with no password initialized or with ongoing tasks cannot be migrated.
- The destination instance must be empty with no data. During the migration process, the instance will be locked and Writes will not be allowed.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the destination instance.

## Migration Process
### 1. Create a migration task
1. Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page) and click *Create Task** in the data migration list to create a migration task.
2. Select the corresponding region on **Link Region** and click **Buy at 0$**.

### 2. Configure the task
- Task Name: Name the task.
- Scheduled Execution: Specify the start time of the migration task.
>- To modify the scheduled task, you must click **Scheduled Start** again after verification is passed so as to make the task start at the specified time.
> - If the specified time has passed, the task will start immediately. You can also click **Start Now** to start the task immediately.

### 3. Set the source instance and destination instance
Redis instances on CVM are used here as an example, and the same is true for migration of instances over a public network.

| Field | Description | Remarks | Required |
|---------|---------|---------|---------|
| Task name | Migration task name | Facilitates task management | Yes |
| CVM instance ID | ID of the CVM instance where the source Redis instance resides | The migration task checks the CVM running conditions based on the CVM instance ID | Yes |
| CVM private IP | Private IP of the CVM instance where the source Redis instance resides | The migration task checks the CVM private IP | Yes |
| Port | Port number of the source instance | The migration task accesses the source instance | Yes |
| Password | Source instance password | The password is used for authentication for accessing the source instance | No |
| Instance ID | Destination instance ID | Data is synched to the destination instance | Yes |

**Notes on Migration in the Cluster Edition**
DTS supports migration in the Redis Cluster Edition. For cluster schemes with the Redis Cluster, Codis, or tewmproxy architecture, simply enter the addresses and passwords of all shard nodes of the source cluster as the node information when creating the task. It is strongly recommended to perform data migration from a replica node (slave) of the source instance to avoid any impact on business access to the source instance. DTS supports password-free migration. The following is an example for entering relevant information for migration:
![](https://main.qcloudimg.com/raw/513d89660769db2dfd155514bcb38dfc.png)

### 4. Start the migration task
1. After the network connectivity test is successful, click **Save**.
2. DTS begins to verify the migration task, and once the migration requirements are met, the migration task will be started.
2. Upon task start, the task status will change to **Verifying**, indicating that another round of parameter verification is underway. During this process, you are only able to cancel or view the task or check the verification progress.
3. After parameter verification succeeds, data migration will start.
During data sync, changes in data offset, source instance, and destination instance key will be displayed.

### 5. Configure a migration alarm
DTS supports migration interruption alarming to keep you informed of any exceptions. A migration alarm can be configured as follows:
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/policylist) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. Click **Create** to create an alarm policy.
 - Policy Type: Select **Data Transfer Service** > **Self-built Migration**.
 - Alarm Object: Select the DTS task to be monitored and configure the **trigger** and **alarm object** to finish alarm configuration.
![](https://main.qcloudimg.com/raw/120d51cd7bc4b66e3722ae6adcbf9469.png)

### 6. Complete the migration task 
Before disabling data sync, the data can be verified on the destination instance, and if everything is correct, the migration task can be completed.
If the keys of the source instance and the destination instance are identical, click **Complete** to finish data sync.

 
