This document describes how to use the data migration feature of DTS to migrate data from MySQL to TencentDB for MariaDB (Percona).

Data migration from MariaDB (Percona) to TencentDB for MariaDB (Percona) and from MariaDB to TencentDB for MariaDB has the same requirements as migration from MySQL to TencentDB for MariaDB (Percona). You can refer to relevant content in this document.

## Notes

- During full data migration, DTS consumes certain source database resources, which may increase the load and pressure of the source database. If your database configuration is low, we recommend you migrate the data during off-peak hours.
- Full migration is implemented with tables locked, which causes write operations to be blocked for a few seconds.

## Prerequisites

- You have created a [TencentDB for MariaDB](https://intl.cloud.tencent.com/document/product/237/7051) instance.
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
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, and TRUNCATE TABLE<br>VIEW: CREATE VIEW and DROP VIEW<br>INDEX: CREATE INDEX and DROP INDEX<br> |

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
The data migration steps in different scenarios are basically the same. For detailed directions, see [Migration from MySQL to TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/571/42645).

