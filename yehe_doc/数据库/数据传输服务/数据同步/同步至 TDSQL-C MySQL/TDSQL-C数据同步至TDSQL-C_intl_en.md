This document describes how to use the data sync feature of DTS to sync data from TDSQL-C for MySQL to TDSQL-C for MySQL.

The requirements for data sync in the following scenarios are the same as those for data sync from TDSQL-C for MySQL to TDSQL-C for MySQL. You can refer to this document for directions.

- Data sync from MySQL to TDSQL-C for MySQL
- Data sync from TDSQL-C for MySQL to MySQL

## Notes 
- During full data sync, DTS consumes certain source instance resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key.
- Sync is implemented without locks by default, during which no global lock (the FTWRL lock) is added to the source database, and only tables without a primary key are locked.
- During data sync, DTS will use the account that executes the sync task to write the system database `__tencentdb__` in the source database to record the data comparison information during the sync task.
  - To ensure that subsequent data problems can be located, the `__tencentdb__` system database in the source database will not be deleted after the sync task ends.
  - The `__tencentdb__` system database uses a single-threaded connection wait mechanism and occupies a very small space, about 0.01%–0.1% of the storage space of the source database; for example, if the source database is 50 GB, `__tencentdb__` will be about 5–50 MB. Therefore, it has almost no impact on the performance of the source database and will not preempt resources. 

## Prerequisites
- You have created a TDSQL-C for MySQL cluster as instructed in [Creating Cluster](https://intl.cloud.tencent.com/document/product/1098/40626).
- Permissions required of the source database:
```
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW VIEW,PROCESS,SELECT ON *.* TO 'account'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%'; 
FLUSH PRIVILEGES;
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.
- The source and target databases must meet the requirements for the sync feature and version as instructed in [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).

## Application restrictions
- Only basic tables and views can be synced, and objects such as functions, triggers, and stored procedures are not supported.
- When a view is exported, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as the sync user `user2`, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to the sync user `user2` (`[DEFINER = user2]`). If the view definition in the source database is too complex, the task may fail.
- If the source TDSQL-C database is a non-GTID instance, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with the following three database engines can be synced: InnoDB, MyISAM, and TokuDB. Tables with other engines will be skipped during sync by default.
- During incremental sync, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, sync will fail.
- If the source database is Alibaba Cloud ApsaraDB RDS for MySQL, then the tables to be synced on v5.6 must have a primary key, while tables on v5.7 and later are unrestricted. If the source database is Amazon RDS for MySQL, then the tables to be synced must have a primary key.
- If the binlog of the source database has a GTID hole, it may compromise the performance of the sync task and cause the task to fail.
- Scenarios that contain both DML and DDL statements in the same transaction are not supported and will trigger errors during task execution.
- Geometry data types are not supported and will trigger errors during task execution.
- The `ALTER VIEW` statement is not supported and will be skipped during sync.

## Operation limits
During the sync, do not perform the following operations; otherwise, the sync task will fail:
- Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
- Do not run distributed transactions in the source database.
- Do not write binlog data in the `STATEMENT` format into the source database.
- Do not clear binlogs in the source database.
- Do not delete the system table `__tencentdb__` during incremental sync. 

## Supported SQL operations
| Operation Type | Synchronizable SQL Operations               |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, and DELETE                                       |
| DDL      | CREATE DATABASE, DROP DATABASE, ALTER DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAME TABLE, CREATE VIEW, DROP VIEW, CREATE INDEX, and DROP INDEX<br/><dx-alert infotype="explain" title="Note">DDL statements involving partitions cannot be synced.</dx-alert> |

## Environment requirements
<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<ul><li>The source and target databases can be connected.</li>
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
<li>On TDSQL-C 5.6 or later, if the `gtid_mode` variable is not `ON`, an alarm will be triggered. We recommend you enable `gtid_mode`.</li>
<li>It is not allowed to set `do_db` and `ignore_db`.</li>
<li>If the source instance is a replica database, the `log_slave_updates` variable must be set to `ON`.</li>
   <li>We recommend you retain the binlog of the source database for at least three days; otherwise, the task cannot be resumed from the checkpoint and will fail.</li>
  </ul></li>
<li>Foreign key dependency:
<ul>
<li>Foreign key dependency can be set to only one of the following two types: `NO ACTION` and `RESTRICT`.</li>
<li>During partial table sync, tables with foreign key dependency must be migrated.</li>
</ul></li></td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>The target database version must be later than or equal to the source database version.</li>
<li>The target database must have sufficient storage space. If you select **Full data initialization** as the initialization type, the target database space must be at least 1.2 times the space of databases/tables to be synced in the source database.</li>
<li>The target database cannot have sync objects such as tables and views with the same name as those in the source database.</li>
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
<td>Source Instance Type</td><td>Select TDSQL-C for MySQL, which cannot be changed once configured.</td></tr>
<tr>
<td>Source Instance Region</td><td>Select the source instance region, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Type</td><td>Select TDSQL-C for MySQL, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Region</td><td>Select the target instance region, which cannot be changed once configured.</td></tr>
<tr>
<td>Specification</td><td>Select a specification based on your business needs. The higher the specification, the higher the performance.</td></tr>
</tbody></table>
2. After successful purchase, return to the [data sync list](https://console.cloud.tencent.com/dts/replication), and you can see the newly created data sync task. You need to configure it before you can use it.
3. In the data sync list, click **Configure** in the **Operation** column to enter the sync task configuration page.
4. On the sync task configuration page, configure the source and target instances and their accounts and passwords, test the connectivity, and click **Next**.
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
<td>Select a type based on your actual conditions. In this document, select **Database**.
<ul>
<li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li><li>VPC: The source and target databases are both deployed in Tencent Cloud <a href="https://intl.cloud.tencent.com/document/product/215">VPCs.</a>.</li></ul>For a third-party cloud database, you can select **Public Network** generally or select **VPN Access**, **Direct Connect**, or **CCN** based on your actual network conditions. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.</td></tr>
<tr>
<td>Instance ID</td><td>Instance ID of the source database.</td></tr>
<tr>
<td>Account</td><td>Account of the source database.</td></tr>    
<tr>
<td>Password</td><td>Password of the source database.</td></tr>       
<tr>
<td rowspan=6 >Target Instance Settings</td>
<td>Target Instance Type</td><td>Select the target database type, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Instance Region</td><td>Select the target database region, which cannot be changed once configured.</td></tr>
<tr>
<td>Access Type</td><td>Select the access type of the target database.</td></tr>
<tr>
<td>Instance ID</td><td>Instance ID of the target database.</td></tr>
<tr>
<td>Account</td><td>Account of the target database.</td></tr>    
<tr>
<td>Password</td><td>Password of the target database.</td></tr>
</tbody></table>
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
>? 
>- If you only select **Full data initialization** for **Initialization Type**, the system will assume by default that you have created the table structures in the target database and will neither migrate table structures nor check whether the source and target databases have tables with the same name. Therefore, if you select **Precheck and report error** for **If Target Already Exists**, the precheck and error reporting feature won't take effect.
>- If you select **Full data initialization** only, you need to create the table structures in the target database in advance.
>- If you want to rename a table (for example, rename table A table B) during sync, you must select the entire database (or entire instance) where table A resides rather than only table A as the **sync object**; otherwise, the system will report an error.
>
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Data Initialization Option</td>
<td>Initialization Type</td>
<td><ul><li>Structure initialization: Table structures in the source instance will be initialized into the target instance before the sync task runs.<li>Full data initialization: Data in the source instance will be initialized into the target database before the sync task runs. Both options are selected by default, and you can deselect them as needed.</td></tr>
<tr>
<td>If Target Already Exists</td>
<td><ul><li>Precheck and report error: If a table with the same name exists in both the source and target databases, an error will be reported, and the task will stop.<li>Ignore and execute: Full and incremental data will be directly added to tables in the target instance.</td></tr>
<tr>
<td rowspan=2>Data Sync Option</td>
<td>Conflict Resolution Method</td>
<td><ul><li>Report: If a primary key conflict is found during data sync, an error will be reported, and the data sync task will be paused.<li>Ignore: If a primary key conflict is found during data sync, the primary key record in the target database will be retained.<li>Overwrite: If a primary key conflict is found during data sync, the primary key record in the source database will overwrite that in the target database.</td></tr>
<tr>
<td>SQL Type</td><td>Supported operations include INSERT, UPDATE, DELETE, and DDL. If you select **Custom DDL**, you can select different DDL statement sync policies as needed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/571/47342">Setting SQL Filter Policy</a>.</td></tr>
<tr>
<td rowspan=2>Sync Object Option</td>
<td>Database and Table Objects of Source Instance</td><td>Select the objects to be synced. You can select databases, tables, and views.</td></tr>
<tr>
<td>Selected Object</td><td><ul><li>Database/Table mapping (renaming) is supported. Hover over a database or table name, click the displayed **Edit** icon, and enter a new name in the pop-up window.</li><li>When advanced objects are selected for sync, we recommend you not rename databases/tables; otherwise, sync of the advanced objects may fail.</li><li>Online DDL temp tables can be synced (through tools such as gh-ost or pt-online-schema-change). Click **Edit** of a table and select a temp table name in the pop-up window. For more information, see <a href="https://intl.cloud.tencent.com/document/product/571/48486">Syncing Online DDL Temp Table</a>.</li></ul></td></tr>
</tbody></table>
6. On the **Verify task** page, complete the verification. After all check items are passed, click **Start Task**.
If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
 - Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
7. Return to the data sync task list, and you can see that the task has entered the **Running** status. 
>?You can click **More** > **Stop** in the **Operation** column to stop a sync task. You need to ensure that data sync has been completed before stopping the task.
>
8. (Optional) You can click a task name to enter the task details page and view the task initialization status and monitoring data.

