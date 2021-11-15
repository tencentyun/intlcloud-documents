## Operation Scenarios
DTS provides data migration and continuous data replication from self-created MySQL databases to TencentDB, allowing you to migrate hot data without interrupting your business. MySQL with public IP/port, Direct Connect-based MySQL in local IDC, and CVM-based self-created MySQL can be migrated. Currently, DTS is supported for MySQL 5.7.

## Preparations
### Precautions
- A DTS data migration task involves two steps: cold backup data export and incremental data sync. As cold backup data export and data comparison after migration have certain impact on the load of the source database, you are recommended to perform database migration during off-hours or in the slave database.
- Migration of specified table
 If `lower_case_table_name` is specified for migration, a migration verification task will be performed to check whether the source and target databases have the same configuration; and if not, an error will be displayed, helping you prevent any restart issues caused by `lower_case_table_name` 
- Migration of entire database
 -  Before migrating configurations, if the source database has some parameters requiring database restart for them to take effect (e.g., `lower_case_table_name`), and their values are different from those in the target database, you need to configure restart of the target database. 
 -  After the full backup is imported, you need to restart the target database.
- SUPER privilege for the source database is required in some scenarios.

### SUPER privilege for source database
SUPER privilege for the source database is not required in most scenarios and required only in the following scenarios:
- You have selected "Full Detection" as "Data Consistency Detection".
- During binlog sync, if you create an event in the source database, and an account that is not used for DTS data migration is specified as the `DEFINER` for this event, an error will occur if the super privilege is unavailable.

### Migratable databases
- CVM-based self-created MySQL databases in the basic network or VPCs can be migrated to TencentDB.
- MySQL databases with public IP/port can be migrated to TencentDB.
- Direct Connect-based or VPN-based MySQL databases can be migrated to TencentDB.

### Precheck items
1. To avoid conflict, check whether the target database has a table with the same name as a table in the source database.
2. Check the database version. Data migration is supported for MySQL 5.1, 5.5, 5.6, and 5.7. As TencentDB no longer supports MySQL 5.1, you are recommended to upgrade MySQL 5.1 to MySQL 5.5 first and then migrate data to TencentDB for MySQL 5.5. You can also use DTS to directly migrate from local MySQL 5.1 to TencentDB for MySQL 5.5.
3. Check whether the capacity of the target database is greater than that of the source database.
4. Create a migration account on the source MySQL database (this is not required if you already have an authorized account for data migration).
```  	
        GRANT ALL PRIVILEGES ON *.* TO "migration account"@"%" IDENTIFIED BY "migration password";
    		FLUSH PRIVILEGES;	
```
5. Confirm the source database's MySQL variables.
    Run `SHOW GLOBAL VARIABLES LIKE 'XXX'; ` to view the global MySQL variables so as to check whether the database in the current state is suitable for migration:
```    	
            server_id > 1      
            log_bin = ON;            
            binlog_format = ROW/MIXED           
            binlog_row_image = FULL            
            innodb_stats_on_metadata = 0            
            You are recommended to set `wait_timeout` to above or equal to 3,600 seconds and mandatorily below 7,200 seconds.            
            Set `interactive_timeout` and `wait_timeout` to the same value.            
            If the source database is slave, confirm the following parameters in it:           
            log_slave_updates = 1           
```
6. Modify the variables.
    a. Modify the source database's MySQL configuration file `my.cnf` and restart the database:
```
  	        log-bin=[custom binlog filename]
```
  b. Modify the configuration dynamically:
```
             set global server_id = 99;                
             set global binlog_format=ROW;              
             set global binlog_row_image=FULL;                
             set global innodb_stats_on_metadata = 0;
```


## Directions
### 1. Create a DTS data migration service
Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page), enter the **Data Migration** page, and click **Create Task**.

### 2. Modify the configuration
Enter the settings of the task, source database, and target database.

#### Task settings
* Task Name: name the task.
* Scheduled Execution: specify a start time for the migration task.

#### Source database settings
Source Database Type: MySQL with public IP, CVM-based self-created MySQL, Direct Connect-based MySQL, and VPN-based MySQL are supported.

| Source Database Type | Description |
|---------|---------|
| MySQL with public IP | It refers to a MySQL database that can be accessed through a public IP. The following information is required: <li> MySQL server address<li> MySQL port<li> MySQL account<li> MySQL password	 |
| CVM-based self-created MySQL | You can migrate a MySQL database deployed on a CVM instance in the basic network or VPC by specifying the CVM instance ID and network environment. The following information is required: <li>Region: currently, a CVM-based self-created MySQL database can be migrated to a TencentDB instance only if they are in the same region; otherwise, you should use the CVM instance's public network access by selecting **MySQL with Public IP** for migration<li>CVM network: you can select the basic network or VPC<li>VPC: if a VPC is selected, you need to specify the VPC and subnet where the CVM instance resides<li>CVM instance ID<li>MySQL port<li>MySQL account<li>MySQL password			 |
| Direct Connect-based MySQL | After connecting a self-created MySQL database in your local IDC to Tencent Cloud through [Direct Connect](https://intl.cloud.tencent.com/product/dc), you can use DTS to migrate data to Tencent Cloud. The following information is required: <li>Direct Connect gateway: it is the Direct Connect gateway used by the database server to connect to Tencent Cloud. For more information, please see [Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256)<li>VPC: it is the VPC where the Direct Connect gateway resides<li>MySQL server address: it is the address of your MySQL server in the IDC. The IP mapped by the Direct Connect gateway will be accessed during DTS data migration<li>MySQL port<li>MySQL account<li>MySQL password |
| VPN-based MySQL | After connecting a self-created MySQL database in your local IDC to Tencent Cloud through [VPN Connections](https://intl.cloud.tencent.com/product/vpn) or a CVM-based self-created VPN service, you can use DTS to migrate data to Tencent Cloud. The following information is required: <li>Region: currently, only VPN services in the same region as that of the target TencentDB instance are supported<li>VPN type: you can select VPN Connections or CVM-based self-created VPN<li>VPN gateway: you need to provide the VPN gateway information only if VPN Connections is selected. <li> VPC: it is the VPC where the VPN Connections instance resides<li> MySQL server address: it is the address of your MySQL server in the IDC. The IP mapped by the Direct Connect gateway will be accessed during DTS data migration<li> MySQL port<li> MySQL account<li> MySQL password	 |

### 3. Select the database to be migrated
Select the database to be migrated (you can choose to migrate the entire database or only certain tables), create a migration task, and check the task information.
>
>1. The `character_set_server` and `lower_case_table_names` configuration items will be migrated only if the entire database is migrated.
>2. If the character set configuration of the migrated tables in the source database is different from that of the target database, the former will be retained.

**Data Migration**: export data from the selected database and import it into TencentDB for MySQL.
**Incremental Sync**: after exporting and importing data, set TencentDB for MySQL as the slave of the source database to implement incremental master/slave sync.
**Overwrite Target Database with Source Database Root Account**: as the root account is used for TencentDB authentication, subsequent TencentDB operations will be affected if the root account of the source database does not exist in the target database. Therefore, if the entire database is migrated, you should specify whether to overwrite the target root account with the source one. Select **Yes** if you want to use the root account of the source database or if the root account is not configured for the target database. Select **No** if you want to retain the root account of the target database.
**Read-only Target Database**: if this configuration item is selected, during data migration, data from the source database will be read-only in the target database and cannot be changed until you click the corresponding button to complete the migration.

### 4. Perform data consistency detection
Select a data consistency detection type as needed (e.g., full detection, sampling detection, or no detection).
>The detection ratio fields are required if sampling detection is selected.

### 5. Verify the migration task information
 After the migration task is created, you need to click **Next step: verify task** to verify the task information. You cannot start the migration task until all the check items are passed.
There are 3 statuses for task verification:

 - Passed: the verification is fully successful.
 - Warning: the verification fails. Database operation may be affected during or after data migration, but the migration task can still be executed.
 - Failed: the verification fails and the migration task cannot be executed. In this case, please check and modify the migration task information according to the error and then verify the task again. For more information on the failure causes, please see "Verification Failure Description".

### 6. Start migration
After the verification is passed, you can click **Start** to start data migration. Please note that if you have configured scheduled execution, the migration task will begin queuing and be executed at the specified time; otherwise, it will be executed immediately.
After the migration is started, you can view the corresponding migration progress under the migration task. The subsequent steps required for migration and the current stage will be displayed if you hover over the exclamation mark after the current step.

>Due to system design limitations, multiple migration tasks committed or queued at the same time will be performed in sequence by queuing time.

### 7. Perform incremental sync
When a migration task is created, the incremental sync option is selected by default. When data migration is completed, the target database will be set as the slave of the source database, and new data in the source database during migration will be synced to the target database through master/slave sync. In this way, any modification of the source database will be synced to the target database.
After migration, you can click **Complete** to close the sync between the source and target databases, and then switch the business to the target database to complete the migration.
>Before closing the sync, do not write data into the target database; otherwise, data comparison may fail due to inconsistency between the source and target databases, resulting in migration failure.


### 8. Cancel migration
>
1. Data that has been synced to the target database will not be cleared if you click "Cancel".
2. Restarting the task may cause the verification or task to fail. You may have to manually clear all databases or tables that may cause conflicts in the target database before you can start the migration task again.
3. When migrating a single table, make sure that all tables depended on by its foreign keys are also migrated.

To cancel an ongoing migration task, click **Cancel**.


### 9. Complete migration
>If the migration is in **not completed** status, the migration task will continue, so will data sync.

After the migration is 100% completed, you can click **Complete** on the right.

The following will be displayed after you click **Complete**



[1]:	https://intl.cloud.tencent.com/product/dc
[2]:	https://intl.cloud.tencent.com/document/product/216/549
[3]:	https://intl.cloud.tencent.com/product/vpn
[3]:	https://intl.cloud.tencent.com/product/vpn
[4]:	https://intl.cloud.tencent.com/document/product/215/4956

[img-creat0]: //mc.qcloudimg.com/static/img/d782322e94fc253a41f95e642f794b32/create0.png
[img-creat1]: //mc.qcloudimg.com/static/img/123cd23d3449cd5497502d8572f4b0a0/creat1.png
[img-creat2]: //mc.qcloudimg.com/static/img/8b75f2ad6610107c0856ea5e335c5923/create3.png
[img-init1]:  //mc.qcloudimg.com/static/img/cb72f72cf07d6b72c516d17d8ae8a114/init1.png
[img-init2]:  //mc.qcloudimg.com/static/img/3085341d195ecd9c0b5e130d86634e5e/init2.png
[img-init3]:  //mc.qcloudimg.com/static/img/5662f6a28286a2bb7ec3d1506206b5c7/init3.png
[img-init4]:  //mc.qcloudimg.com/static/img/2973c030e020d1a6e18ea882c062c741/init4.png
[img-init5]:  //mc.qcloudimg.com/static/img/f4f7f8156acd6899bcc534aa3913fa18/init5.png
[img-init6]:  //mc.qcloudimg.com/static/img/2402e535c9e893ba899ccf756e0c204c/init6.png
[img-init7]:  //mc.qcloudimg.com/static/img/d745dd9b585ca0a62cc30cabb1f31a3c/init7.png
[img-init8]:  //mc.qcloudimg.com/static/img/21effe29a213a3d3315ee776b8eed362/init8.png
