This document describes how to use the data sync feature of DTS to sync data from MySQL to TencentDB for MySQL.

## Notes
- During full data sync, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key.

## [Prerequisites](id:qttj)
- The source and target databases must meet the requirements for the sync feature and version as instructed in [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).
- Permissions required of the source database:
```sql  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SELECT ON *.* TO 'migration account'@'%' IDENTIFIED BY 'migration password';
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%'; // If the source database is a TencentDB database, you need to grant the `__tencentdb__` permission
FLUSH PRIVILEGES;
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Application Restrictions
- Only basic tables and views can be synced, and objects such as functions, triggers, and stored procedures are not supported. 
- When a view is exported, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as the sync user `user2`, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to the sync user `user2` (`[DEFINER = user2]`).
- If the source MySQL database is a non-GTID database, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with the following three database engines can be synced: InnoDB, MySIAM, and TokuDB. Tables with other engines will be skipped during synching by default.
- Correlated data objects need to be synced together; otherwise, sync will fail. Common correlations include table reference by views, view reference by views, view/table reference by stored procedures/functions/triggers, and tables correlated through primary/foreign keys.
- During incremental sync, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, sync will fail.
- If the source database is Alibaba Cloud ApsaraDB RDS for MySQL, then the tables to be synced on v5.6 must have a primary key, while tables on v5.7 and later are unrestricted. If the source database is Amazon RDS for MySQL, then the tables to be synced must have a primary key.

## Operation Restrictions
During the sync, do not perform the following operations; otherwise, the sync task will fail:
- Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
- Do not run distributed transactions in the source database.
- Do not write binlog data in the `STATEMENT` format into the source database.
- Do not clear binlogs in the source database.
- Do not delete the system table `__tencentdb__` during incremental sync. 

## Synchronizable SQL Operations

| Operation Type | SQL Statements                                              |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, and DELETE                                       |
| DDL      | CREATE DATABASE, DROP DATABASE, ALTER DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAME TABLE, CREATE VIEW, DROP VIEW, CREATE INDEX, and DROP INDEX |

## Environment Requirements

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<li>The source and target databases can be connected.</li>
<ul>
<li>Requirements for the database parameters:
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
<li>On MySQL 5.6 or above, if the `gtid_mode` variable is not `ON`, an alarm will be triggered. We recommend you enable `gtid_mode`.</li>
<li>It is not allowed to set `do_db` and `ignore_db`.</li>
<li>If the source database is a slave database, the `log_slave_updates` variable must be set to `ON`.</li></ul></li>
<li>Foreign key dependency:
<ul>
<li>Foreign key dependency can be set to only one of the following three types: `NO ACTION`, `RESTRICT`, and `CASCADE`.</li>
<li>During partial table sync, tables with foreign key dependency must be migrated.</li></ul></li></td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>The target database version must be above or equal to the source database version.</li>
<li>The target database must have sufficient storage space. If you select **Full data initialization** as the initialization type, the target database space must be at least 1.2 times the space of databases/tables to be synced in the source database.</li>
<li>The target database cannot have sync objects such as tables and views with the same name as those in the source database.</li>
<li>The `max_allowed_packet` parameter of the target database must be set to 4 MB or above.</li></td></tr>
<tr> 
<td>Other requirements</td>
<td>The environment variable `innodb_stats_on_metadata` must be set to `OFF`.</td></tr>
</table>

## Directions
1. Log in to the [data sync purchase page](https://buy.cloud.tencent.com/dts), select the corresponding configuration items, and click **Buy Now**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Billing Mode</td><td>Monthly subscription and pay-as-you-go billing modes are supported. Currently, the data sync feature is free of charge, and you will receive notifications by email and Message Center one month before the billing officially starts.</td></tr>
<tr>
<td>Source Database Type</td><td>Select MySQL (including TencentDB for MySQL and self-built MySQL).</td></tr>
<tr>
<td>Source Database Region</td><td>Select the source database region.</td></tr>
<tr>
<td>Target Database Type</td><td>Select MySQL (including TencentDB for MySQL and self-built MySQL).</td></tr>
<tr>
<td>Target Database Region</td><td>Select the target database region.</td></tr>
<tr>
<td>Sync Task Specification</td><td>Currently, only the Standard Edition is supported</td></tr>
</tbody></table>
2. After successful purchase, return to the [data sync list](https://console.cloud.tencent.com/dts/replication), and you can see the newly created data sync task. You need to configure it before you can use it.
3. In the data sync list, click **Configure** in the **Operation** column to enter the sync task configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/334132cfea2b813ae8d28a46f8ef791a.png)
4. On the sync task configuration page, configure the source and target databases and their accounts and passwords, test the connectivity, and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e07286b280ea9a7c5de5cea619f760de.png"  style="margin:0;">
<table>
<thead><tr><th width="10%">Category</th><th width="15%">Parameter</th><th width="75%">Description</th></tr></thead>
<tbody><tr>
<td rowspan=2 >Task Configuration</td>
<td>Task Name</td>
<td>DTS will automatically generate a task name, which is customizable.</td></tr>
<tr>
<td>Running Mode</td><td>Immediate execution and scheduled execution are supported.</td></tr>
<tr>
<td rowspan=4 >Source Database Settings</td>
<td>Source Database Type</td>
<td>Select the TencentDB instance type selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Source Database Region</td>
<td>Select the TencentDB instance region selected during purchase, which cannot be changed once configured.</td></tr>
<tr>
<td>Service Provider</td>
<td>Others (including TencentDB for MySQL and self-built MySQL), AWS, and Alibaba Cloud are supported.</td></tr>
<tr>
<td>Access Type</td>
<td>If **Other Cloud Vendors** is selected as **Service Provider**, the access type can be public network; if **Others** is selected as **Service Provider**, you need to select an access type according to the database deployment conditions.<ul>
<li>Public Network: the source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: the source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connection</a>.</li>
<li>Database: the source database is a TencentDB database.</li>
<li>CCN: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li><li>VPC: the source and target databases are both deployed in Tencent Cloud <a href="https://intl.cloud.tencent.com/document/product/215">VPCs.</a>.</li></ul>For a third-party cloud database, you can select **Public Network** generally or select **VPC Access**, **Direct Connect**, or **CCN** based on your actual network conditions. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.</td></tr>
<tr>
<td rowspan=3 >Target Database Settings</td>
<td>Target Database Type</td><td>Select the target database type, which cannot be changed once configured.</td></tr>
<tr>
<td>Target Database Region</td><td>Select the target database region, which cannot be changed once configured.</td></tr>
<tr>
<td>Access Type</td><td>Select the access type of the target database.</td></tr>
</tbody></table>
<strong>Access type description</strong><br>In the settings of the source and target databases, you need to enter different parameters according to the access type as listed below:
<table>
<thead><tr><th>Service Provider</th><th>Access Type</th><th>Instance ID</th><th>CVM Instance</th><th>Host Address</th><th>Port</th><th>Account</th><th>Password</th></tr></thead>
<tbody><tr>
<td rowspan=4>Others</td><td>Database</td>
<td>&#10003;</td><td>×</td><td>×</td><td>×</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Self-Build on CVM</td><td>×</td><td>&#10003;</td><td>×</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Public Network</td><td>×</td><td>×</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>CCN</td><td>×</td><td>×</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>AWS</td>
<td>Public Network</td><td>×</td><td>×</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Alibaba Cloud</td>
<td>Public Network</td><td>×</td><td>×</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td></tr>
</tbody></table>
5. On the **Set sync options and objects** page, set the data initialization, data sync, and sync object options and click **Save and Go Next**.
>?
>- If you only select **Full data initialization** for **Initialization Type**, the system will assume by default that you have created the table structures in the target database and will neither migrate table structures nor check whether the source and target databases have tables with the same name. Therefore, if you select **Precheck and report error** for **If Target Already Exists**, the precheck and error reporting feature won't take effect.
>- If you select **Full data initialization** only, you need to create the table structures in the target database in advance.
>- If you want to use a tool such as gh-ost and pt-osc to perform online DDL operations on a table during sync, you must select the entire database (or entire instance) where the table resides rather than only the table as the **sync object**; otherwise, the temporary table data generated by online DDL changes cannot be synced to the target database.
>- If you want to rename a table (for example, rename table A to table B) during sync, you must select the entire database (or entire instance) where table A resides rather than only table A as the **sync object**; otherwise, the system will report an error.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/03141e48fcc271b029541b49a0cb1020.png"  style="margin:0;">
<strong>Database/Table mapping</strong>: hover over the right side of a selected object, and the **Edit** icon will be displayed. Click it and then enter a mapping name in the pop-up window.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7b0a6732dde12ecb286dbd596906a07d.png"  style="margin:0;">
<table>
<thead><tr><th>Category</th><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>Data Initialization Option</td>
<td>Initialization Type</td>
<td><ul><li>Structure initialization: table structures in the source database will be initialized into the target database before the sync task runs.<li>Full data initialization: data in the source database will be initialized into the target database before the sync task runs. Both options are selected by default, and you can deselect them as needed.</td></tr>
<tr>
<td>If Target Already Exists</td>
<td><ul><li>Precheck and report error: if a table with the same name exists in both the source and target databases, an error will be reported, and the task will stop.<li>Ignore and execute: full and incremental data will be directly added to tables in the target database.</td></tr>
<tr>
<td rowspan=2>Data Sync Option</td>
<td>Conflict Resolution Method</td>
<td><ul><li>Report: if a primary key conflict is found during data sync, an error will be reported, and the data sync task will be paused.<li>Ignore: if a primary key conflict is found during data sync, the primary key record in the target database will be retained.<li>Overwrite: if a primary key conflict is found during data sync, the primary key record in the source database will overwrite that in the target database.</td></tr>
<tr>
<td>SQL Type</td><td>The following operations are supported: INSERT, DELETE, UPDATE, and DDL.</td></tr>
<tr>
<td rowspan=2>Sync Object Option</td>
<td>Database and Table Objects of Source Database</td><td>Select the objects to be synced. You can select databases, tables, and views.</td></tr>
<tr>
<td>Selected Object</td><td>It displays the selected sync objects, and database/table mapping is supported.</td></tr>
</tbody></table>
6. On the task verification page, complete the verification. After all check items are passed, click **Start Task**.
    If the verification failed, fix the problem as instructed in [Fix for Verification Failure](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
 - Failed: it indicates that a check item failed and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: it indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
![](https://qcloudimg.tencent-cloud.cn/raw/27e959ca0ccff7ebf26b21291f5ad9f0.png)
7. Return to the data sync task list, and you can see that the task has entered the **Running** status.
>?You can click **More** > **Stop** in the **Operation** column to stop a sync task. You need to ensure that data sync has been completed before stopping the task.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ba40f40d5fc6893155c723358d74bc45.png)
8. (Optional) you can click a task name to enter the task details page and view the task initialization status and monitoring data.

