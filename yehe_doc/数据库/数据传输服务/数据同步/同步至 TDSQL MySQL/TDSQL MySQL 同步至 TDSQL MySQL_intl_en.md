This document describes how to use the data sync feature of DTS to sync data from TDSQL for MySQL to TDSQL for MySQL.

The requirements for data sync in the following scenarios are the same as those for data sync from TDSQL for MySQL to TDSQL for MySQL. You can refer to this document for directions.
- Data sync from TDSQL for MySQL to TencentDB for MariaDB
- Data sync from TDSQL for MySQL to TencentDB for MySQL 
- Data sync from MySQL/MariaDB/Percona to TDSQL for MySQL (source database types can be self-built MySQL/MariaDB/Percona or TencentDB for MySQL/MariaDB)


## Notes
- During full data sync, DTS consumes certain source instance resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key.
- During data sync, DTS will use the account that executes the sync task to write the system database `__tencentdb__` in the source database to record the data comparison information during the sync task.
  - To ensure that subsequent data problems can be located, the `__tencentdb__` system database in the source database will not be deleted after the sync task ends.
  - The `__tencentdb__` system database uses a single-threaded connection wait mechanism and occupies a very small space, about 0.01%–0.1% of the storage space of the source database; for example, if the source database is 50 GB, `__tencentdb__` will be about 5–50 MB. Therefore, it has almost no impact on the performance of the source database and will not preempt resources. 

## [Prerequisites](id:qttj)
- The source and target databases must meet the requirements for the sync feature and version as instructed in [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).
- Permissions required of the source database:
```sql
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SELECT ON *.* TO 'migration account'@'%' IDENTIFIED BY 'migration password';
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%'; 
FLUSH PRIVILEGES;
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Application restrictions
- Only basic tables can be synced, and objects such as views, functions, triggers, and stored procedures are not supported. 
- If the source MySQL database is a non-GTID instance, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with the InnoDB database engine can be synced. Tables with other engines will trigger an error during task verification.
- Correlated data objects must be synced at the same time; otherwise, sync will fail.
- During incremental sync, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, sync will fail.
- Two-level partitioned tables as described in [Subpartitioning](https://intl.cloud.tencent.com/document/product/1042/33361) cannot be synced. If they are included in the synced tables, the task will report an error and stop.
- If TDSQL for MySQL (MariaDB) is used as the source or target database, two-way sync is not supported.
- The TDSQL sync feature adopts a row-level concurrency policy to speed up the incremental sync. Therefore, during the incremental sync, intermediate values of transactions may be observed for a very short period of time in the target database, but the data in the source and target databases will remain consistent eventually. 
- Currently, the primary key conflict resolution policy can only be **Overwrite**. For primary key data conflicts in the incremental sync phase, conflict overwrite will be performed directly. However, the task will report an error for conflicts during full data initialization.
- Scenarios that contain both DML and DDL statements in the same transaction are not supported and will trigger errors during task execution.
- Geometry data types are not supported and will trigger errors during task execution.

## Operation restrictions
During the sync, do not perform the following operations; otherwise, the sync task will fail:
- Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
- Do not run distributed transactions in the source database.
- Do not write binlog data in the `STATEMENT` format into the source database.
- Do not clear binlogs in the source database.
- Do not delete the system table `__tencentdb__` during incremental sync. 

## Synchronizable SQL operations
| Operation Type | SQL Statements                                              |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, and DELETE                                       |
| DDL      | CREATE DATABASE, DROP DATABASE, ALTER DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAME TABLE, CREATE INDEX, DROP INDEX<br/><dx-alert infotype="explain" title="Note">DDL statements involving partitions cannot be synced.</dx-alert> |

## Environment requirements
<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<li>The source and target databases can be connected.</li>
<ul>
<li>Requirements for the instance parameters:
<ul>
<li>The `server_id` parameter in the source database must be set manually and cannot be 0.</li>
<li>`row_format` for the source databases/tables cannot be set to `FIXED`.</li>
<li>The values of the `lower_case_table_names` variable in both the source and target databases must be the same.</li>
<li>The `connect_timeout` variable in the source database must be greater than or equal to 10.</li></ul></li>
<li>Requirements for binlog parameters:
<ul>
<li>The `log_bin` variable in the source database must be set to `ON`.</li>
<li>The `binlog_format` variable in the source database must be set to `ROW`.</li>
<li>The `binlog_row_image` variable in the source database must be set to `FULL`.</li>
<li>On MySQL 5.6 or later, if the `gtid_mode` variable is not `ON`, an alarm will be triggered. We recommend you enable `gtid_mode`.</li>
<li>It is not allowed to set `do_db` and `ignore_db`.</li>
<li>If the source instance is a replica database, the `log_slave_updates` variable must be set to `ON`.</li>
   <li>We recommend you retain the binlog of the source database for at least three days; otherwise, the task cannot be resumed from the checkpoint and will fail.</li>
  </ul></li>
<li>Foreign key dependency:
<ul>
<li>Foreign key dependency can be set to only one of the following two types: `NO ACTION` and `RESTRICT`.</li>
<li>During partial table sync, tables with foreign key dependency must be migrated.</li>
</ul>
</li>
</td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>If the target database is a distributed database, we recommend you manually create a partitioned table and plan the shardkey in advance; otherwise, DTS will create a table in the target database based on the table style of the source database. If the source database is a standalone instance, the target database will be created as a single table.</li>
<li>The target database version must be later than or equal to the source database version.</li>
<li>The target database must have sufficient storage space. If you select **Full data initialization** as the initialization type, the target database space must be at least 1.2 times the space of databases/tables to be synced in the source database.</li>
<li>The `max_allowed_packet` parameter of the target database must be set to 4 MB or above.</li></td></tr>
<tr> 
<td>Other requirements</td>
<td>The environment variable `innodb_stats_on_metadata` must be set to `OFF`.</td></tr>
</table>

## Directions
1. Log in to the [data sync purchase page](https://buy.intl.cloud.tencent.com/replication), select appropriate configuration items, and click **Buy Now**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Billing Mode</td><td>Pay-as-you-go billing is supported.</td></tr>
<tr>
<td>Source Instance Type</td><td>Select TDSQL for MySQL, which cannot be changed once configured.</td></tr>
<tr>
<td>Source Instance Region</td><td>Select the source instance region, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Type</td><td>Select TDSQL for MySQL, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Region</td><td>Select the target instance region, which cannot be changed once configured.</td></tr>
<tr>
<td>Specification</td><td>Currently, only the Standard Edition is supported</td></tr>
</tbody></table>
2. After successful purchase, return to the [data sync list](https://console.cloud.tencent.com/dts/replication), and you can see the newly created data sync task. You need to configure it before you can use it.
3. In the data sync list, click **Configure** in the **Operation** column to enter the sync task configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/446672e7198110da07be81e29885d151.png)
4. On the sync task configuration page, configure the source and target instances and their accounts and passwords, test the connectivity, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/4e09c5e94a31ae02012db00bcfadbd87.png)
<table>
<thead><tr><th width="10%">Category</th><th width="15%">Parameter</th><th width="75%">Description</th></tr></thead>
<tbody><tr>
<td rowspan=2 >Task Configuration</td>
<td>Task Name</td>
<td>DTS will automatically generate a task name, which is customizable.</td></tr>
<tr>
<td>Running Mode</td><td>Immediate execution and scheduled execution are supported.</td></tr>
<tr>
<td rowspan=6 >Source Instance Settings</td>
<td>Source Instance Type</td>
<td>Select the TencentDB instance type selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>Select the TencentDB instance region selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Access Type</td>
<td>Select **Database**, indicating that the source instance is a TencentDB instance.</td></tr>
<tr>
<td>Instance ID</td>
<td>Source instance ID.</td></tr>
<tr>
<td>Account</td>
<td>Source instance account.</td></tr>
<tr>
<td>Password</td>
<td>Source instance password.</td></tr>
<tr>
<td rowspan=6 >Target Instance Settings</td>
<td>Target Instance Type</td><td>Select the target database type, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Region</td><td>Select the target database region, which cannot be changed once configured.</td></tr>
<tr>
<td>Access Type</td><td>Select the access type of the target database.</td></tr>
<tr>
<td>Instance ID</td><td>Target instance ID.</td></tr>
<tr>
<td>Account</td><td>Target instance account.</td></tr>
<tr>
<td>Password</td><td>Target instance password.</td></tr>
</tbody></table>
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
>?
>- If you want to use a tool such as gh-ost and pt-osc to perform online DDL operations on a table during sync, you must select the entire database (or entire instance) where the table resides rather than only the table as the **sync object**; otherwise, the temporary table data generated by online DDL changes cannot be synced to the target database.
>- If you want to rename a table (for example, rename table A table B) during sync, you must select the entire database (or entire instance) where table A resides rather than only table A as the **sync object**; otherwise, the system will report an error.
>
![](https://qcloudimg.tencent-cloud.cn/raw/367d16f2af9fd6b08e9b81632a2951b8.png)
<strong>Database/Table mapping</strong>: Hover over the right side of a selected object, and the **Edit** icon will be displayed. Click it and then enter a mapping name in the pop-up window.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d8260ec27667ef8fadcf32ae9e41e3e.png" style="zoom:70%;" />
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Data Initialization Option</td>
<td>Initialization Type</td>
<td><ul><li>Structure initialization: Table structures in the source instance will be initialized into the target instance before the sync task runs.</li><li>Full data initialization: Data in the source instance will be initialized into the target instance before the sync task runs. </li></ul>Both options are selected by default, and you can deselect them as needed. If you select **Full data initialization**, you need to create the table structure in the target database in advance.
</ul></td></tr>
<tr>
<td>If Target Already Exists</td>
<td><ul><li>Precheck and report error: If a table with the same name exists in both the source and target databases, an error will be reported, and the task will stop.<li>Ignore and execute: Full and incremental data will be directly added to tables in the target instance.</td></tr>
<tr>
<td rowspan=2>Data Sync Option</td>
<td>Conflict Resolution Method</td>
<td>Overwrite: If a primary key conflict is found during data sync, the primary key of the source database will overwrite that of the target database.</td></tr>
<tr>
<td>SQL Type</td><td>The following operations are supported: INSERT, DELETE, UPDATE, and DDL.</td></tr>
<tr>
<td rowspan=2>Sync Object Option</td>
<td>Database and Table Objects of Source Instance</td><td>Select the objects to be synced. You can select databases and tables.</td></tr>
<tr>
<td>Selected Object</td><td>It displays the selected sync objects, and database/table mapping is supported.</td></tr>
</tbody></table>
6. On the **Verify task** page, complete the verification. After all check items are passed, click **Start Task**.
    If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
 - Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
![](https://qcloudimg.tencent-cloud.cn/raw/99e53691dc68b1a987424a3a91ada555.png)
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.
>?You can click **More** > **Stop** in the **Operation** column to stop a sync task. You need to ensure that data sync has been completed before stopping the task.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a14d84281ab739bfba84a61b2e09fa79.png)
8. (Optional) You can click a task ID to enter the task details page and view the task initialization status and monitoring data.

