This document describes how to use DTS’s data migration feature to migrate data from MySQL to TencentDB for MySQL.

## Notes 
- During full data migration, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you migrate the data during off-peak hours.
- Full migration is implemented with tables locked, causing write operations to be blocked for a few seconds.

## Prerequisites
- You have created a [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/37785) instance.
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all [preparations](https://intl.cloud.tencent.com/document/product/571/42652).
- The source database must have the following permissions:
  - Migration of the entire instance:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%'; // If the source database is a TencentDB database, you need to grant the `__tencentdb__` permission  
GRANT SELECT ON *.* TO 'migration account';
```
  - Migration of specified objects:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%'; // If the source database is a TencentDB database, you need to grant the `__tencentdb__` permission  
GRANT SELECT ON `mysql`.* TO 'migration account'@'%';
GRANT SELECT ON database to be migrated.* TO 'migration account';
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Application Restrictions
- Only basic tables and views can be migrated, and objects such as functions, triggers, and stored procedures are not supported.
- System databases/tables and user information including `information_schema`, `sys`, `performance_schema`, `__cdb_recycle_bin__`, `__recycle_bin__`, `__tencentdb__`, and `mysql` cannot be migrated. After the migration is completed, if you want a view, stored procedure, or function in the target database to be called, you must grant the caller the read/write permissions. 
- When a view is exported, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as `user2` in the migration target, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to `user2` of the migration target (`[DEFINER = migration target user2]`).
- If the source MySQL database is a non-GTID database, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with InnoDB, MySIAM, and TokuDB database engines can be migrated. Other data table engines will be skipped by default during migration.
- Correlated data objects need to be migrated together; otherwise, migration will fail. Common correlations include table reference by views, view reference by views, view/table reference by stored procedures/functions/triggers, and tables correlated through primary/foreign keys.
- During incremental migration, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, the migration will fail.
- In migration without locks (the source database is Alibaba Cloud ApsaraDB RDS for MySQL 5.6, Alibaba Cloud PolarDB for MySQL 5.6, or Amazon RDS for MySQL, and the target database is TencentDB for MySQL), DDL operations are not supported during full migration.

## Operation Restrictions
- During the migration, do not perform the following operations; otherwise, the migration task will fail:
  - Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
  - Do not run distributed transactions in the source database.
  - Do not write binlog data in the `STATEMENT` format into the source database.
  - Do not clear binlogs in the source database.
  - Do not run DDL operations of changing the database/table structure during database/table structure migration or full migration.
  - Do not delete the system table `__tencentdb__` during incremental migration. 
- If you only perform full data migration, do not write new data into the source database during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

## Supported SQL Operations
| Operation Type | Supported SQL Operations                                              |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, and REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, and RENAME TABLE <br>VIEW: CREATE VIEW and DROP VIEW<br>INDEX: CREATE INDEX and DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, and DROP DATABASE |

## Environment Requirements
>?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Requirements for Check Items](https://intl.cloud.tencent.com/document/product/571/42552); otherwise, wait for the system verification to complete and fix the problem according to the error message.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<ul>
<li>The source and target databases can be connected.</li>
<li>The server where the source database resides has enough outbound bandwidth; otherwise, the migration speed will be affected.</li>
<li>Requirements for the database parameters:
<ul>
<li>The `server_id` parameter in the source database must be set manually and cannot be 0.</li>
<li>`row_format` for the source databases/tables cannot be set to `FIXED`.</li>
<li>The values of the `lower_case_table_names` variable in both the source and target databases must be the same.</li>
<li>The `connect_timeout` variable in the source database must be greater than or equal to 10.</li>
<li>We recommend you enable `skip-name-resolve` to reduce the possibility of connection timeout.</li></ul></li>
<li>Requirements for binlog parameters:
<ul>
<li>The `log_bin`variable in the source database must be set to `ON`.</li>
<li>The `binlog_format` variable in the source database must be set to `ROW`.</li>
<li>The `binlog_row_image` variable in the source database must be set to `FULL`.</li>
<li>On MySQL 5.6 or above, if the `gtid_mode` variable is not `ON`, an alarm will be triggered. We recommend you enable `gtid_mode`.</li>
<li>You cannot set filter conditions with `do_db` and `ignore_db`.</li>
<li>If the source database is a slave database, the `log_slave_updates` variable must be set to `ON`.</li>
</ul></li>
<li>Foreign key dependency:
<ul>
<li>Foreign key dependency can be set to only one of the following three types: `NO ACTION`, `RESTRICT`, and `CASCADE`.</li>
<li>During partial table migration, tables with foreign key dependency must be migrated.</li>
</ul></li>
<li>The migration precision of DTS for data in `FLOAT` type is 38 digits, and for data in `DOUBLE` type is 308 digits. You should check whether this meets your requirements.</li></ul></td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>The target database version must be above or equal to the source database version.</li>
<li>The size of the target database space must be at least 1.2 times that of the databases/tables to be migrated in the source database. (Full data migration will execute INSERT operations concurrently, causing some tables in the target database to generate data fragments. Therefore, after full migration is completed, the size of the tables in the target database may be larger than that in the source database.)</li>
<li>The target database cannot have migration objects such as tables and views with the same name as those in the source database.</li>
<li>The `max_allowed_packet` parameter of the target database must be set to 4 MB or above.</li></td></tr>
<tr> 
<td>Other requirements</td>
<td>The environment variable `innodb_stats_on_metadataw` must be set to `OFF`.</td></tr>
</table>

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the region of the target database and click **Free Trial**. Currently, the DTS data migration feature is free of charge.
![](https://qcloudimg.tencent-cloud.cn/raw/169060acf75d5ffaa309fe7f342c1746.png)
3. On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
>?If the connectivity test fails, troubleshoot and fix the problem as prompted and as instructed in [Troublehshooting Guide](https://intl.cloud.tencent.com/document/product/571/42552) and try again.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/62e0b79ff55a94357eed9611173037a3.png"  style="margin:0;">
<table>
<thead><tr><th width="10%">Setting Type</th><th width="20%">Configuration Item</th><th width="70%">Description</th></tr></thead>
<tbody>
<tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td><ul><li>Immediate execution: the task will be started immediately after the task verification is passed.</li><li>Scheduled execution: you need to configure a task execution time and the task will be started automatically then.</li></ul></td></tr>
<tr>
<td>Tag</td>
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=10>Source Database Settings</td>
<td>Source Database Type</td><td>Select your source database type. In this document, select **MySQL**.</td></tr>
<tr>
<td>Service Provider</td><td>Select **Others**.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, select **Direct Connect** or **VPN Access**.
<ul><li>Public Network: the source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: the source database is deployed in a <a href="intl.cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li>
<li>VPN Access: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connection</a>.</li>
<li>Database: the source database is a TencentDB database.</li>
<li>CCN: the source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</li></ul>For a third-party cloud database, you can select **Public Network** generally or select **VPC Access**, **Direct Connect**, or **CCN** based on your actual network conditions. For the preparations for different access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.</td></tr>
<tr>
<td>Region</td><td>The region where the source database resides is the outbound region of the DTS service. Select a region nearest to your self-built database.</td></tr>
<tr>
<td>VPC-Based Direct Connect Gateway/VPN Gateway</td><td>Only VPC-based Direct Connect gateway is supported. You need to confirm the network type associated with the gateway.<br>VPN Gateway: select a VPN Gateway instance.</td></tr>
<tr>
<td>VPC</td><td>Select a VPC and subnet associated with the VPC-based Direct Connect Gateway or VPN Gateway.</td></tr>
<tr>
<td>Host Address</td><td>IP address or domain name for accessing the source MySQL database.</td></tr>
<tr>
<td>Port</td><td>Port for accessing the source MySQL database.</td></tr>
<tr>
<td>Account</td><td>Account of the source MySQL database, which must have certain permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source MySQL database.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>Select **MySQL**.</td></tr>
<tr>
<td>Access Type</td><td>Select a type based on your scenario. In this document, select **Database**.</td></tr>
<tr>
<td>Region</td><td>Select the same region as in the source database settings.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target database.</td></tr>
<tr>
<td>Account.</td><td>Account of the target database, which must have certain permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target database.</td></tr>
</tbody></table>
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
>?
>- If you want to use a tool such as gh-ost and pt-osc to perform online DDL operations on a table during migration, you must select the entire database (or entire instance) where the table resides rather than only the table as the **migration object**; otherwise, the temporary table data generated by online DDL changes cannot be migrated to the target database.
>- If you want to rename a table (for example, rename table A table B) during migration, you must select the entire database (or entire instance) where table A resides rather than only table A as the **migration object**; otherwise, the system will report an error. 
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/7b9a8f1d46745de41304c21c5a9fa338.png"  style="margin:0;">
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
![](https://qcloudimg.tencent-cloud.cn/raw/f65181fc4ed621be17312324dc9de574.png)
6. Return to the data migration task list, and you can see that the task has entered the **Preparing** status. After 1–2 minutes, the data migration task will be started.
   - Select **Structural migration** or **Full migration**: once completed, the task will be stopped automatically.
   - Select **Full + Incremental migration**: after full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
      - Select an appropriate time to manually complete the incremental data sync and perform business switch.
      - You can see that the migration task is in the incremental sync stage, and there is no latency. Stop writing the source database for several minutes.
      - When the source-target database data gap is 0 MB, and the source-target database time lag is 0s, manually complete the incremental sync.
   ![](https://qcloudimg.tencent-cloud.cn/raw/eb6011194927699890f3edf52b84f026.png)
7. (Optional) If you want to view, delete, or perform other operations on a task, click the corresponding task and select the corresponding operation in the **Operation** column. For more information, see [Task Management](https://intl.cloud.tencent.com/document/product/571/42637).
8. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Overview](https://cloud.tencent.com/document/product/571/58660).
