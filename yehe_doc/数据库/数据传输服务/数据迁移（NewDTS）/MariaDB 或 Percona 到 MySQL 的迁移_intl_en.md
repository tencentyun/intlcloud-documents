This document describes how to use the data migration feature of DTS to migrate data from MariaDB or Percona to TencentDB for MySQL.

## Notes 
- During full data migration, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you migrate the data during off-peak hours.
- Full migration is implemented with tables locked (backup lock), which causes write operations to be blocked for a few seconds.

## Prerequisites
- You have created a [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/37785) instance.
- The source and target databases must meet the requirements for the migration feature and version as instructed in [Databases Supported by Data Migration](https://intl.cloud.tencent.com/document/product/571/42647).
- You have completed all [preparations](https://intl.cloud.tencent.com/document/product/571/42652).
- The source database must have the following permissions:
  - Migration of the entire instance:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO 'migration account'@'%';  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%';  // If the source database is a TencentDB database, you need to grant the `__tencentdb__` permission
GRANT SELECT ON *.* TO 'migration account';
```
  - Migration of specified objects:
```
CREATE USER 'migration account'@'%' IDENTIFIED BY 'migration password';  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW, RELOAD, PROCESS ON *.* TO 'migration account'@'%';  // If the source database is a TencentDB for MariaDB/Percona database, you need to submit a ticket to authorize `RELOAD`; otherwise, you can authorize by referring to the sample code
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'migration account'@'%';  // If the source database is a TencentDB database, you need to grant the `__tencentdb__` permission
GRANT SELECT ON `mysql`.* TO 'migration account'@'%';
GRANT SELECT ON database to be migrated.* TO 'migration account';
```
 - If the source database is MariaDB 10.5 or 10.6, you also need the `SLAVE MONITOR` permission to run `show slave status`.
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Compatibility Description for Heterogeneous Migration
During migration from MariaDB to MySQL, due to their slight differences in features, the following compatibility issues may occur:
1. Due to MariaDB's functional characteristics, some SQL statements are different from the returned result of `SHOW CREATE TABLE`, which may cause differences of the synced DDL statements in the target database.
   - Even if no default value is specified for the blob type in MariaDB, `SHOW CREATE TABLE` will still display the default value `DEFAULT NULL` after the table is created.   
   - If the DDL statement of `datetime` type in the source database is `datetime NOT NULL ON UPDATE CURRENT_TIMESTAMP`, `SHOW CREATE TABLE` will display `datetime NOT NULL DEFAULT '0000-00-00 00:00:00' ON UPDATE current_timestamp()` after the table is created, and the DDL parsed by the target MySQL will be `datetime NOT NULL ON UPDATE CURRENT_TIMESTAMP`.

2. Some statements only supported by MariaDB (such as `CREATE OR REPLACE TABLE/PERIOD FOR/WITHOUT OVERLAPS`) may cause the migration task to report errors during full migration and will be ignored during incremental migration. 
   - If the `PERIOD FOR/WITHOUT OVERLAPS` statement is executed before the migration task is started or during full migration (in the source database export and data import step), the migration task will fail; if it is executed during incremental sync, the target database will ignore it, and data cannot be synced to the target database.
   - As DDL operations that change the database or table structure cannot be performed during full migration, if the `CREATE OR REPLACE TABLE` statement is executed during full migration, the migration task will fail; if it is executed during incremental sync, the target database will ignore it, and data cannot be synced to the target database. 

3. MariaDB allows default values for blob/text data, but MySQL does not. If there are SQL statements of these types, the migration task will report errors.  

## Application Restrictions
- Only basic tables and views can be migrated, while objects such as functions, triggers, and stored procedures cannot.
- System databases/tables and user information including `information_schema`, `sys`, `sysdb`, `performance_schema`, `__cdb_recycle_bin__`, `__recycle_bin__`, `__tencentdb__`, and `mysql` cannot be migrated. After the migration is completed, if you want a view, stored procedure, or function in the target database to be called, you must grant the caller the read/write permissions. 
- When a view is exported, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as `user2` in the migration target, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to `user2` of the migration target (`[DEFINER = migration target user2]`).
- If the source MySQL database is a non-GTID database, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with the following three database engines can be migrated: InnoDB, MySIAM, and TokuDB. Tables with other engines will be skipped during migration by default.
- Correlated data objects must be migrated together; otherwise, migration will fail. Common correlations include table reference by views, view reference by views, view/table reference by stored procedures/functions/triggers, and tables correlated through primary/foreign keys.
- During incremental migration, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, the migration will fail.
- The DTS migration task requires that the values of the `lower_case_tame_name` parameter (table name case sensitivity) of the source and target databases be the same. If the source database is TencentDB for MariaDB or Percona, as they allow modifying this parameter only during instance creation, you need to determine the case sensitivity rule when creating the source database and modify this parameter of the target database if the values are different during verification.
- If the source database is TencentDB for MariaDB 10.4, the **Access Type** does not support the **Database** option, and you need to select **Public Network** or other types.

## Operation Restrictions
- During migration, do not perform the following operations; otherwise, the migration task will fail:
  - Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers.
  - Do not run distributed transactions in the source database.
  - Do not write binlog data in the `STATEMENT` format into the source database.
  - Do not clear binlogs in the source database.
  - Do not run DDL operations of changing the database/table structure during database/table structure migration or full migration.
  - Do not delete the system table `__tencentdb__` during incremental migration. 
  - If MariaDB's unique statements such as `CREATE OR REPLACE TABLE/PERIOD FOR/WITHOUT OVERLAPS` are included, the migration task may report errors during full migration and will ignore them during incremental migration.
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
<li>On MariaDB 10.2 or above and Percona 5.6 or above, if the `gtid_mode` variable is not `ON`, an alarm will be triggered. We recommend you enable `gtid_mode`.</li>
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
Migration from MariaDB and Percona to TencentDB for MySQL follows the same steps of migration from MySQL to TencentDB MySQL. For detailed configurations, see [Migration from MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/42645).
