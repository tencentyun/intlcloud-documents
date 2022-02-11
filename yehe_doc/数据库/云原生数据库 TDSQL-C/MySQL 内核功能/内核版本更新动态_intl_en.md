
This document describes the TDSQL-C kernel version updates. For information on how to upgrade the kernel, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/1098/44617).

## TDSQL-C for MySQL 8.0
### 3.0.1
#### Feature updates
- Supported three methods of querying `cynos_version`: `select CYNOS_VERSION()`, `select @@cynos_version`, and `show variables like 'cynos_version'`.
- Added a space limit parameter. If the total space usage exceeds the limit, an error will be reported to prompt you to release the space or upgrade the specification.
- Added the `innodb_ncdb_log_priority` read-only parameter, which indicates the priority of the primary instance's backend log thread.
- Added the `innodb_ncdb_apply_priority` read-only parameter, which indicates the priority of the read-only instance's log replay thread.
- Added the `innodb_ncdb_fast_shutdown` dynamic parameter, which controls whether to quickly shut down processes. After it is enabled, when a process exits, no destruction operations on the global structure will be performed, which reduces the shutdown time. It is disabled by default.
- Added the `innodb_max_temp_data_file_size` read-only parameter. Its default value is 128 MB. If its value is greater than 0, it indicates the maximum size of the temp tablespace in the local storage.

## TDSQL-C for MySQL 5.7
### 2.0.14
#### Feature updates
- Supported INSTANT MODIFY COLUMN. For more information, see [Instant DDL Overview](https://intl.cloud.tencent.com/document/product/1098/44588).

#### Fixes
- Fixed the issue where the used space was not reclaimed when a temp table in a read-only instance was dropped.
- Fixed the issue where the process exited when a read-only instance read the old page version due to changes in storage routes.
- Fixed the issue of possible crash when `information_schema.metadata_locks` was queried.
- Fixed the concurrency error of forward scan and B-tree SMO in read-only instance.
- Fixed the issue where when multiple tables had complex foreign key dependencies and the foreign key attribute was `ON DELETE CASCADE`, the corresponding record in a child table might be deleted twice when a record was delete in its parent table with DELETE.
- Fixed the issue where the process exited due to operations such as CREATE USER in a read-only instance.
- Fixed the issue where SHOW VOLUME STATUS in a read-only instance might trigger an assertion failure.
- Fixed the issue where a read-only instance had exceptional query results and crashed when DDL operations were performed in partitioned tables frequently.
- Fixed the issue where the process crashed during historical version construction when an read-only instance scanned a purged undo log.

### 2.0.13
#### Feature updates
- Supported INSTANT ADD COLUMN. For more information, see [Instant DDL Overview](https://intl.cloud.tencent.com/document/product/1098/44588).
- Optimized the audit performance under high load and added the `lock_usleep_time` dynamic parameter.

#### Fixes
- Fixed the issue where `dict_operation_lock` might cause deadlock during foreign key check.
- Fixed the issue where the process might exit when the ACL change log was replayed during read-only instance startup.
- Fixed the issue where data in primary and secondary instances was inconsistent after INSTANT ADD COLUMN and TRUNCATE TABLE.
- Fixed the log replay error occurring when data was inserted again after INSTANT ADD COLUMN and TRUNCATE TABLE.
- Fixed the issue where the process exited when a primary key containing a column added by INSTANT ADD COLUMN was created.
- Fixed the issue where the process exited during table structure query in a read-only instance when INSTANT COLUMN was used to create or rebuild a partition.

### 2.0.12
#### Feature updates
- Supported database audit. For more information on how to use it, see [Enabling TDSQL-C Audit](https://intl.cloud.tencent.com/document/product/1102/41312).
- Supported purging page read-ahead to accelerate space reclaim.
- Supported real-time update of the size information of tables and indexes in the system view.
- Added a thread to accelerate recycle LSN and storage GC.

#### Fixes
- Fixed official bugs in full-text index, including BUG#24938374, BUG#21625016, BUG#27082268, BUG#27155294, BUG#27326796, BUG#27304661, BUG#25289359, BUG#29717909, and BUG#30787535.
- Fixed official bugs where concurrent update might cause system crashes, including BUG#30950714, BUG#31205266, and BUG#25669686.
- Fixed the official bug BUG#28104394 where uncommitted INSERT operations would affect the range scan created by an index and made it return an incorrect number of rows.
- Fixed the official bug BUG#30488700 where an incorrect query execution plan of a derived table could result in a poor performance.
- Fixed the issue where the process exited when a read-only instance replayed statistics logs after the primary (read-write) instance executed a DDL statement.
- Fixed the issue where RENAME TABLE was performed on a database that did not exist.
- Fixed the issue where a read-only instance might exit when OPTIMIZE TABLE was used for the primary instance.
- Fixed the issue where transactions were inconsistent after a table with a full-text index was updated in a read-only instance.
- Fixed the deadlock occurring during SET OFFLINE MODE and SHOW VARIABLES operations.

### 2.0.11
#### Feature updates
- Optimized the binlog file index to accelerate binlog file scan.
- Optimized the shutdown process to make it faster.
- Optimized the instance memory to reduce the memory usage by structures such as buffer, ZIP, and hash.
- Optimized the DDL lock recovery process during read-only instance startup to accelerate replay.
- Optimized system table loading in read-only instance to accelerate startup.
- Optimized worker thread assignment during PURGE COORDINATOR to accelerate purge.

#### Fixes
- Fixed the issue where the process crashed during OPEN TABLE due to incorrect index structure mapping.
- Fixed the issue where read-only instance replication was exceptional during XA transaction rollback.
- Fixed the issue where startup crashed when binlog replication was started in a read-only instance.
- Fixed the memory leak caused by FLUSH LOGS.
- Fixed the shutdown failure of `mysqladmin shutdown`.
- Fixed the issue where a read-only instance failed to replay logs when DROP COLUMN was performed on the primary instance.
- Fixed the issue where data could still be input after space restriction was triggered when a BLOB was inserted.
- Fixed the issue of read-only instance replication availability that might be caused by DDL statements in big tables or slow log storage in the primary instance.
- Fixed the issue where storage wasted small tables after `innodb_max_temp_data_file_size` was set for a temp table.

