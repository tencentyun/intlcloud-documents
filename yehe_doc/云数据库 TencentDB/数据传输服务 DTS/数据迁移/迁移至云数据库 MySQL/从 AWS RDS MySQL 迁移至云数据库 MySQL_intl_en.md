This document describes how to migrate data from AWS RDS for MySQL to TencentDB for MySQL, using the data migration feature of Data Transmission Service (DTS). DTS supports structural migration, full data migration, and incremental data migration, as well as non-stop smooth data migration to TencentDB for MySQL.
<span id="qttj"></span>
## Prerequisites
- You have [created a TencentDB for MySQL instance](https://intl.cloud.tencent.com/document/product/236/37785). Supported versions: MySQL 5.6 and MySQL 5.7.
- You need to create a migration account on the target MySQL instance. Account permissions required: all the read/write permissions for objects to be migrated.
- The source AWS RDS for MySQL instance to be migrated can be accessed via public network. The public availability of AWS RDS for MySQL should be enabled. Supported versions: MySQL 5.6 and MySQL 5.7.
-. You need to create a migration account on the source AWS RDS MySQL instance. Account permissions required are as follows:
```
CREATE USER ‘migration account’@‘%’ IDENTIFIED BY ‘migration password’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ‘migration account’@‘%’;  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO ‘migration account’@‘%’;  
GRANT SELECT ON `mysql`.* TO ‘migration account’@‘%’;
```
- Partial table migration: `GRANT SELECT ON database to be migrated.* TO ‘migration account’;`
- Full instance migration: `GRANT SELECT ON *.* TO ‘migration account’;`

## Notes:
- When DTS performs full data migration, it will occupy certain source instance resources, which may increase the load of the source instance and the database pressure. If your database has low configurations, we recommend that you migrate data during off-peak hours.
- Only tables with primary keys on the source MySQL instance can be migrated. During the full data migration process, no locks are needed and write operations are not blocked, so your business will be less impacted. We recommend that you add primary keys to the data tables of the source MySQL instance before data migration.
- In case of DDL operations during the lock-free full data migration process, the migration task may fail. Therefore, please avoid DDL operations during this process.
- The storage capacity of TencentDB for MySQL instance must be at least 1.2 times larger than that of AWS RDS for MySQL instance.
- If the source AWS RDS for MySQL instance is not GITD-based, DTS will not support the HA (Highly Available) switchover of the source instance. Once the HA switchover occurs on the source AWS RDS for MySQL instance, the DTS incremental sync may be interrupted.

## Supported Migration Types
- Structural migration: DTS allows you to migrate the structure definition of migration objects to the target instance. Currently, DTS supports the structural migration of databases, data tables, and views.
- Full migration: DTS allows you to migrate the full data of the source MySQL instance to the target TencentDB for MySQL instance.
- Incremental sync: DTS reads and parses the binlog information of the source AWS RDS for MySQL instance based on full data migration, and synchronizes the incremental data of the AWS RDS for MySQL instance to the target TencentDB for MySQL. In this way, incremental data can be smoothly migrated to Tencent Cloud in a non-stop manner.

## SQL Operations Supported by Incremental Sync
| Operation Type | SQL Operations Supported by Incremental Sync |
| -------- | ------------------------------------------------------------ |
| DML | INSERT, UPDATE, DELETE, and REPLACE |
| DDL | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, and RENAEM TABLE <br>VIEW: CREATE VIEW, ALTER VIEW, and DROP VIEW<br>INDEX: CREATE INDEX and DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, and DROP DATABASE |

## Preparation
Log in to the AWS RDS for MySQL instance, set the binlog retention period, and run the following command:
```
call mysql.rds_set_configuration('binlog retention hours', 24);
```
The command above sets the binlog retention period as 24 hours, and the maximum retention period can be 168 hours, namely 7 days.

## Precheck
You need to perform precheck before starting a data migration task. The main check content and points are shown below:

| Check Content | Check Point |
| -------------------- | ------------------------------------------------------------ |
| Database connectivity check | The source and target databases can access the Internet |
| Environment check | Check the environment variable `innodb_stats_on_metadata=off` |
| Version check | Only MySQL 5.6 and MySQL 5.7 are supported for the source and target databases, and the source database version must be earlier than or the same as the target database version |
| Partial instance parameter check | The `table_row_format` cannot be `Fixed`<br>The `lower_case_table_names` variables of the source and target databases must be consistent<br>The parameter `max_allowed_packet` of the target database must be at least 4 M<br>The variable `connect_timeout` of the source database must be greater than 10 |
| Source instance permission check | See account permissions in [Prerequisites](#qttj) |
| Target instance permission check | The target TencentDB for MySQL instance needs the following permissions: ALTER,  ALTER ROUTINE,  CREATE,  CREATE ROUTINE,  CREATE TEMPORARY TABLES,  CREATE USER,  CREATE VIEW,  DELETE,  DROP,  EVENT,  EXECUTE,  INDEX,  INSERT,  LOCK TABLES,  PROCESS,  REFERENCES,  RELOAD,  SELECT,  SHOW DATABASES,  SHOW VIEW,  TRIGGER,  UPDATE |
| Target instance’s content conflict check | The target instance cannot have tables that conflict with the source instance |
| Target instance capacity check | The capacity of the target instance must be at least 1.2 times larger than the tablespace of the source instance |
| Binlog parameter check | The variable `binlog_format` of the source instance must be `ROW`<br>The variable `log_bin` of the source instance must be `ON`<br>The variable `binlog_row_image` of the source instance must be  `FULL`<br> If the variable `gtid_mode` of the source instance (including MySQL 5.6 and later versions) is not `ON`, the `WARNING` will appear. We recommend that you enable `gtid_mode`<br>You are not allowed to set `do_db` and `ignore_db`<br>If the source instance is a secondary database, the variable `log_slave_updates` must be `ON` |
| Foreign key dependency check | The foreign key dependency can either be `no action` or `restrict`<br>For partial table migration, tables with foreign key dependencies must be complete |
| View check | Only a definer that is the same as the `user@host` of the migration objects is allowed |
| Other warning check | If the `max_allowed_packet` of the source database is larger than that of the target database, a warning will appear<br>If the `max_allowed_packet` of the target database is less than 1 GB, a warning will appear<br>If the character sets of the source and target databases are inconsistent, a warning will appear<br>For full migration (incremental migration excluded), you will be warned that this is a lock-free full data migration, so data consistency cannot be guaranteed |
| Checking table without primary key | Tables to be migrated cannot contain tables without primary key |

## Directions
1. Log in to the [DTS data migration console](https://console.cloud.tencent.com/dts/migration?rid=8&page=1&pagesize=20) and click **Create Migration Task** to enter the migration task creation page.
2. Select the region of the target instance and click ** Buy at 0 USD**. Currently, DTS data migration services are free of charge.
3. Complete task configuration, source database settings, and target database settings on the “Set source and target databases” page. After the connectivity test for the source and target databases is passed, click **Create**.
>?If the connectivity test fails, follow the prompts to troubleshoot, resolve the problem, and try again.
>
<table>
<thead><tr><th>Setting Type</th><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a name that has business meaning for easy task identification</td></tr>
<tr>
<td>Running Mode</td>
<td>“Immediate execution” and “Scheduled execution” supported. For immediate execution, the task is started immediately after the task is verified; for scheduled execution, you need to set the task execution time so that the task can be started upon the execution time.</td></tr>
<tr>
<td>Tag</td>
<td>The tag is used to manage resources by category from different dimensions. If the existing tag does not meet your requirements, please go to the console **Manage Tags**.</td></tr>
<tr>
<td rowspan=9>Source Database Settings</td>
<td>Source Database Type</td><td>Select “MySQL”.</td></tr>
<tr>
<td>Service Provider</td><td>Select “AWS”.</td></tr>
<tr>
<td>Database Version</td><td>Select RDS MySQL 5.6 or RDS MySQL 5.7.</td></tr>
<tr>
<td>Access Type</td><td>Select “Public Network”.</td></tr>
<tr>
<td>Region</td><td>The region of the source database refers to the outbound region of DTS. Please select the nearest region to AWS RDS for MySQL.</td></tr>
<tr>
<td>Host Address</td><td>The IP address to access AWS RDS for MySQL. You can obtain this address on the basic information page of AWS RDS for MySQL.</td></tr>
<tr>
<td>Port</td><td>The access port of AWS RDS for MySQL, which is 3306 by default.</td></tr>
<tr>
<td>Account</td><td>The database account of AWS RDS for MySQL. The account permissions need to meet certain requirements.</td></tr>
<tr>
<td>Password</td><td>The password of the AWS RDS for MySQL database account.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>Select “MySQL”.</td></tr>
<tr>
<td>Access Type</td><td>Select “TencentDB”</td></tr>
<tr>
<td>Region</td><td>The region you select in the last step.</td></tr>
<tr>
<td>Database Instance</td><td>Select the target TencentDB instance ID.</td></tr>
<tr>
<td>Account</td><td>The account of the target TencentDB database. The account permissions need to meet certain requirements.</td></tr>
<tr>
<td>Password</td><td>The password of the target TencentDB database account.</td></tr>
</tbody></table>
4. On the “Set migration options and select migration objects” page, set the migration type and objects, and click **Save**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select “structural migration” if you only need structural migration.<br>Select “full migration” if you only need full data migration.<br>Select “full + incremental migration” if you need non-stop smooth data migration</td></tr>
<tr>
<td>Migration Object</td>
<td>Select “entire instance” if you need to migrate the entire instance, but system databases such as `information_schema`, `mysql`, `performance_schema`, and `sys` won’t be migrated <br>Select “specified object” if you need to migrate specified tables.</td></tr>
<tr>
<td>Specified Object</td>
<td>Select the object to be migrated in the “source database object” box, and drag it to the “selected object” box.</td></tr>
</tbody></table>
5. Verify the migration task on the “Verify task” page. After the task is verified, click **Start**.
 -  If the task is verified, start the migration task according to the running mode you select.
 -  If task verification fails, you can view the verification items and troubleshoot. Verify the task again after the problem is solved.
6. Return to the data migration task list, and the task will be in the “creating” status. After running for 1-2 minutes, the data migration task will be started.
 - Structural + full migration task: the task will automatically end when it is completed. If you don’t need to cancel the task, do not manually end it. Otherwise, the migrated data will be lost.
 - Full + incremental migration task: After the full migration task is completed, it will automatically enter the stage of incremental data sync which will not automatically end. You need to click **Complete** to end incremental data sync.
    - Please manually complete incremental data sync and business switchover at appropriate time.
    - Observe whether the migration task is in the incremental sync stage and is in the “no delay” status. If so, stop writing data to the source database for a few minutes.
    - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time delay between them is 0 second.
7. (Optional) You can also click the task ID to enter the task details page, and then view migration task details and the migration object list.
