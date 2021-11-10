
## Overview
DTS provides data migration and continuous data replication from self-created PostgreSQL databases to TencentDB, allowing you to migrate hot data without interrupting your business. PostgreSQL with public IP/port, Direct Connect-based PostgreSQL in local IDC, and CVM-based self-created PostgreSQL can be migrated.

>!Currently, data migration is only supported for PostgreSQL databases on 9.3.x or 9.5.x. Incremental sync is not supported for 9.3.x and can be used in 9.5.x only through an online [sync plugin](https://main.qcloudimg.com/raw/97b6b39254c963fcafc228a9c565a2e0.zip). For more information on how to configure and use the plugin, please see [Sync Plugin Configuration](#.E5.90.8C.E6.AD.A5.E6.8F.92.E4.BB.B6.E9.85.8D.E7.BD.AE).

## Directions

### Creating DTS data migration service
Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page.


### Setting source and target databases
On the page you are redirected to, enter the settings of the task, source database, and target database.
#### Task setting
* Task Name: specify a name for the task.
* Scheduled Execution: specify the start time of the migration task.

#### Source and target database settings
Source Database Type: PostgreSQL with public IP, CVM-based self-created PostgreSQL, Direct Connect-based PostgreSQL, VPN-based PostgreSQL, and TencentDB for PostgreSQL are supported.

| Source Database Type | Description |
|---------|---------|
| PostgreSQL with public IP | It refers to a PostgreSQL database that can be accessed through a public IP. The following information is required: <br><li>PostgreSQL server address<li>PostgreSQL port<li>PostgreSQL account<li>PostgreSQL password |
| CVM-based self-created PostgreSQL | You can migrate a PostgreSQL database deployed on a CVM instance in the classic network or VPC by specifying the CVM instance ID and network environment. The following information is required: <br><li>Region: currently, a CVM-based self-created PostgreSQL database can be migrated to a TencentDB instance only if they are in the same region; otherwise, you should use the CVM instance's public network access by selecting **PostgreSQL with Public IP** for migration<li>CVM network: you can select the classic network or VPC<li>VPC: if a VPC is selected, you need to specify the VPC and subnet where the CVM instance resides<li>CVM instance ID<li>PostgreSQL port<li>PostgreSQL account<li>PostgreSQL password |
| Direct Connect-based PostgreSQL | After connecting a self-created PostgreSQL database in your local IDC to Tencent Cloud through [Direct Connect](https://intl.cloud.tencent.com/product/dc), you can use DTS to migrate data to Tencent Cloud. The following information is required: <br><li>Direct Connect gateway: it is the Direct Connect gateway used by the database server to connect to Tencent Cloud. For more information, please see [Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256)<li>VPC: it is the VPC where the Direct Connect gateway resides<li>PostgreSQL server address: it is the address of your PostgreSQL server in the IDC. The IP mapped by the Direct Connect gateway will be accessed during DTS data migration<li>PostgreSQL port<li>PostgreSQL account<li>PostgreSQL password |
| VPN-based PostgreSQL | After connecting a self-created PostgreSQL database in your local IDC to Tencent Cloud through [VPN Connections](https://intl.cloud.tencent.com/product/vpn) or a CVM-based self-created VPN service, you can use DTS to migrate data to Tencent Cloud. The following information is required: <br><li>Region: currently, only VPN services in the same region as that of the target TencentDB instance are supported<li>VPN type: you can select [VPN Connections](https://intl.cloud.tencent.com/product/vpn) or CVM-based self-created VPN<li>VPN gateway: you need to provide the VPN gateway information only if [VPN Connections](https://intl.cloud.tencent.com/product/vpn) is selected. For more information, please see [VPN](https://intl.cloud.tencent.com/product/vpn)<li> VPC: it is the VPC where the VPN Connections instance resides<li>PostgreSQL server address: it is the address of your PostgreSQL server in the IDC. The IP mapped by the Direct Connect gateway will be accessed during DTS data migration<li>PostgreSQL port<li>PostgreSQL account<li>PostgreSQL password |
| TencentDB for PostgreSQL | It refers to a TencentDB for PostgreSQL instance. The following information is required:<br><li>PostgreSQL instance ID<li>PostgreSQL account<li>PostgreSQL password   |

![](https://main.qcloudimg.com/raw/a5c20fabbb3dc7994f33439042226a65.png)

### Selecting database to be migrated
Select the database to be migrated (you can choose to migrate the entire database or only certain tables).
![](https://main.qcloudimg.com/raw/ebb6a7e26b857b22957a0295fa5947a5.png)

### Verifying migration task information
Click **Next step: verify task** to verify the migration task information. You cannot start the migration task until all the check items are passed. After the verification is completed, click **Start**.
There are 3 statuses for task verification:
 - Passed: the verification is fully successful.
 - Warning: the verification fails. Database operation may be affected during or after data migration, but the migration task can still be executed.
 - Failed: the verification fails and the migration task cannot be executed. In this case, please check and modify the migration task information according to the error and then verify the task again.
![](https://main.qcloudimg.com/raw/234b7900b1d1049204bb42977c5fa2c6.png)

### Starting migration
After the verification is passed, return to the data migration list and click **Start** in the **Operation** column to start data migration. Please note that if you have configured scheduled execution, the migration task will begin queuing and be executed at the specified time; otherwise, it will be executed immediately.
After the migration is started, you can view the corresponding migration progress under the migration task. The subsequent steps required for migration and the current stage will be displayed if you hover over the exclamation mark after the current step.

>!Due to system design limitations, multiple migration tasks committed or queued at the same time will be performed in sequence by queuing time.

### Incremental sync
When a migration task is created, the incremental sync option is selected by default. When data migration is completed, the target database will be set as the slave of the source database, and new data in the source database during migration will be synced to the target database through master/slave sync. In this way, any modification of the source database will be synced to the target database.
After migration, you need to click **Complete** to close the sync between the source and target databases so as to complete the migration.

>!Before closing the sync, do not write data into the target database; otherwise, data comparison may fail due to inconsistency between the source and target databases, resulting in migration failure.

### Stopping migration
To stop an ongoing migration task, click **Cancel** in the **Operation** column of the task.

>!
>- Restarting the task may cause the verification or task to fail. You may have to manually clear all databases or tables that may cause conflicts in the target database before you can start the migration task again.
>- When migrating a single table, make sure that all tables depended on by its foreign keys are also migrated.

### Completing migration
![](https://main.qcloudimg.com/raw/1bd1e0106ab6ac0b40765e030dc3b102.png)

## Sync Plugin Configuration
1. Download and copy [dts_decoding](https://main.qcloudimg.com/raw/97b6b39254c963fcafc228a9c565a2e0.zip) to the `lib` directory in the PostgreSQL installation path.
![](https://main.qcloudimg.com/raw/1fdb249844a331ffb073cf0544ac8c3f.png)
2. Modify the configuration file `postgresql.conf` in the `data` directory.
```
wal_level >= logical
 Available max_replication_slots >= number of databases to be migrated
 Available max_wal_senders >= number of databases to be migrated
```
![](https://main.qcloudimg.com/raw/1a6819eff953e9d885175f0ff7cdde42.png)
![](https://main.qcloudimg.com/raw/41a8bb56280c4f6e82c9a9025e611b49.png)
3. Modify the configuration file `pg_hba.conf` in the `data` directory.
 Replication connection needs to be configured. 
![](https://main.qcloudimg.com/raw/9ea1ec694a672b98f168a81ee7080c6a.png)
4. Restart the source database.
>!When specified tables are migrated, if tables use rules or are associated with other tables, data insertion during incremental migration may fail, as some SQL operations are not supported by the migration feature. In this case, you can migrate schemas or all databases.





