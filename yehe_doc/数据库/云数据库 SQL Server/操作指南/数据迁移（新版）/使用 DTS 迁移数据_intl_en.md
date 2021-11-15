This document describes how to use the Data Transmission Service (DTS) to migrate data from SQL Server databases to TencentDB for SQL Server databases.

DTS migrates data with no downtime. To migrate with DTS, you need to make sure the source instance can connect to the target instance over a network.

## Description
- **Supported versions**
DTS supports migration to SQL Server 2008 R2, 2012, 2014, 2016, 2017 and 2019 databases.
- **Supported networks**
DTS supports data migration and data sync between CVM-based self-created instances and over a public network, Direct Connect, and VPN.

## Migration Use Cases
- **Migration to cloud**: DTS supports migrating your SQL Server databases in a traditional IDC to TencentDB for SQL Server, moving your businesses to the cloud in an efficient and convenient manner.
- **Migration from self-created databases**: DTS supports migrating your SQL Server databases self-created on virtual machines on Tencent Cloud or other clouds to TencentDB for SQL Server.
- **Migration from other cloud vendors**: DTS supports migrating SQL Server databases from other cloud vendors to TencentDB for SQL Server.
- **Migration between instances on Tencent Cloud**: DTS supports migration between instances on Tencent Cloud. However, data of high-availability and cluster instances cannot be migrated to basic instances.

## Notes
- Before migration, make sure that the SQL Server version of the target instance is not earlier than that of the source instance.
- Only one migration task can be initiated for a source instance at a time.
- To migrate data from a source SQL Server instance which is created on CVM or other clouds, or to migrate over a public network, you need the `sysadmin` permission.
- A full migration task cannot be canceled.
- When a full + incremental migration task is canceled, the target instance will be rolled back to the state prior to the start of the migration.
- Currently, cross-region data migration is supported only for regions in the Chinese mainland.

## Migration Directions
### 1. Create a migration task
1) Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.
2) Select a region in **Linkage Region** and click **Buy at 0 USD**.
>?The linkage region you select should be the region where the target instance resides.

### 2. Configure the migration task
Configure the task, source database, and target database. After the network connectivity test is successful, click **Create**.

#### a. Task settings
- Task name: specify a name for the task.
- Scheduled execution: specify the start time of the migration task.
>?
>- To modify the scheduled task, you must click **Scheduled start** again after the check is passed, so as to make the task start at the specified time.
>- If the specified time has passed, the task will start immediately. You can also click **Immediate start** to start the task immediately.

#### b. Source database settings
- Source database type: select SQL Server.
- Access type: public network, self-created on CVM, Direct Connect, or VPN.

#### c. Target database settings
- Target database type: select SQL Server.
- Database instance: select the target database instance and enter its account and password.
![](https://main.qcloudimg.com/raw/0c0db8639cc644fbf56d12d94ae8d24c.png) 

 

### 3. Set migration options and select migration objects
Specify the data type and objects to be migrated. The migration type supports full migration and full + incremental migration. After confirming that everything is correct, click **Save**.
 ![](https://main.qcloudimg.com/raw/3a0d33529d07be6b6c2ed7d245a0cf52.png) 

### 4. Verify the migration task
View the verification results of the migration task.
- If the verification is successful, click **Start Task**.
![](https://main.qcloudimg.com/raw/1c7cc5db78038606e3f8f8d38baa91b4.png)
- If one or more check items fail, click **View Details**, troubleshoot based on the pop-up tips, and verify the task again.

### 5. Start the migration task
1) After the verification is successful, click **Start Task** on the task verification page.
![](https://main.qcloudimg.com/raw/06639e9b1ad76bbf49afe2a4722c0eee.png)
>!
>- If the scheduled start is not set, the task will start immediately.
>- If the scheduled start is set, the migration task will queue and start at the specified start time. You can also manually start the migration task by clicking **Immediate start** in the migration task list.
>
2) After the migration task starts, go back to the migration task list and view its progress.


### 6. Complete the migration task
Before disabling data sync, the data can be verified on the target instance, and if everything is correct, the migration task can be completed.
