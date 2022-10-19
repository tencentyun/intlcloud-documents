This document describes how to use the data sync feature of DTS to sync data from MySQL/MariaDB/Percona to TencentDB for MariaDB.

The following deployment modes of the source database are supported:

- Self-built MySQL and TencentDB for MySQL.
- Self-built MariaDB and TencentDB for MariaDB.
- Self-built Percona.

This document describes how to sync data from MariaDB to TencentDB for MariaDB. The requirements and steps of data sync from MySQL and Percona to TencentDB for MariaDB are basically the same.

## Notes
- During full data sync, DTS consumes certain source instance resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you sync the data during off-peak hours.
- To avoid duplicate data, make sure that the tables to be synced have a primary key or non-null unique key.
- Sync is implemented without locks by default, during which no global lock (the FTWRL lock) is added to the source database, and only tables without a primary key are locked.
- During data sync, DTS will use the account that executes the sync task to write the system database `__tencentdb__` in the source database to record the data comparison information during the sync task.
  - To ensure that subsequent data problems can be located, the `__tencentdb__` system database in the source database will not be deleted after the sync task ends.
  - The `__tencentdb__` system database uses a single-threaded connection wait mechanism and occupies a very small space, about 0.01%–0.1% of the storage space of the source database; for example, if the source database is 50 GB, `__tencentdb__` will be about 5–50 MB. Therefore, it has almost no impact on the performance of the source database and will not preempt resources. 

## [Prerequisites](id:qttj)
- The source and target databases must meet the requirements for the sync feature and version as instructed in [Databases Supported by Data Sync](https://intl.cloud.tencent.com/document/product/571/42579).
- Permissions required of the source database:
```sql
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW VIEW,PROCESS,SELECT ON *.* TO 'account'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'account'@'%'; 
FLUSH PRIVILEGES;
```
- Permissions required of the target database: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, and UPDATE.

## Use limits
- Only basic tables, views, procedures, and functions can be synced. 
- When views, procedures, and functions are synced, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as the sync account `user2`, and if not, DTS will change the `SQL SECURITY` attribute of `user1` in the target database from `DEFINER` to `INVOKER` (`[INVOKER = user1]`) after the sync, and set the `DEFINER` in the target database to the sync account `user2` (`[DEFINER = sync account user2]`). If the view definition in the source database is too complex, the task may fail.
- If the source MySQL database is a non-GTID instance, DTS doesn't support HA switch for it. If it is switched, DTS incremental sync may be interrupted.
- Only data with the following three database engines can be synced: InnoDB, MyISAM, and TokuDB. Tables with other engines will be skipped during sync by default.
- Correlated data objects must be synced together; otherwise, sync will fail. Common correlations include table referenced by views, view referenced by views, and tables correlated through primary/foreign keys.
- During incremental sync, if the source database has distributed transactions or generates binlog statements in the `STATEMENT` format, sync will fail.
- If the source database is Alibaba Cloud MySQL, then the tables to be synced on v5.6 must have a primary key, while tables on v5.7 and later are unrestricted. If the source database is AWS MySQL, then the tables to be synced must have a primary key.
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

## Synchronizable SQL operations

| Operation Type | SQL Statements                                              |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, and DELETE                                       |
| DDL      | CREATE DATABASE, DROP DATABASE, ALTER DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAME TABLE, CREATE VIEW, DROP VIEW, CREATE INDEX, and DROP INDEX<br><dx-alert infotype="explain" title="Note">DDL statements involving partitions cannot be synced.</dx-alert> |

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
<li>During partial table sync, tables with foreign key dependency must be migrated.</li></ul></li></td></tr>
<tr> 
<td>Requirements for the target database</td>
<td>
<li>The target database version must be later than or equal to the source database version.</li>
    <li>The target database must have sufficient storage space. If you select <b>Full data initialization</b> as the initialization type, the target database space must be at least 1.2 times the space of databases/tables to be synced in the source database.</li>
<li>The target database cannot have sync objects such as tables and views with the same name as those in the source database.</li>
<li>The `max_allowed_packet` parameter of the target database must be set to 4 MB or above.</li></td></tr>
<tr> 
<td>Other requirements</td>
<td>The environment variable `innodb_stats_on_metadata` must be set to `OFF`.</td></tr>
</table>


## Directions
You can refer to the directions described in [Data Sync from MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/47344).
