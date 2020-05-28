## MySQL 5.7
### 20190830
#### New features
- Supports skipping corrupted data and continuing to parse when a binlog is damaged. In scenarios where the master instance and binlog are both damaged, this feature can restore available data from the slave database for use as much as possible.
- Supports syncing data from the non-GTID mode to GTID mode.
- Allows you to query the "user thread memory usage information" by executing the `show full processlist` statement.
- Supports [quick column adding](https://intl.cloud.tencent.com/document/product/236/35990) for tables. This feature does not copy the data or use disk space/IO and can implement changes during peak hours.
- Supports persistence of auto-increment values.

#### Fixes
- Fixed the error where replication would be interrupted if the column name in a `GRANT` statement contains reserved words.
- Fixed the error where SQL statement execution efficiency dropped when reverse scanning was performed on a partition table.
- Fixed the error where the query result was exceptional due to inconsistent virtual index data in a primary key table.
- Fixed the error where data was missing due to InnoDB primary key range query.
- Fixed the error where the system crashed when a DDL statement was executed for a table with spatial indexes.
- Fixed the error where master/slave disconnection occurred when the binlog size was too large and the file length in the heartbeat information exceeded the limit.
- Fixed the error where other events could not be executed as scheduled when an event was deleted.
- Fixed the error where the aggregated query result was incorrect.

### 20190615
#### New features
- Supports transparent data encryption (TDE).

### 20190430
#### Fixes
- Fixed the error where null pointer reference occurred when the long text feature was used in subqueries.
- Fixed the error where the master/slave disconnection occurred due to hash scan.
- Fixed the error where the slave node's I/O thread was interrupted due to binlog switch of the master database.
- Fixed the crash caused by the use of `NAME_CONST`.
- Fixed the illegal mix of collation error caused by the character set.


### 20190203
#### New features
- Supports async deletion of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by big table deletion. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Supports the CATS lock scheduling.
- Allows you to create and delete temp tables and CTS syntax in transactions after GTID is enabled. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Supports implicit primary keys. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Allows users without the super privileges to kill sessions of other users by setting the `cdb_kill_user_extra` parameter (default value: `root@%`).
- Supports enterprise-grade encryption functions. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

#### Fixes
- Fixed the error where replication was interrupted when the binlog cache file space was insufficient.
- Fixed the error where an infinite loop occurred when `EIO` was returned for `fsync` and retries were made repeatedly.
- Fixed the error where the replication was interrupted and could not be recovered due to GTID holes.
   

### 20180918
#### New features
- Supports automatic killing of idle tasks to reduce resource conflicts. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Automatically changes the MEMORY engine to InnoDB engine: if the global variable `cdb_convert_memory_to_innodb` is set to `ON`, the table engine will be changed to InnoDB from MEMORY when a table is created or modified.
- Supports index hiding.
- Supports memory management with jemalloc, which can replace the jlibc memory management module to reduce the memory usage and improve the memory allocation efficiency.
   
#### Performance optimizations
- Optimizes binlog switch to reduce the `rotate` holdlock duration and improve the system performance.
- Increases the crash recovery speed.
    
#### Fixes
- Fixed the error where an event became invalid due to master/slave switch.
- Fixed the crash caused by `REPLAY LOG RECORD`.
- Fixed the error where the query result was incorrect due to loose index scans.


### 20180530
#### New features
- Supports SQL auditing.
- Supports table-level concurrent replication. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
   
#### Performance optimizations
- Optimizes slave instance locks to improve the sync performance of slave instances.   
- Optimizes pushdown of the `select ... limit` statement.
   
#### Fixes
- Fixed the error where switch failed due to inconsistent checkpoints between `relay_log_pos` and `master_log_pos`.
- Fixed the crash caused by `Crash on UPDATE ON DUPLICATE KEY`.
- Fixed the “Invalid escape character in string.” error when a JSON column was imported.
   
### 20171130
#### New features
- Supports the `information_schema.metadata_locks` view to query the MDL granting and waiting status of the current instance.
- Supports the `ALTER TABLE NO_WAIT | TIMEOUT` syntax to grant DDL operations wait timeout. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Supports the thread pool. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

#### Fixes
- Fixed the error of `innodb_buffer_pool_pages_data` parameter overflow by calculating it based on `bytes_data`.
- Fixed the error where the speed limit plugin became unavailable in async mode.

   
## MySQL 5.6
### 20190930
#### New features
- Allows you to query the "user thread memory usage information" by executing the `show full processlist` statement. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.  

#### Fixes
- Fixed GTID holes caused by the replication filter of the slave database.
- Fixed the error where master/slave disconnection occurred when the binlog size was too large and the file length in the heartbeat information exceeded the limit.
- Fixed the illegal mix of collation error caused by the character set.
- Fixed the error where the master/slave disconnection occurred due to hash scan.
- Fixed the crash caused by the use of `NAME_CONST`.
- Fixed the error where the slave node's I/O thread was interrupted due to binlog switch of the master database.
- Fixed the error of incompatible backup files due to `innodb_log_checusum`.

### 20190530
#### Fixes
- Fixed the error where dirty data might be read in RC mode.
- Fixed the error where slave replay might fail due to the deletion of temp table.
- Fixed the error of deadlock under high concurrency.
   

### 20190203
#### New features
- Supports async deletion of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by big table deletion. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Allows users without the super privileges to kill sessions of other users by setting the `cdb_kill_user_extra` parameter (default value: `root@%`).
- Allows you to create and delete temp tables and CTS syntax in transactions after GTID is enabled. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
   
#### Performance optimizations   
- Optimizes replication replay of partition tables to improve the partition table replay efficiency.
   
#### Fixes
- Fixed the error of inconsistent data between master and slave due to insufficient temporary space.
- Fixed the error of hot record update suspension.
- Fixed the error where the `Seconds_Behind_Master` value was exceptional during concurrent replication.

### 20180915
#### New features
- Automatically changes the MEMORY engine to InnoDB engine: if the global variable `cdb_convert_memory_to_innodb` is set to `ON`, the table engine will be changed to InnoDB from MEMORY when a table is created or modified.
- Supports automatic killing of idle tasks to reduce resource conflicts. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
   
#### Fixes
- Fixed the crash caused by `REPLAY LOG RECORD`.
- Fixed the error of inconsistent time data between master and slave due to the decimal place accuracy issue.


### 20180130
#### New features
- Supports the thread pool. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Supports dynamic modification and replication of filters for slave nodes.

#### Performance optimizations
- Reduces the performance fluctuation caused by `drop table`.
   
#### Fixes
- Fixed the error where the database crashed due to authentication password strings.
   
### 20180122
#### New features
- Supports SQL auditing.

#### Fixes
- Fixed the error of integer overflow.
- Fixed the error caused by queries using full-text index.
- Fixed the error where the slave crashed during replication.
	
### 20170830
#### Fixes
- Fixed the error where the binlog speed limit became invalid in async mode.
- Fixed the error where the `buffer_pool` status was exceptional.
- Fixed the error where `SEQUENCE` and implicit primary key conflicted.
   
### 20170228
#### Fixes
- Fixed the character encoding bug in `drop table`.
- Fixed the error where special symbols such as decimal points in a database or table could not be properly filtered during execution of the `replicate-wild-do-table` statement.
- Fixed the error where SQL threads exited too early after the `rotate` event occurred in the slave database.
  
### 20161130
#### Performance optimizations
- Splits the `lock_log` lock to reduce the time used by the lock log and improve the concurrency performance.
- Separates the ACK thread of the master database to improve response time.
- Prohibits the user thread from being killed when it waits for ACK in order to prevent phantom reads.
- Fixes the unnecessary `lock_sync` lock occurring in case of `sync_binlog != 1`.

