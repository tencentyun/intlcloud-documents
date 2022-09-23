This document describes how to use the data migration feature of DTS to migrate data from MySQL, MariaDB, or Percona to TDSQL-C for MySQL.

The following deployment modes of the source database are supported:

- Self-built MySQL, third-party cloud MySQL, and TencentDB for MySQL.
- Self-built MariaDB and TencentDB for MariaDB.
- Self-built Percona.

This document describes how to migrate data from MySQL to TDSQL-C for MySQL. The requirements and steps of data migration from MariaDB and Percona to TDSQL-C for MySQL are basically the same.

## Notes

- During full data migration, DTS consumes certain source instance resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- Migration is implemented without locks by default, during which no global lock (the FTWRL lock) is added to the source database, and only tables without a primary key are locked.
- When you [create a data consistency check task](https://intl.cloud.tencent.com/document/product/571/42724), DTS will use the account that executes the migration task to write the system database `__tencentdb__` in the source database to record the data comparison information during the migration task.
  - To ensure that subsequent data problems can be located, the `__tencentdb__` system database in the source database will not be deleted after the migration task ends.
  - The `__tencentdb__` system database uses a single-threaded connection wait mechanism and occupies a very small space, about 0.01%–0.1% of the storage space of the source database; for example, if the source database is 50 GB, `__tencentdb__` will be about 5–50 MB. Therefore, it has almost no impact on the performance of the source database and will not preempt resources. 

## Prerequisites
- You have created a TDSQL-C for MySQL cluster as instructed in [Creating Cluster](https://intl.cloud.tencent.com/document/product/1098/40626).
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all the preparations as instructed in [Overview](https://intl.cloud.tencent.com/document/product/571/42652).
- You need to create a migration account in the source self-built MySQL database and grant it the following required permissions:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW
DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%'; 
// If the source database is a TencentDB for MariaDB database, you need to submit a ticket to authorize `RELOAD`; otherwise, you can authorize by referring to the sample code
// If the source database is an Alibaba Cloud database, you don't need to grant the `SHOW DATABASES` permission; otherwise, you need to do so. For more information on authorizing an Alibaba Cloud database, visit https://help.aliyun.com/document_detail/96101.html.
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%'; 
GRANT SELECT ON `mysql`.* TO 'migration account'@'%';
```
- Specified database/table migration: `GRANT SELECT ON database to be migrated.* TO 'migration account';`
- Entire instance migration: `GRANT SELECT ON *.* TO 'migration account';`
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Application restrictions
- Only basic tables and views can be migrated, while objects such as functions, triggers, and stored procedures cannot.
- System tables such as `information_schema`, `sys`, `performance_schema`, `__cdb_recycle_bin__`, `__recycle_bin__`, `__tencentdb__`, and `mysql` cannot be migrated.
- When a view is exported, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as `user2` in the migration target, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to `user2` of the migration target (`[DEFINER = migration target user2]`). If the view definition in the source database is too complex, the task may fail.
- If the source MySQL database is a non-GTID instance, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with the following three database engines can be migrated: InnoDB, MyISAM, and TokuDB. Tables with other engines will be skipped during migration by default.
- Correlated data objects must be migrated together; otherwise, migration will fail. Common correlations include table reference by views, view reference by views, and associative tables based on primary/foreign keys.
- During incremental migration, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, the migration will fail.
- In migration scenarios without locks, after the migration task enters the "source database export" step, DDL operations are not supported.
- If the binlog of the source database has a GTID hole, it may compromise the performance of the migration task and cause the task to fail.
- Scenarios that contain both DML and DDL statements in the same transaction are not supported and will trigger errors during task execution.
- Geometry data types are not supported and will trigger errors during task execution.
- The `ALTER VIEW` statement is not supported and will be skipped during migration.

## Operation limits
- During migration, do not perform the following operations; otherwise, the migration task will fail:
  - Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
  - Do not run distributed transactions in the source database.
  - Do not write binlog data in the `STATEMENT` format into the source database.
  - Do not clear binlogs in the source database.
  - Do not run DDL operations of changing the database/table structure during database/table structure migration or full migration.
  - Do not delete the system table `__tencentdb__` during incremental migration. 
- If you only perform full data migration, do not write new data into the source instance during migration; otherwise, the data in the source and target instances will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend you select full + incremental data migration.

## Supported SQL operations
| Operation Type | Synchronizable SQL Operations               |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, and REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, and RENAME TABLE <br>VIEW: CREATE VIEW and DROP VIEW <br>INDEX: CREATE INDEX and DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, and DROP DATABASE |

## Environment requirements
> ?The system will automatically check the following environment requirements before starting a migration task and report an error if a requirement is not met. If you can identify the failed check item, fix it as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551); otherwise, wait for the system verification to complete and fix the problem according to the error message.

<table>
<tr><th width="20%">Type</th><th width="80%">Environment Requirement</th></tr>
<tr>
<td>Requirements for source database</td>
<td>
<ul>
<li>The source and target databases can be connected.</li>
<li>The server where the source database resides must have enough outbound bandwidth; otherwise, the migration speed will be affected.</li>
<li>Requirements for the instance parameters:
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
<li>If the source instance is a replica database, the `log_slave_updates` variable must be set to `ON`.</li>
<li>We recommend you retain the binlog of the source database for at least three days; otherwise, the task cannot be resumed from the checkpoint and will fail.</li>
</ul></li>
<li>Foreign key dependency:
<ul>
<li>Foreign key dependency can be set to only one of the following two types: `NO ACTION` and `RESTRICT`.</li>
<li>During partial table migration, tables with foreign key dependency must be migrated.</li>
</ul></li>
<li>The migration precision of DTS for data in `FLOAT` type is 38 digits, and for data in `DOUBLE` type is 308 digits. You should check whether this meets your requirements.</li></ul></td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>The target database version must be later than or equal to the source database version.</li>
<li>The size of the target database space must be at least 1.2 times that of the databases/tables to be migrated in the source database. (Full data migration will execute INSERT operations concurrently, causing some tables in the target database to generate data fragments. Therefore, after full migration is completed, the size of the tables in the target database may be larger than that in the source database.)</li>
<li>The target database cannot have migration objects such as tables and views with the same name as those in the source database.</li>
<li>The `max_allowed_packet` parameter of the target database must be set to 4 MB or above.</li></td></tr>
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
<td>Select the source database type, which cannot be changed after purchase. In this scenario, select **MySQL**.</td></tr>
<tr>
<td>Source Instance Region</td>
<td>Select the source database region. If the source database is a self-built one, select a region nearest to it.</td></tr>
<tr>
<td>Target Instance Type</td>
<td>Select the target database type, which cannot be changed after purchase. In this scenario, select **TDSQL-C for MySQL**.</td></tr>
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
<td rowspan=8>Source Database Settings</td>
<td>Source Database Type</td><td>The source database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Service Provider</td><td>For a self-built database (such as a CVM-based one) or TencentDB database, select **Others**. For a third-party cloud database, select the corresponding service provider. In this scenario, select **Others** (with a self-built database as an example).</td></tr>
<tr>
<td>Region</td><td>The source database region selected during purchase, which cannot be changed.</td></tr>
 <tr>
<td>Access Type</td><td>Select a type based on your scenario. In this scenario, select **Public Network**.
<ul><li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a <a href="https://cloud.tencent.com/document/product/213">CVM</a> instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://cloud.tencent.com/document/product/216">Direct Connect</a>. If you select this type, you need to configure VPN-IDC interconnection as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/42651">Direct Connect or VPN Access: Configuring VPN-IDC Interconnection</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>. If you select this type, you need to configure VPN-IDC interconnection as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/42651">Direct Connect or VPN Access: Configuring VPN-IDC Interconnection</a>.</li>
<li>Database: The source database is a TencentDB instance.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>. If you select this type, you need to configure VPC-IDC interconnection as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/42650">CCN Access: Configuring VPC-IDC Interconnection Through CCN</a>. </li></ul>For a third-party cloud database, you can select **Public Network** generally or select **VPN Access**, **Direct Connect**, or **CCN** based on your actual network conditions.</td></tr>
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
<td>Target Database Type</td><td>The target database type selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Region</td><td>The target database region selected during purchase, which cannot be changed.</td></tr>
<tr>
<td>Access Type</td><td>Select **Database**.</td></tr>
<tr>
<td>Database Instance</td><td>Select the target TDSQL-C for MySQL instance ID.</td></tr>
<tr>
<td>Account</td><td>Account of the target TDSQL-C for MySQL database, which must have the required permissions.</td></tr>
<tr>
<td>Password</td><td>Password of the target TDSQL-C for MySQL database.</td></tr>
</tbody></table>
4. On the **Set migration options and select migration objects** page, configure the migration type and objects and click **Save**.
>?
>
>If you want to rename a table (for example, rename table A table B) during migration, you must select the entire database (or entire instance) where table A resides rather than only table A as the **migration object**; otherwise, the system will report an error.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/2d9b4d6316c079e7cee34c9d9102641b.png" style="zoom:67%;" />
<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Migration Type</td>
<td><ul><li>Structural migration: Structured data such as databases and tables in the database will be migrated. </li><li>Full migration: The entire database will be migrated. The migrated data will include only the existing data from the source database when the task is started, not incremental data written to the source database after the task is started. </li><li>Full + Incremental migration: The migrated data will include the existing data from the source database when the task is started as well as the incremental data written to the source database after the task is started. If there are data writes to the source database during migration, and you want to smoothly migrate the data in a non-stop manner, select this type.</li></ul></td></tr>
<tr>
<td>Migration Object</td>
<td>Select **Entire instance** if you need to migrate the entire instance, but system databases such as `information_schema`, `mysql`, `performance_schema`, and `sys` won't be migrated <br>Select specified object if you need to migrate specified tables.</td></tr>
<tr>
<td>Migrate Account</td>
<td>Select this feature if you want to migrate the account information of the source database.</td></tr><tr>
<td>Selected Object</td>
<td><ul><li>Database/Table mapping (renaming) is supported. Hover over a database or table name, click the displayed **Edit** icon, and enter a new name in the pop-up window.</li><li>When advanced objects are selected for migration, we recommend you not rename databases/tables; otherwise, migration of the advanced objects may fail.</li><li>Online DDL temp tables can be migrated (through tools such as gh-ost or pt-online-schema-change). Click **Edit** of a table and select a temp table name in the pop-up window. For more information, see <a href="https://cloud.tencent.com/document/product/571/75889">Migrating Online DDL Temp Table</a>.</li></ul></td></tr>
</tbody></table>
5. On the task verification page, verify the task. After the verification is passed, click **Start Task**.
 - If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
    - Failed: It indicates that a check item fails and the task is blocked. You need to fix the problem and run the verification task again.
    - Alarm: It indicates that a check item doesn't completely meet the requirements, and the task can be continued, but the business will be affected. You need to assess whether to ignore the alarm or fix the problem and continue the task based on the alarm message.
 - If you select **Migrate Account**, the account information of the source database will be verified. For more information, see [Migrating Account](https://cloud.tencent.com/document/product/571/65702).
![](https://qcloudimg.tencent-cloud.cn/raw/c18a641009300d8e765a4664ef7f3063.png)
6. Return to the data migration task list, and you can see that the task has entered the **Creating** status. After 1–2 minutes, the data migration task will be started.
 -  Select **Structural migration** or **Full migration**: once completed, the task will be stopped automatically.
 -  Select **Full + Incremental migration**: After full migration is completed, the migration task will automatically enter the incremental data sync stage, which will not stop automatically. You need to click **Complete** to manually stop the incremental data sync.
    - Manually complete incremental data sync and business switchover at appropriate time.
    - Check whether the migration task is in the incremental sync stage without any lag. If so, stop writing data to the source database for a few minutes.
    - Manually complete incremental sync when the data gap between the target and the source databases is 0 MB and the time lag between them is 0 seconds.
7. (Optional) If you want to view, delete, or perform other operations on a task, click the task and select the target operation in the **Operation** column. For more information, see [Viewing Task](https://intl.cloud.tencent.com/document/product/571/42637).
8. After the migration task status becomes **Task successful**, you can formally cut over the business. For more information, see [Cutover Description](https://intl.cloud.tencent.com/document/product/571/42612).


