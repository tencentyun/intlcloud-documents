
This document describes how to migrate data between TencentDB for MySQL instances, using the data migration feature of Data Transmission Service (DTS). DTS supports structural migration, full data migration, and incremental data migration, as well as non-stop smooth data migration between TencentDB for MySQL instances.
<span id="qttj"></span>
## Prerequisites
- You have [created a TencentDB for MySQL instance](https://intl.cloud.tencent.com/document/product/236/37785). Supported versions: MySQL 5.5, MySQL 5.6, and MySQL 5.7.
- You need to create a migration account on the target MySQL instance. Account permissions required: all the read/write permissions for objects to be migrated.

## Notes: 
A DTS data migration task between TencentDB for MySQL instances involves two steps: cold backup data export and incremental data sync. Cold backup data export and migrated data comparison have certain effect on the load of the source database, so we recommended that you perform database migration during off-peak hours or in the standby database.
- During the migration verification task, `lower_case_table_name` is specified to check whether the configuration of the source and target instances is consistent. If not, an error will be reported. Please avoid any restart issue due to `lower_case_table_name` in advance.
- For a full instance migration task, you need to restart the target instance after the full backup is imported.

## Supported Migration Types
- Structural migration: DTS allows you to migrate the structure definition of migration objects to the target instance. Currently, DTS supports the structural migration of an entire instance and specified tables.
- Full migration: DTS allows you to migrate the full data of the source MySQL instance to the target TencentDB for MySQL instance.
- Incremental sync: DTS reads and parses the binlog information of the source MySQL database based on full data migration, and synchronizes the incremental data of the source MySQL database to the target MySQL database.

## Precheck Items
1. To avoid conflict, check if any tables with the same name exist in the target TencentDB for MySQL database.
2. Check database versions. MySQL 5.5, MySQL 5.6, and MySQL 5.7 can be migrated to cloud.
3. Check and ensure that the target TencentDB for MySQL database has a larger capacity than the source TencentDB for MySQL database does.
4. Create a migration account on the source TencentDB for MySQL database. Ignore this step if you already have an authorized account for data migration.
```
GRANT ALL PRIVILEGES ON *.* TO "migration account"@"%" IDENTIFIED BY "migration password";
FLUSH PRIVILEGES;
```
5. Confirm source MySQL database variables.
Run `SHOW GLOBAL VARIABLES LIKE 'XXX';` to view the global MySQL variables so as to check whether the database in the current state is suitable for migration:
```
server_id > 1
log_bin = ON;
binlog_format = ROW/MIXED
binlog_row_image = FULL
innodb_stats_on_metadata = 0
wait_timeout is recommended to be greater than or equal to 3600 seconds, and must be less than 7200 seconds
Set the same duration for interactive_timeout and wait_timeout
```
If the source instance is a slave instance, confirm the following parameters in the source instance:
```
log_slave_updates = 1
```
6. Modify the variables.
a. For a self-created MySQL database, you need to modify the configuraiton file `my.cnf` of the source MySQL database and restart:
```
log-bin=[custom binlog file name]
```
b. Modify configuration dynamically:
```
set global server_id = 99;
set global binlog_format=ROW;
set global binlog_row_image=FULL;
set global innodb_stats_on_metadata = 0;
```

## Directions
1. Log in to the [DTS data migration console](https://console.cloud.tencent.com/dts/migration?rid=8&page=1&pagesize=20) and click **Create Migration Task** to enter the migration task creation page.
2. Select the region of the target instance and click ** Buy at 0 USD**. Currently, DTS data migration services are free of charge.
3. Complete task configuration, source database settings, and target database settings on the “Set source and target databases” page. After the connectivity test for the source and target databases is passed, click **Create**.
>?If the connectivity test fails, follow the prompts to troubleshoot, resolve the problem, and try again.
>
 - Task Configuration
    - Task Name: specify a name for the task.
    - Scheduled Execution: specify the start time of the migration task.
    - Tag: you can use tags to manage resources by category from different dimensions.
 - Source Database Settings
    - Source Type: select “MySQL”.
 - Target Database Settings
    - Select the target database instance and enter its account and password.
4. On the “Set migration options and select migration objects” page, set the migration type and objects, and click **Save**.
>!
>- The `character_set_server` and `lower_case_table_names` configuration items are migrated only when the entire instance is migrated.
>- If the character set configuration of migrated tables in the source instance is different from that of the target instance, the character set configuration of the source instance is retained.
>
 - Migration Type: structural migration, full migration, and full + incremental migration supported.
 - Migration Object: the entire instance and specified objects supported.
 - Overwrite Target Database with Source Database Root Account: root accounts are used to verify the security of the TencentDB for MySQL database. Without the root account of the source database, you cannot conveniently use the TencentDB for MySQL database subsequently. Therefore, you need to specify whether to overwrite the target database root account with the source one during the full instance migration process. Select **Yes** if you want to use the root account of the source database or if the root account is not configured for the target database. Select **No** if you want to retain the root account of the target database.
 - Read-only Target Database: if this configuration item is selected, during data migration, data from the source database will be read-only in the target database and cannot be changed until you click the corresponding button to complete the migration.
 - Data Consistency Check: you can select “full data consistency check” or “no check”.
5. Verify the migration task on the “Verify task” page. After the task is verified, click **Start**.
There are 3 statuses for task verification:
 - Passed: the verification is fully successful.
 - Warning: the verification fails. Database operation may be affected during or after data migration, but the migration task can still be executed.
 - Failed: the verification fails and the migration task cannot be executed. In this case, please check and modify the migration task information according to the error and then verify the task again. For more information on the failure causes, please see "Verification Failure Description".
After the verification is passed, return to the data migration list and click **Start** to start data migration immediately. Please note that if you have configured scheduled execution, the migration task will begin queuing and be executed at the specified time; otherwise, it will be executed immediately.
After the migration is started, you can view the corresponding migration progress under the migration task. The subsequent steps required for migration and the current stage will be displayed if you hover over the exclamation mark after the current step.
>!Due to system design limitations, multiple migration tasks submitted or queued at the same time will be performed in sequence by queuing time.
>
7. During the creation of the migration task, the incremental sync option is selected by default. When data migration is completed, the target TencentDB for MySQL database will be set as the slave database for the source database. The incremental data of the source database during migration will be synchronized to the target TencentDB for MySQL database via master/slave sync. In this case, any changes made to the source database will be synchronized to the target TencentDB for MySQL database.
>!Do not write data into the target database instance before terminating the sync. Otherwise, data comparison may fail due to data inconsistency between the source and target databases, resulting in a migration failure.
>
8. (Optional) To cancel an in-progress migration task, click **Cancel**.
>!
>- Data that has been synchronized to the target database will not be cleared if you click **Cancel**.
>- Restarting the task may cause verification or task failure. You may need to manually clear all databases or tables that may cause conflicts in the target database before you can start the migration task again.
>- When migrating a single table, make sure that all tables relying on foreign keys are migrated.
>
9. Complete the migration.
>!If the migration is in “not completed” status, the migration task will continue, so will data sync.
>
When the migration progress reaches 100%, the data gap between the target and source databases is 0 MB, and the time delay between them is 0 second, it means data has been synchronized. You can click **Complete** on the right to complete the migration task.
