## Overview

This document describes how to use the data migration feature of DTS to migrate data from a self-built database to a TencentDB database through CCN.

CCN can interconnect a VPC with another VPC or a local IDC. To use CCN access, you must establish cross-VPC and VPC-IDC interconnections through CCN in advance.

In this scenario, you have used CCN to interconnect the three networks of VPC-Guangzhou, VPC-Chengdu, and VPC-Shanghai, have a self-built database in Guangzhou, and plan to migrate the data in the source database in Guangzhou to the target database in Nanjing. VPC-Chengdu is selected as the **Accessed VPC**.

## Configuration Principles

When selecting CCN access, you need to connect the source database to the source of the DTS migration/sync linkage over CCN as follows: source database > accessed VPC > source of the migration/sync linkage, as shown in orange below.

<img src="https://qcloudimg.tencent-cloud.cn/raw/731aafbd4595e86f9a59ba173f0e4662.jpg" style="zoom:67%;" />

The accessed VPC and the source of the migration/sync linkage are interconnected as follows in the entire DTS task:

- The source of the migration/sync linkage is the network in the region of the source database selected during the task purchase, as shown below:
  The region of the source database selected during task purchase must be the same as the region of the accessed VPC; otherwise, the networks cannot be interconnected, and DTS will change the former to the latter.
  <img src="https://qcloudimg.tencent-cloud.cn/raw/be0a5f791aa2c827a7936d01bd48cc5f.png" style="zoom:50%;" />

- Accessed VPC: The accessed VPC refers to the VPC in CCN over which the migration/sync linkage is connected. It can be configured when you set the source and target databases as shown below:
  The accessed VPC and the VPC of the source database are interconnected over CCN.
  

## Notes 

- When DTS performs full data migration, it will occupy certain source instance resources, which may increase the load of the source instance and the database pressure. If your database has low configurations, we recommend that you migrate data during off-peak hours.
- Migration is implemented without locks by default, during which no global lock (the FTWRL lock) is added to the source database, and only tables without a primary key are locked.

## Prerequisites

- You have created a TencentDB for MySQL instance as instructed in [Creating MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37785).
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all preparations as instructed in [Overview](https://intl.cloud.tencent.com/document/product/571/42652).
- The source database must have the following permissions:
  - Migration of the entire instance:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%';  
GRANT SELECT ON *.* TO 'migration account';
```
  - Migration of specified objects:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%';  
GRANT SELECT ON `mysql`.* TO 'migration account'@'%';
GRANT SELECT ON database to be migrated.* TO 'migration account';
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Application Restrictions

- Basic tables, views, functions, triggers, stored procedures, and events can be migrated, while system tables such as `information_schema`, `sys`, `performance_schema`, `__cdb_recycle_bin__`, `__recycle_bin__`, `__tencentdb__`, and `mysql` cannot.
- When views, stored procedures, and functions are migrated, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as the migration account `user2`, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`) after the migration, and set the `DEFINER` in the target database to the migration account `user2` (`[DEFINER = migration account user2]`). If the view definition in the source database is too complex, the task may fail.
- If the source MySQL database is a non-GTID database, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with the following three database engines can be migrated: InnoDB, MyISAM, and TokuDB. Tables with other engines will be skipped during migration by default.
- Correlated data objects must be migrated together; otherwise, migration will fail. Common correlations include table reference by views, view reference by views, and tables correlated through primary/foreign keys.
- During incremental migration, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, the migration will fail.
- In migration without locks (the source database is Alibaba Cloud ApsaraDB RDS for MySQL 5.6, Alibaba Cloud PolarDB for MySQL 5.6, or Amazon RDS for MySQL, and the target database is TencentDB for MySQL), DDL operations are not supported during full migration.

## Operation Limits

- During migration, do not perform the following operations; otherwise, the migration task will fail:
  - Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
  - Do not run distributed transactions in the source database.
  - Do not write binlog data in the `STATEMENT` format into the source database.
  - Do not clear binlogs in the source database.
  - Do not run DDL operations of changing the database/table structure during database/table structure migration or full migration.
  - Do not delete the system table `__tencentdb__` during incremental migration. 
- If you only perform full data migration, do not write new data into the source instance during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

## Supported SQL Operations

| Operation Type | Supported SQL Operations                                              |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, and REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, and RENAME TABLE <br>VIEW: CREATE VIEW and DROP VIEW <br>INDEX: CREATE INDEX and DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, and DROP DATABASE |

## Environment Requirements

>?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552); otherwise, wait for the system verification to complete and fix the problem according to the error message.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<ul>
<li>The source and target databases can be connected.</li>
<li>The server where the source database resides must have enough outbound bandwidth; otherwise, the migration speed will be affected.</li>
<li>Requirements for the database parameters:
<ul>
<li>The `server_id` parameter in the source database must be set manually and cannot be 0.</li>
<li>`row_format` for the source databases/tables cannot be set to `FIXED`.</li>
<li>The values of the `lower_case_table_names` variable in both the source and target databases must be the same.</li>
<li>The `connect_timeout` variable in the source database must be greater than or equal to 10.</li>
<li>We recommend you enable `skip-name-resolve` to reduce the possibility of connection timeout.</li></ul></li>
<li>Requirements for binlog parameters:
<ul>
<li>The `log_bin` variable in the source database must be set to `ON`.</li>
<li>The `binlog_format` variable in the source database must be set to `ROW`.</li>
<li>The `binlog_row_image` variable in the source database must be set to `FULL`.</li>
<li>On MySQL 5.6 or later, if the `gtid_mode` variable is not `ON`, an alarm will be triggered. We recommend you enable `gtid_mode`.</li>
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
<li>The target database version must be equal to or later than the source database version.</li>
<li>The size of the target database space must be at least 1.2 times that of the databases/tables to be migrated in the source database. (Full data migration will execute INSERT operations concurrently, causing some tables in the target database to generate data fragments. Therefore, after full migration is completed, the size of the tables in the target database may be larger than that in the source database.)</li>
<li>The target database cannot have migration objects such as tables and views with the same name as those in the source database.</li>
<li>The `max_allowed_packet` parameter of the target database must be set to 4 MB or above.</li></td></tr>
<tr> 
<td>Other requirements</td>
<td>The environment variable `innodb_stats_on_metadata` must be set to `OFF`.</td></tr>
</table>

## Directions

### Configuring the network interconnection through CCN

Establish interconnections as instructed in [Connecting Network Instances Under the Same Account](https://intl.cloud.tencent.com/document/product/1003/31986).

> ?CCN only provides bandwidth below 10 Kbps between all regions free of charge. However, DTS requires a higher bandwidth. Therefore, bandwidth configuration in the link is required.

### Configuring a DTS migration task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, and click **Create Migration Task** to enter the **Create Migration Task** page.
2. On the **Create Migration Task** page, select the types, regions, and specifications of the source and target instances and click **Buy Now**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Source Instance Type</td>
<td>Select the source database type, which cannot be changed after purchase. Here, select <b>MySQL</b>.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>Select the source database region. If the source database is a self-built one, select a region nearest to it.</td></tr>
<tr>
<td>Target Instance Type</td>
<td>Select the target database type, which cannot be changed after purchase. Here, select <b>MySQL</b>.</td></tr>
<tr>
<td>Target Instance Region</td>
<td>Select the target database region.</td></tr>
<tr>
<td>Specification</td>
<td>Select the specification of the migration linkage based on your business conditions.</td></tr>
</tbody></table>
3. On the **Set source and target databases** page, configure the task, source database, and target database settings. After the source and target databases pass the connectivity test, click **Create**.
>?If the connectivity test fails, troubleshoot and fix the problem as prompted and as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552) and try again.
>
<table>
<thead><tr><th>Setting Type</th><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td rowspan=3>Task Configuration</td>
<td>Task Name</td>
<td>Set a meaningful name for easy task identification.</td></tr>
<tr>
<td>Running Mode</td>
<td>Immediate execution: The task will be started immediately after the task verification is passed. Scheduled execution: You need to configure a task execution time and the task will be started automatically then.</td></tr>
<tr>
<td>Tag</td>
<td>Tags are used to manage resources by category in different dimensions. If the existing tags do not meet your requirements, go to the console to create more.</td></tr>
<tr>
<td rowspan=12>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Service Provider</td><td>Select <b>Others</b>.</td></tr>
<tr>
<td>Region</td><td>The source database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select <b>CCN</b>. For more information on access types, see <a href="https://intl.cloud.tencent.com/document/product/571/42652">Overview</a>.</td></tr>
<tr>
<td>Host Address</td><td>IP address or domain name for accessing the source MySQL database.</td></tr>
<tr>
<td>Port</td><td>Port for accessing the source MySQL database.</td></tr>
<tr>
<td>Account</td><td>Account of the source MySQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the source MySQL database.</td></tr>
<tr>
<td>VPC-based CCN Instance</td><td>Only VPC-based CCN instance is supported. You need to confirm the network type associated with CCN.</td></tr>
<tr>
<td>Accessed VPC</td><td>The accessed VPC refers to the VPC in CCN over which the migration/sync linkage is connected. You need to select a CCN-associated VPC other than the VPC where the source database resides. <br>To ensure the network connectivity, you must check whether the following key requirements are met: <ul><li>The selected CCN-associated VPC cannot be in the same region as the host address of the source database. If the source database is MySQL in a self-built IDC, this restriction can be ignored. </li><li>The selected CCN-associated VPC cannot be in the same VPC as the host address of the source database. If the source database is MySQL in a self-built IDC, the selected VPC cannot be the VPC of the Direct Connect gateway associated with the self-built IDC.</li><ul></td></tr>
<tr>
<td>Subnet</td>
<td>Name of the subnet of the selected VPC.<br>If you cannot pull the subnet, there may be a problem with your account. The account of the accessed VPC must be the same as the migration account.<br>For example, to migrate a database under account A to account B, you should use account B to create a task. Therefore, the accessed VPC must be under account B.</td></tr>
<tr>
<td>Region of Accessed VPC</td><td>The region of the source database selected during task purchase must be the same as the region of the accessed VPC; otherwise, DTS will change the former to the latter.</td></tr>
<tr>
<td rowspan=6>Target Database Settings</td>
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select <b>Database</b>.</td></tr>
<tr>
<td>Database Instance</td><td>Select the instance ID of the target TencentDB database.</td></tr>
<tr>
<td>Account</td><td>The account of the target TencentDB database, which needs to have required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target TencentDB database.</td></tr>
</tbody></table>
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td>Select a type based on your scenario.<ul><li>Structural migration: Structured data such as databases and tables in the database will be migrated.</li><li>Full migration: The entire database will be migrated.</li><li>Full + incremental migration: The entire database and subsequent incremental data will be migrated. If there are data writes during migration, and you want to smoothly migrate the data in a non-stop manner, select this option.</li></ul></td></tr>
<tr>
<td>Migration Object</td>
<td><ul><li>Entire instance: Migrate the entire database instance excluding the system databases such as `information_schema`, `mysql`, `performance_schema`, and `sys`.</li>
<li>Specified objects: Migrate specified objects.</li></ul> </td></tr>
<tr>
<td>Specified objects</td>
<td>Select the objects to be migrated in <b>Source Database Object</b> and move them to the <b>Selected Object</b> box.</td></tr>
</tbody></table>

5. On the task verification page, verify the task. After the verification is passed, click **Start Task**.
   If the verification failed, fix the problem as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification task again.
 - Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.
 - Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.

6. Return to the data migration task list, and you can see that the task has entered the **Creating** status. After 1–2 minutes, the data migration task will be started.
 - Select **Structural migration** or **Full migration**: once completed, the task will be stopped automatically.
 - Select **Full + Incremental migration**: After full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
    - Manually complete incremental data sync and business switchover at appropriate time.
    - Observe whether the migration task is in the incremental sync stage and is not in the lag status. If so, stop writing data to the source database for a few minutes.
    - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 seconds.
    
7. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637).

### Business cutover

After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).

