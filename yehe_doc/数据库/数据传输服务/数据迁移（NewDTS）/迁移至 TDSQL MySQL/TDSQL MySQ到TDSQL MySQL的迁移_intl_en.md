This document describes how to use the data migration feature of DTS to migrate data from TDSQL for MySQL to TDSQL for MySQL.

The requirements for data migration in the following scenarios are the same as those for data migration from TDSQL for MySQL to TDSQL for MySQL. You can refer to this document for directions.

- Data migration from TDSQL for MySQL to TencentDB for MariaDB
- Data migration from TDSQL for MySQL to TencentDB for MySQL

## Notes
- During full data migration, DTS consumes certain source instance resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- Migration is implemented without locks by default, during which no global lock (the FTWRL lock) is added to the source database, and only tables without a primary key are locked.
- When you [create a data consistency check task](https://intl.cloud.tencent.com/document/product/571/42724), DTS will use the account that executes the migration task to write the system database `__tencentdb__` in the source database to record the data comparison information during the migration task.
  - To ensure that subsequent data problems can be located, the `__tencentdb__` system database in the source database will not be deleted after the migration task ends.
  - The `__tencentdb__` system database uses a single-threaded connection wait mechanism and occupies a very small space, about 0.01%–0.1% of the storage space of the source database; for example, if the source database is 50 GB, `__tencentdb__` will be about 5–50 MB. Therefore, it has almost no impact on the performance of the source database and will not preempt resources. 

## Prerequisites
- You have created a TDSQL for MySQL instance as instructed in [Creating Instances](https://intl.cloud.tencent.com/document/product/1042/33336).
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all the preparations as instructed in [Overview](https://intl.cloud.tencent.com/document/product/571/42652).
- You need to create a `__tencentdb__` database in advance in the source TDSQL for MySQL database.
- You need to have the permissions of the source database.
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT SELECT,RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
// If the source database is a TDSQL for MySQL database, you need to submit a ticket to authorize `RELOAD`; otherwise, you can authorize by referring to the sample code
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, INDEX, ALTER, CREATE ON `__tencentdb__`.* TO 'migration account'@'%';
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.


## Application restrictions
- Only basic tables can be migrated, while objects such as views, functions, triggers, and stored procedures cannot.
- System tables and user information such as `information_schema`, `sysdb`, `test`, `sys`, `performance_schema`, `__tencentdb__`, and `mysql` cannot be migrated.
- Only data with the InnoDB database engine can be migrated. Tables with other engines will be skipped during migration by default.
- Correlated data objects must be migrated at the same time; otherwise, migration will fail.
- During incremental migration, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, the migration will fail.
- Two-level partitioned tables as described in [Subpartitioning](https://intl.cloud.tencent.com/document/product/1042/33361) cannot be migrated.
   - During migration from TDSQL for MySQL to MySQL/MariaDB, if a two-level partitioned table is encountered, the task will report an error.
   - During migration from TDSQL for MySQL to TDSQL for MySQL, if the migrated databases/tables contain two-level partitioned tables, such partitioned table will be skipped. If the entire database or instance is migrated, and a two-level partitioned table is encountered, the task will report an error and pause.
- Scenarios that contain both DML and DDL statements in the same transaction are not supported and will trigger errors during task execution.
- Geometry data types are not supported and will trigger errors during task execution.

## Operation limits
- During migration, do not perform the following operations; otherwise, the migration task will fail:
  - Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
  - Do not run distributed transactions in the source database.
  - Do not write binlog data in the `STATEMENT` format into the source database.
  - Do not clear binlogs in the source database.
  - Do not delete the system table `__tencentdb__` during incremental migration. 
- If you only perform full data migration, do not write new data into the source instance during migration; otherwise, the data in the source and target instances will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.
- During incremental migration, you cannot add new shards or adjust the shard specification in the source database; otherwise, the migration task will not sync the data in the new shards or will report an error and pause. If you need to maintain incremental sync for a long time and add or adjust shards in the source database, see [Sync from TDSQL for MySQL to TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/571/47350).

## Supported SQL operations
| Operation Type | Synchronizable SQL Operations               |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, and REPLACE                              |
| DDL      | Table: CREATE TABLE, ALTER TABLE, DROP TABLE, and TRUNCATE TABLE<br>View: CREATE VIEW and DROP VIEW<br>Index: CREATE INDEX and DROP INDEX<br>Database: CREATE DATABASE, ALTER DATABASE, and DROP DATABASE |

## Environment requirements
>?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551); otherwise, wait for the system verification to complete and fix the problem according to the error message.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<li>The source and target databases can be connected.</li>
<ul>
<li>Requirements for the instance parameters:
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
<li>On v5.6 or later, if the `gtid_mode` variable in the source database is not `ON`, a warning will be triggered. We recommend you enable `gtid_mode`.</li>
<li>It is not allowed to set `do_db` and `ignore_db`.</li>
<li>If the source instance is a replica database, the `log_slave_updates` variable must be set to `ON`.</li>
  <li>We recommend you retain the binlog of the source database for at least three days; otherwise, the task cannot be resumed from the checkpoint and will fail.</li>
  </ul></li>
<li>Foreign key dependency:
<ul>
<li>Foreign key dependency can be in either the `NO ACTION` or `RESTRICT` type.</li>
<li>During partial table migration, tables with foreign key dependency must be migrated.</li></ul></li></td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>If the target database is a distributed database, we recommend you manually create a partitioned table and plan the shardkey in advance; otherwise, DTS will create a table in the target database based on the table style of the source database. If the source database is a standalone instance, the target database will be created as a single table.</li>
<li>The target database version must be later than or equal to the source database version.</li>
<li>The space of the target database must be at least 1.2 times the size of the tables to be migrated in the source database.</li>
<li>The target database cannot have tables that conflict with the source database.</li> 
</td></tr>
<tr> 
<td>Other requirements</td>
<td>The environment variable `innodb_stats_on_metadata` must be set to `OFF`.</td></tr>
</table>

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the types, regions, and specifications of the source and target instances and click **Buy Now**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Source Instance Type</td>
<td>Select the source database type, which cannot be changed after purchase. In this scenario, select **TDSQL for MySQL**.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>Select the source database region.</td></tr>
<tr>
<td>Target Instance Type</td>
<td>Select the target database type, which cannot be changed after purchase. In this scenario, select **TDSQL for MySQL**.</td></tr>
<tr>
<td>Target Instance Region</td>
<td>Select the target database region.</td></tr>
<tr>
<td>Specification</td>
<td>Select the specification of the migration link based on your business conditions.</td></tr>
</tbody></table>
3. On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
>?If the connectivity test fails, troubleshoot as prompted or as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552) and try again.
<table>
<thead><tr><th width="15%">Setting Type</th><th width="15%">Configuration Item</th><th width="70%">Description</th></tr></thead>
<tbody><tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a task name that is easy to identify.</td></tr>
<tr>
<td>Running Mode</td>
<td>Immediate execution: The task will be started immediately after the task verification is passed. Scheduled execution: You need to configure a task execution time and the task will be started automatically then.</td></tr>
<tr>
<td>Tag</td>
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=6>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The source database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select **Database**.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the source database.</td></tr>
<tr>
<td>Account</td><td>Account of the source TDSQL for MySQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source TDSQL for MySQL database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select **Database**.</td></tr>
<tr>
<td>Database Instance</td><td>Select the target TDSQL for MySQL instance ID.</td></tr>
<tr>
<td>Account</td><td>Account of the target TDSQL for MySQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target TDSQL for MySQL database.</td></tr>
</tbody></table>
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
> ?
>- If you want to use a tool such as gh-ost and pt-osc to perform online DDL operations on a table during migration, you must select the entire database (or entire instance) where the table resides rather than only the table as the **migration object**; otherwise, the temporary table data generated by online DDL changes cannot be migrated to the target database.
>- If you want to rename a table (for example, rename table A table B) during migration, you must select the entire database (or entire instance) where table A resides rather than only table A as the **migration object**; otherwise, the system will report an error.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/41078c7405441ed5ae8809527561a306.png" style="zoom:80%;" />
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select a type based on your scenario. <ul><li> Structural migration: Structured data of databases and tables will be migrated. </li><li>Full migration: The entire database will be migrated. The migrated data will include only the existing data from the source database when the task is started, not incremental data written to the source database after the task is started. </li><li>Full + Incremental migration: The migrated data will include the existing data from the source database when the task is started as well as the incremental data written to the source database after the task is started. If there are data writes to the source database during migration, and you want to smoothly migrate the data in a non-stop manner, select this type.</li></ul></td></tr>
<tr>
<td>Migration Object</td>
<td><ul><li>Entire instance: Migrate the entire database instance excluding the system databases such as `information_schema`, `mysql`, `performance_schema`, and `sys`.</li>
<li>Specified objects: Migrate specified objects.</li></ul> </td></tr>
<tr>
<td>Specified objects</td>
<td>Select the objects to be migrated in **Source Database Object** and move them to the **Selected Object** box.</td></tr>
</tbody></table>
5. On the task verification page, verify the task. After the verification is passed, click **Start Task**.
If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
 - Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
6. Return to the data migration task list, and you can see that the task has entered the **Creating** status. After 1–2 minutes, the data migration task will be started.
   -  Select **Structural migration** or **Full migration**: once completed, the task will be stopped automatically.
   -  Select **Full + Incremental migration**: After full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
      - Manually complete incremental data sync and business switchover at appropriate time.
      - Check whether the migration task is in the incremental sync stage without any lag. If so, stop writing data to the source database for a few minutes.
      - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 seconds.      
7. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637).
8. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).

