This document describes how to use the data migration feature of DTS to migrate data from MySQL to TDSQL for MySQL.

## Notes
- During full data migration, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you migrate the data during off-peak hours.
- Full migration is implemented with tables locked, which causes write operations to be blocked for a few seconds.

## Prerequisites
- You have created a [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/1042/33336) instance.
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all [preparations](https://intl.cloud.tencent.com/document/product/571/42652).
- You need to create a `__tencentdb__` database in advance in the source MySQL database.
- You need to have the permissions of the source database.
  - To migrate the "entire instance", the following account permissions are required:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, CREATE ON `__tencentdb__`.* TO 'migration account'@'%'; // If the source database is a TencentDB database, you need to grant the `__tencentdb__` permission
GRANT SELECT ON *.* TO 'migration account';
```
  - To migrate the "specified objects", the following account permissions are required:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, CREATE ON `__tencentdb__`.* TO 'migration account'@'%'; // If the source database is a TencentDB database, you need to grant the `__tencentdb__` permission
GRANT SELECT ON `mysql`.* TO 'migration account'@'%';
GRANT SELECT ON database to be migrated.* TO 'migration account';
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Application Restrictions
- Only basic tables can be migrated, while objects such as views, functions, triggers, and stored procedures cannot.
- System databases/tables and user information including `information_schema`, `sys`, `performance_schema`, `__tencentdb__`, and `mysql` cannot be migrated. After the migration is completed, if you want a view, stored procedure, or function in the target database to be called, you must grant the caller the read/write permissions. 
- When exporting the view structure, only the `definer` that is the same as the target migration account's `user@host` can be migrated.
- View restrictions:
  - Views in the source database will be ignored and not migrated during full migration.
  - View DDL operations generated in the source database will only be replayed in the first shard of the target database during incremental migration.
- Only data with the InnoDB database engine can be migrated. Tables with other engines will be skipped during migration by default.
- Correlated data objects must be migrated at the same time; otherwise, migration will fail.
- During incremental migration, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, the migration will fail.

## Operation Restrictions
- During migration, do not perform the following operations; otherwise, the migration task will fail:
  - Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
  - Do not run distributed transactions in the source database.
  - Do not write binlog data in the `STATEMENT` format into the source database.
  - Do not clear binlogs in the source database.
  - Do not delete the system table `__tencentdb__` during incremental migration. 
- If you only perform full data migration, do not write new data into the source database during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

## Supported SQL Operations
| Operation Type | Synchronizable SQL Operations               |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, and REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, and TRUNCATE TABLE<br>VIEW: CREATE VIEW and DROP VIEW<br>INDEX: CREATE INDEX and DROP INDEX |

## Environment Requirements
> ?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Requirements for Check Items](https://intl.cloud.tencent.com/document/product/571/42552); otherwise, wait for the system verification to complete and fix the problem according to the error message.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<li>The source and target databases can be connected.</li>
<ul>
<li>Requirements for the database parameters:
<ul>
<li>`table_row_format` cannot be set to `FIXED`.</li>
<li>The values of the `lower_case_table_names` variable in both the source and target databases must be the same.</li>
<li>The `max_allowed_packet` parameter in the target database must be at least 4 MB.</li>
<li>The `connect_timeout` variable in the source database must be greater than or equal to 10.</li></ul></li>
<li>Requirements for binlog parameters:
<ul>
<li>The `binlog_format` variable in the source database must be set to `ROW`.</li>
<li>The `log_bin` variable in the source database must be set to `ON`.</li>
<li>The `binlog_row_image` variable in the source database must be set to `FULL`.</li>
<li>On v5.6 or above, if the `gtid_mode` variable in the source database is not `ON`, a warning will be triggered. We recommend you enable `gtid_mode`.</li>
<li>It is not allowed to set `do_db` and `ignore_db`.</li>
<li>If the source database is a slave database, the `log_slave_updates` variable must be set to `ON`.</li></ul></li>
<li>Foreign key dependency:
<ul>
<li>Foreign key dependency can be in either the `NO ACTION` or `RESTRICT` type.</li>
<li>During partial table migration, tables with foreign key dependency must be migrated.</li></ul></li></td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>The target database version must be above or equal to the source database version.</li>
<li>The space of the target database must be at least 1.2 times the size of the tables to be migrated in the source database.</li>
<li>The target database cannot have tables that conflict with the source database.</li>
<li>If the source database instance is a distributed database, you need to create sharded tables in the target database in advance; otherwise, the tables will become non-sharded tables after being migrated.</li></td></tr>
<tr> 
<td>Other requirements</td>
<td>The environment variable `innodb_stats_on_metadata` must be set to `OFF`.</td></tr>
</table>

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the region of the target database and click **Free Trial**. Currently, the DTS data migration feature is free of charge.
3. On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
>?If the connectivity test fails, troubleshoot and fix the problem as prompted and as instructed in [Troubleshooting Guide](https://intl.cloud.tencent.com/document/product/571/42552) and try again.
<table>
<thead><tr><th width="15%">Setting Type</th><th width="15%">Configuration Item</th><th width="70%">Description</th></tr></thead>
<tbody><tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td>Immediate execution: the task will be started immediately after the task verification is passed. Scheduled execution: you need to configure a task execution time and the task will be started automatically then.</td></tr>
<tr>
<td>Tag</td>
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=8>Source Database Settings</td>
<td>Source Database Type</td><td>Select **MySQL**.</td></tr>
<tr>
<td>Service Provider</td><td>Select **Others**.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, select **Public Network**.
<ul><li>Public Network: the source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: the source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connection</a>.</li>
<li>Database: the source database is a TencentDB database.</li>
<li>CCN: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li></ul>For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.</td></tr>
<tr>
<td>Region</td><td>The region where the source database resides is the outbound region of the DTS service. Select a region nearest to your self-built database.</td></tr>
<tr>
<td>Host Address</td><td>IP address or domain name for accessing the source MySQL database.</td></tr>
<tr>
<td>Port</td><td>Port for accessing the source MySQL database.</td></tr>
<tr>
<td>Account</td><td>Account of the source MySQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source MySQL database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>Select **TDSQL MySQL Edition**.</td></tr>
<tr>
<td>Access Type</td><td>Select **Database**.</td></tr>
<tr>
<td>Region</td><td>Select the region selected in the previous step.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target TDSQL for MySQL database.</td></tr>
<tr>
<td>Account.</td><td>Account of the target TDSQL for MySQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target TDSQL for MySQL database.</td></tr>
</tbody></table>
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
> ?
>- If you want to use a tool such as gh-ost and pt-osc to perform online DDL operations on a table during migration, you must select the entire database (or entire instance) where the table resides rather than only the table as the **migration object**; otherwise, the temporary table data generated by online DDL changes cannot be migrated to the target database.
>- If you want to rename a table (for example, rename table A table B) during migration, you must select the entire database (or entire instance) where table A resides rather than only table A as the **migration object**; otherwise, the system will report an error.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/deb994f49499b1ce50a17098e4d6dcd0.png"  style="margin:0;">
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select a type based on your scenario.<ul><li>Structural migration: structured data such as databases and tables in the database will be migrated.</li><li>Full migration:the entire database will be migrated.</li><li>Full + incremental migration: the entire database and subsequent incremental data will be migrated. If there are data writes during migration, and you want to smoothly migrate the data in a non-stop manner, select this option.</li></ul></td></tr>
<tr>
<td>Migration Object</td>
<td><ul><li>Entire instance: migrate the entire database instance excluding the system databases such as `information_schema`, `mysql`, `performance_schema`, and `sys`.</li>
<li>Specified objects: migrate specified objects.</li></ul> </td></tr>
<tr>
<td>Specify object</td>
<td>Select the objects to be migrated in **Source Database Object** and move them to the **Selected Object** box.</td></tr>
</tbody></table>
5. On the task verification page, verify the task. After the verification is passed, click **Start Task**.
If the verification failed, fix the problem as instructed in [Fix for Verification Failure](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
 - Failed: it indicates that a check item failed and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: it indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
6. Return to the data migration task list, and you can see that the task has entered the **Creating** status. After 1–2 minutes, the data migration task will be started.
   -  Select **Structural migration** or **Full migration**: once completed, the task will be stopped automatically.
   -  Select **Full + Incremental migration**: after full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
      - Select an appropriate time to manually complete the incremental data sync and perform business switch.
      - You can see that the migration task is in the incremental sync stage, and there is no latency. Stop writing the source database for several minutes.
      - When the source-target database data gap is 0 MB, and the source-target database time lag is 0s, manually complete the incremental sync.      
7. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Task Management](https://intl.cloud.tencent.com/document/product/571/42637).
8. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).

