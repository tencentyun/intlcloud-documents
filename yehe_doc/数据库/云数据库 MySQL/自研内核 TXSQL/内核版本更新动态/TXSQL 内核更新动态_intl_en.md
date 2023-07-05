This document describes the version updates of the TXSQL kernel.
>?
>- For more information on how to upgrade the minor kernel version of a TencentDB for MySQL instance, see [Upgrading Kernel Minor Version](https://www.tencentcloud.com/document/product/236/36816).
>- When you upgrade the minor version, some minor versions may be under maintenance and cannot be selected. The minor versions available in the console shall prevail.

<dx-tabs>
::: MySQL 8.0 Kernel Version Release Notes
<table>
<thead><tr><th>Minor Version</th><th>Description</th></tr></thead>
<tbody>
<tr>	
<td>20220831</td>
<td><ul><li>New features</li><ul>
<li>Supported setting the MySQL version dynamically.</li>
<li>Supported transparent column encryption. When creating a table, you can specify the encryption attribute for the `varchar` field, and the storage system will encrypt the column. This capability is expected to be commercialized in 2023.</li>
<li>Fixed the exception of the third-party data subscription tool caused by subscription to the comparison SQL for internal data consistency during tool usage. <dx-alert infotype="explain" title="Note">After the database instance is migrated, upgraded, or recovered after failure, the system will compare the data consistency to ensure the consistency of data. When comparison SQL is in `statement` mode, exceptions are easy to occur in response of some third-party subscription tools to the SQL in `statement` mode. When the instance is upgraded to its kernel, the third-party data subscription tool can't subscribe the comparison SQL for internal data consistency.</dx-alert></li>
<li>Supported adding NO_WAIT | WAIT [n] for DDL operations. This enables such operations to be rolled back immediately if they cannot obtain the MDL lock and must wait or if they have waited the specified time for the MDL lock.</li>
<li>Supported the fast query cache feature, which is suitable for scenarios with more reads than writes. If there are more writes than reads, the data is updated very frequently, or the result set of the query is very large, we recommend that you not enable this feature.</li>
<li>Supported enhanced MTS deadlock detection.</li>
<li>Supported <a href="https://www.tencentcloud.com/document/product/236/52512">parallel query</a>. After this feature is enabled, large queries can be automatically identified. The parallel query capability leverages multiple compute cores to greatly shorten the response time of large queries.</li>
</ul>
<li>Performance optimizations</li><ul>
<li>Optimized the overheads of the transaction system to take snapshots. The Copy Free Snapshot method is adopted, the transaction delay is deleted from the global active transaction hash, and the snapshot taking method is optimized to determine the logical timestamp of the snapshot event. As tested by sysbench, the extreme performance is increased by 11% in the read-write scenario.</li>
<li>Optimized permission check for prepared statements. A variable is used globally to indicate the permission version number, a prepared statement records the version number after being prepared, and the system checks whether the version number has changed during execution. If there is no permission change, the system will skip the permission check; otherwise, it will check the permission and record the version number again.</li>
<li>Optimized the accuracy of time acquisition in the thread pool.</li>
<li>Optimized record offset acquisition. A record offset is cached for each index. When the conditions are met, the cached offset will be directly used, saving the computing overheads of invoking the `rec_get_offsets()` function.</li>
<li>Optimized parallel DDL. <br>1. When the index field is small, the sampled memory size is reduced to lower the sampling frequency. <br>2. The K-way merge algorithm is used for sorting, which effectively reduces the number of rounds of merging and sorting to lower the number of IOs. <br>3. When records are read, the fixed-length offset is cached in order to avoid generating offsets for each record each time.</li>
<li>Optimized the undo log information recording logic to improve the INSERT performance. </li>
<li>Improved the performance after semi-sync was enabled.</li>
<li>Optimized the audit performance to reduce the system overheads.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where the displayed value of `Thread_memory` was abnormal sometimes.</li>
<li>Fixed the issue where the timestamp was inaccurate during batch statement audit.</li>
<li>Fixed issues related to column modification at the second level.</li>
<li>Fixed the issue where the `CREATE TABLE t1 AS SELECT ST_POINTFROMGEOHASH("0123", 4326);` statement caused source-replica disconnection.</li>
<li>Fixed the issue where the replica failed to retry during concurrent requests at the table level.</li>
<li>Fixed the `Malformed packet` error reported when `show slave hosts` was executed.</li>
<li>Fixed recycle bin issues.</li>
<li>Fixed the issue where the jemalloc mechanism easily triggered OOM on ARM device models.</li>
<li>Fixed the issue where `truncate pfs account table` caused the failure to collect statistics.</li>
<li>Fixed the exception that occurred while restoring the child table first and then restoring the parent table when the recycle bin had a foreign key constraint.</li>
<li>Fixed sql_mode log issues.</li>
<li>Fixed the occasional issue where a procedure became abnormal when `CREATE DEFINER` was executed.</li>
<li>Fixed Copy Free Snapshot issues.</li>
<li>Fixed the performance fluctuation of the thread pool.</li>
<li>Fixed the issue where the result of `hash join+union` might be empty.</li>
<li>Fixed memory issues.</li>
</ul>
</td>
</tr>	

<tr>	
<td>20220401</td>
<td><ul><li>Bug fixes</li><ul>
<li>Fixed the issue where the stage variable error in Parallel DDL caused the stage null pointer to crash when creating FTS indexes.</li>
<li>Fixed the possible crash when adding full-text indexes.</li>
</ul></td>
</tr>	

<tr>	
<td>20220331</td>
<td><ul><li>Bug fixes</li><ul>
<li>Fixed the crash caused by dereferencing wild pointers in the thread pool.</li>
</ul></td>
</tr>

<tr>	
<td>20220330</td>
<td>
<ul><li>New features</li><ul>
<li>Enabled writeset parallel replication by default.</li>
<li>Supported extended resource groups to control the I/O, memory utilization, and SQL timeout policy by user.</li>
<li>Supported flashback query to query data at any time point within the UNDO time range.</li>
<li>Supported `RETURNING` in a `DELETE`, `INSERT`, or `REPLACE` statement to retrieve the data rows modified by the statement.</li>
<li>Supported the GTID replication feature extension in row mode.</li>
<li>Supported transaction lock optimization.</li>
<li>Enhanced the recycle bin to support TRUNCATE TABLE and automatic cleanup of tables in the recycle bin.</li>
<li>Supported parallel DDL to speed up DDL operations for which to create indexes through three-phase parallel operations.</li>
<li>Supported quick index column modification.</li>
<li>Supported automatic statistics collection and cross-server statistics collection.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the GTID lock conflicts when transactions were committed if `binlog_order_commits` was disabled.</li>
<li>Accelerated MySQL startup by changing the InnoDB startup phase from single-threaded creation of Rsegs to multi-threaded creation.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where the transaction did not end when the connection was closed after deadlock or lock wait.</li>
<li>Fixed the issue where the `innodb_row_lock_current_waits` value was abnormal.</li>
<li>Fixed the SQL type error in the audit plugin without USE DATABASE.</li>
<li>Fixed the issue where tables smaller than `innodb_async_table_size` were also renamed during async drop of big tables.</li>
<li>Fixed the issue with incorrect escape characters in the audit plugin.</li>
<li>Fixed the issue of rollback after quick column modification.</li>
<li>Fixed the issue where the transaction system (trx_sys) may crash if it contains XA transactions when it is closed.</li>
<li>Fixed the crash when merging derived tables.</li>
<li>Fixed the issue where `binlog_format` was modified after writeset was enabled.</li>
<li>Fixed the error (error code: 1032) caused by hash scans with A->B->A->C update on the same row.</li>
<li>Fixed the issue where the sort index might be invalid in prepared statement mode.</li>
<li>Fixed the issue where the operator that consumed the materialized result might be merged into the returned value path of the materialized operator and result in incorrect comprehension and display of the execution plan.</li>
<li>Fixed exceptions in extreme cases for async drop of big tables.</li>
<li>Fixed the abnormal error message when setting a SQL filter.</li>
<li>Fixed the syntax error reported during stored procedure parsing.</li>
<li>Fixed the issue where historical histograms couldn't be applied.</li>
<li>Fixed the role column display compatibility issue caused by `SHOW SLAVE HOSTS(show replicas)`.</li>
<li>Fixed the crash of `Item_in_subselect::single_value_transformer` when the number of columns was incorrect.</li>
<li>Fixed the crash caused by memory leaks during cascading update if a subtable contained virtual columns and foreign key columns.</li>
</ul>
</td>
</tr>

<tr>	
<td>20211202</td>
<td>
<ul><li>New features</li><ul>
<li>Supported quick column modification.</li>
<li>Supported histogram versioning.</li>
<li>Supported SQL:2003 TABLESAMPLE (single table) sampling control syntax for obtaining random samples of physical tables.</li>
<li>Added non-reserved keywords: TABLESAMPLE BERNOULLI.</li>
<li>Added the `HISTOGRAM()` function to build a histogram for a given input field.</li>
<li>Supported compressed histograms.</li>
<li>Supported SQL throttling.</li>
<li>Supported MySQL cluster role configuration (default role: CDB_ROLE_UNKNOWN).</li>
<li>Added a new `Role` column to the `show replicas` command's display results to display roles.</li>
<li>Supported proxy.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the hotspot update problem caused by `insert on duplicate key update`.</li>
<li>Accelerated the application of hash scan by aggregating multiple identical binlog events.</li>
<li>Greatly reduced the memory usage by the `PREPARE` statement in point queries in the thread pool mode when the plan cache was enabled.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the error of unstable performance after hotspot update optimization was enabled.</li>
<li>Fixed the issue where `select count(*)` parallel scans caused full-table scans in extreme cases.</li>
<li>Fixed performance issues caused by execution plan changes due to reading zero statistics in various cases.</li>
<li>Fixed the bug where queries were in the `query end` status for a long time.</li>
<li>Fixed the bug where statistics were severely underestimated in long records.</li>
<li>Fixed the bug where an error was reported when the Temptable engine was used and the number of aggregate functions in the selected column exceeded 255.</li>
<li>Fixed the case sensitivity issue of column names in the `json_table` function.</li>
<li>Fixed the bug that caused correctness issues in window functions because expressions returned early during `return true`.</li>
<li>Fixed the correctness issue caused by the pushdown by `derived condition pushdown` when it contained user variables.</li>
<li>Fixed the issue where SQL filters were prone to crash when no namespaces were added in a rule.</li>
<li>Fixed the QPS jitters when the thread pool was enabled under high concurrency and high conflict.</li>
<li>Fixed the issue where source-replica buffer pool sync leaked file handles in extreme cases (when host file systems were corrupted).</li>
<li>Fixed the index mapping issue.</li>
<li>Fixed the statistics cache sync issue.</li>
<li>Fixed the crash when information was not cleared during execution of the `UPDATE` statement or stored procedures.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210830</td>
<td>
<ul><li>New features</li><ul>
<li>Supported limiting the number of preloaded rows.</li>
<li>Supported optimizing plan cache point query.</li>
<li>Supported extended ANALYZE syntax (UPDATE HISTOGRAM c USING DATA 'json') and direct writes to histograms.
</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Replaced index seek with histogram to reduce evaluation errors and I/O overheads (this capability is not enabled by default).</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where there might be no statistics information during online DDL.</li>
<li>Fixed the issue where generated columns on replica instances were not updated.</li>
<li>Fixed the issue where the instance hung when binlog was compressed.</li>
<li>Fixed the issue of missing GTID in the previous_gtids event of the newly generated binlog file.</li>
<li>Fixed possible deadlocks when system variables were modified.</li>
<li>Fixed the issue where the information of the SQL thread of the replica instance in SHOW PROCESSLIST was incorrectly displayed.</li>
<li>Implemented the bug fix related to hash join provided in MySQL 8.0.23.</li>
<li>Implemented the bug fix related to writeset provided in MySQL.</li>
<li>Implemented the bug fix related to the query optimizer provided in MySQL 8.0.24.</li>
<li>Fixed the concurrency bugs of optimizing flush list and releasing pages in FAST DDL.</li>
<li>Optimized the memory usage during data dictionary update in instances with a large number of tables.</li>
<li>Fixed the crash caused by new primary key creation after INSTANT ADD COLUMN.</li>
<li>Fixed the OOM caused by memory growth in full-text index query.</li>
<li>Fixed the issue where -1 was included in the TIME field in the result set returned by SHOW PROCESSLIST.</li>
<li>Fixed the issue where tables might fail to be opened due to histogram compatibility.</li>
<li>Fixed the floating point accumulation error when Singleton histograms were constructed.</li>
<li>Fixed the replication interruption caused by using many Chinese characters in the table name of a row format log.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210330</td>
<td>
<ul><li>New features</li><ul>
<li>Supported source-replica buffer pool sync: After a high-availability (HA) source-replica switch occurs, it usually takes a long time to warm up the replica, that is, to load hotspot data into its buffer pool. To accelerate the replica's warmup, TXSQL now supports the buffer pool sync between the source and the replica.</li>
<li>Supported sort-merge join.</li>
<li>Supported FAST DDL operations.</li>
<li>Supported querying the value of the `character_set_client_handshake` parameter.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the mechanism of scanning and flushing the dirty pages tracked in the flush list, so as to solve the performance fluctuation issue while creating indexes and thus improve the system stability.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the deadlocks caused by the modification of the `offline_mode` and `cdb_working_mode` parameters.</li>
<li>Fixed the persistent concurrency issue of the `max_trx_id` field in `trx_sys` table.</li>
</ul>
</td>
</tr>

<tr>	
<td>20201230</td>
<td>
<ul><li>New features</li><ul>
<li>Supported the official updates of MySQL <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-19.html" target="_blank">8.0.19</a>, <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-20.html" target="_blank">8.0.20</a>, <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-21.html" target="_blank">8.0.21</a>, and <a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-22.html" target="_blank">8.0.22</a>.</li>
<li>Supported dynamic setting of thread pooling mode or connection pooling mode by using the `thread_handling` parameter.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the `BINLOG LOCK_done` conflict to improve write performance.</li>
<li>Optimized the `trx_sys mutex` conflict by using lock-free hash to improve performance.</li>
<li>Optimized redo log flushing.</li>
<li>Optimized the buffer pool initialization time.</li>
<li>Optimized the clearing of adaptive hash indexes (AHI) during the `drop table` operations on big tables.</li>
<li>Optimized audit performance.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed performance fluctuation when cleaning InnoDB temporary tables.</li>
<li>Fixed the read-only performance decrease when the instance has many cores.</li>
<li>Fixed the error (error code: 1032) caused by hash scans.</li>
<li>Fixed concurrency security issues caused by hotspot update.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200630</td>
<td>
<ul><li>New features</li><ul>
<li>Supported async drop of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by dropping big tables. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported automatic killing of idle tasks to reduce resource conflicts. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported transparent data encryption (TDE).</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where switch failed due to inconsistent positions between `relay_log_pos` and `master_log_pos`.</li>
<li>Fixed the data file error caused by asynchronously storing data in the disk.</li>
<li>Fixed the hard error when `fsync` returned `EIO` and retries were made repeatedly.</li>
<li>Fixed the crash caused by phrase search under multi-byte character sets in full-text index.</li>
</ul>
</td>
</tr>
</tbody></table>
:::
::: MySQL 5.7 Kernel Version Release Notes
<table>
<thead><tr><th>Minor Version</th><th>Description</th></tr></thead>
<tbody>

<tr>	
<td>20220716</td>
<td>
<ul><li>New features</li><ul>
<li>Supported auto-increment column persistence for InnoDB.</li>
<li>Supported precise memory statistics.</li>
<li>Supported query-level memory monitoring.</li>
<li>Supported recycle bin. </li>
<li>Supported parallel DDL statements.</li>
<li>Supported flashback query.</li>
<li>Supported async rollback for internal XA transactions.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized async drop of big tables.<br>The original definition of big table is 50 GB, which can now be controlled by the `innodb_async_table_size` to make it more flexible.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where `ERROR 1878 (HY000): Temporary file write failure` was reported when `alter table` was executed to create indexes.</li>
<li>Fixed the issue where buf/buf/pool couldn't be viewed in PFS memory monitoring data.</li>
<li>Fixed the issue where the returning statement might cause exceptions in some scenarios due to permission checks.</li>
<li>Fixed the issue where an error was reported because the parser did not correctly handle semicolons in statements.</li>
<li>Fixed the issue where single quotation marks in audit statements were not escaped. </li>
<li>Fixed the issue of sudden memory usage increase on the ARM platform.</li>
<li>Fixed the issue of source-replica inconsistency caused by modifying `binlog_format` after writeset was enabled.</li>
<li>Fixed the issue of high CPU usage caused by exiting a large number of threads at the same time.</li>
<li>Fixed bugs related to `drop table partition force`.</li>
<li>Fixed the issue where binlog dump got stuck and caused the instance restart to become slow.</li>
<li>Fixed the issue where the source-replica sync failed because `create table like temporary table` did not inherit the character set in the binlog.</li>
<li>Fixed the issue where `show detail processlist` displayed illegal characters.</li>
<li>Fixed the issue where the `thread_group` lock was not released when the thread pool was closed in some cases.</li>
<li>Fixed the issue where updating the parent table at the parallel table level caused the instance to run abnormally.</li>
<li>Fixed the issue where virtual columns were calculated incorrectly on the replica.</li>
<li>Fixed the issue where `gtid_subset` did not set `null_value` to `false` after executing a row.</li>
</ul>
</td>
</tr>

<tr>	
<td>20211230</td>
<td>
<ul><li>New features</li><ul>
<li>Supported the official updates of MySQL <a href="https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-19.html" target="_blank">5.7.19</a>–<a href="https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-36.html" target="_blank">5.7.36</a>.</li>
<li>Supported source-replica buffer pool sync to speed up the performance recovery after HA switch (around 90 seconds faster than that in native mode).</li>
<li>Added the backup lock feature to provide lightweight metadata locks to improve the service availability during backup.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Made functions related to `utf8/utf8mb4 my_charpos` inline to optimize the performance of UTF_8 functions in read_write scenarios.
<li>Upgraded jemalloc to v5.2.1.</li>
<li>Optimized file number acquisition during binlog rotation.</li>
<li>Optimized semi-sync replica I/O.</li>
<li>Optimized hash scan aggregation.</li>
<li>Accelerated the startup of crash recovery for large transactions.</li>
</ul>

<tr>	
<td>20211102</td>
<td>
<ul><li>New features</li><ul>
<li>Fixed the exception of the third-party data subscription tool caused by subscription to the comparison SQL for internal data consistency during tool usage. <dx-alert infotype="explain" title="Note">After the database instance is migrated, upgraded, or recovered after failure, the system will compare the data to ensure data consistency. When comparison SQL is in `statement` mode, exceptions are prone to occur in response of some third-party subscription tools to the SQL in `statement` mode. When the instance is upgraded to its kernel, the third-party data subscription tool can't subscribe the comparison SQL for internal data consistency.</dx-alert></li>
</ul>
</td>
</tr>

<tr>	
<td>20211031</td>
<td>
<ul><li>New features</li><ul>
<li>Supported writeset replication.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the checkpoint mechanism to increase the backup success rate.</li>
<li>Optimized the hash scan index selection.</li>
<li>Optimized the hotspot update performance to support `insert on duplicate key update`.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the error of unstable performance after hotspot update was enabled.</li>
<li>Fixed the crash caused by rolling back the UPDATE operation after an instant DDL.</li>
<li>Fixed the issue where the `CREATE TABLE AS SELECT` statement didn't inherit the compression attribute after column compression was enabled.</li>
<li>Fixed the instance crash caused by the `show variables like 'tencent_root%'` statement after the `skip-grant-table` option was enabled.</li>
<li>Fixed the crash of the Query Rewriter plugin in read-only mode.</li>
<li>Fixed the error (error code: 1032) caused by hash scans in partitioned tables.</li>
<li>Fixed the issue where the first large transaction's SBM was 0 in MTS mode.</li>
<li>Fixed the crash of `stop slave` caused by `slave_preserve_commit_order=ON, slave_transaction_retries=0`.</li>
<li>Fixed several XA transaction bugs.</li>
<li>Fixed the issue where SQL splicing went wrong during `show create` after a JSON field with a default value was created.</li>
<li>Fixed the issue where disconnected transactions could not be rolled back after transactions were blocked.</li>
<li>Fixed the issue where there might be no statistics information for long records in InnoDB persistent mode.</li>
<li>Ported 8.0 to fix the issue where `ANALYZE TABLE` might cause query retention.</li>
<li>Fixed the issue where the InnoDB statistics couldn't be synced to the server layer in time after change.</li>
<li>Fixed the issue where statistical sampling might block writes for too long and cause a crash (bug# 31889883).</li>
<li>Fixed the possibility of reading zero rows during the InnoDB statistics update process (bug# 105224).</li>
<li>Fixed the possible O(N^2) behavior in MVCC (bug# 28825617).</li>
<li>Fixed the crash caused by closing a temp table and triggering binlog rotation when a connection was released.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210630</td>
<td>
<ul><li>New features</li><ul>
<li>Added the new command SHOW SLAVE DETAIL [FOR CHANNEL channel] for displaying the binlog timestamp that the current replica has replayed.</li>
<li>Supported transaction_read_only/transaction_isolation parameters.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Accelerated the application of hash scan on replicas by aggregating multiple identical binlog events.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where duplicate primary keys existed, columns couldn't be found, and columns were too long in temp tables caused by the `UPDATE` statement.</li>
<li>Fixed the issue where there might be no statistics information during the DDL process.</li>
<li>Fixed the inaccurate undo log size in connection status statistics.</li>
<li>Fixed the instance crash caused by querying the metadata_locks table.</li>
<li>Modified `of` as a non-reserved keyword.</li>
<li>Fixed the issue where the dynamically modified version number was not invalidly displayed in new connections.</li>
<li>Fixed the issue where the wild pointer was accessed during page_cache cleanning.</li>
<li>Fixed the issue where the execution of ALTER TABLE might report the "Incorrect key file for table" error.</li>
<li>Fixed the excessive memory usage by partitioned tables.</li>
<li>Fixed the issue where -1 was included in the TIME field in the result set returned by SHOW PROCESSLIST.</li>
<li>Fixed the lock wait of XA transaction replication on replica nodes.</li>
<li>Fixed the incorrect lock of partitioned tables in equal range query.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210331</td>
<td>
<ul><li>New features</li><ul>
<li>Supported `RETURNING` clause in a `DELETE`, `INSERT`, or `REPLACE` statement to return information about the rows that were deleted or modified.by the statement. For `DELETE`, undo data is returned, while for `INSERT` or `UPDATE`, redo data is returned.</li>
<li>Supported column compression: Row compression and data page compression are already supported, but if small fields in a table are read and written frequently while big fields are not, both of the compression methods waste a lot of computing resources. In contrast, column compression can compress big fields that are infrequently accessed and reduce the space for storing whole rows of fields, so as to improve read and write access efficiency.</li>
<li>Supported querying the value of the `character_set_client_handshake` parameter.</li>
<li>Supported the manual cleaning of page cache occupied by log files by using the `posix_fadvise()` function based on the sliding window technique, so as to lower the memory pressure on the operating system and improve instance stability.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the parallelism of CREATE INDEX: A merge sort is needed in a temp table in the process of creating indexes, which is time-consuming. The parallel temp-table merge sort algorithm is now supported to reduce the time by more than 50%.</li>
<li>Optimized the mechanism of scanning and flushing the dirty pages tracked in the flush list, so as to solve the performance fluctuation issue while creating indexes and thus improve the system stability.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the memory leak issue.</li>
<li>Implemented the JSON bug fixes provided in MySQL 8.0 to improve the stability of using JSON.</li>
<li>Fixed the error (error code: 1032) caused by hash scans.</li>
<li>Fixed concurrency security issues caused by hotspot update.</li>
<li>Implemented the gcol bug fixes provided by MySQL in batches.</li>
<li>Fixed the failure to compare DateTime data with String data in some cases.</li>
<li>Fixed the bug where file handles cannot be released if source-replica buffer pool sync is enabled.</li>
<li>Fixed the deadlocks caused by setting the `offline_mode` parameter and creating connections at the same time.</li>
<li>Fixed the crashes caused by the `m_end_range` parameter incorrectly set in concurrent range queries.</li>
<li>Fixed the issue where it takes a long time to execute an `UPDATE` statement on a temp table if a JSON column appears in the `GROUP BY` clause.</li>
</ul>
</td>
</tr>

<tr>	
<td>20201231</td>
<td>
<ul><li>New features</li><ul>
<li>Supported using `NOWAIT` and `SKIP LOCKED` in `SELECT FOR UPDATE/SHARE`.</li>
<li>Supported dynamic setting of thread pooling mode or connection pooling mode by using the `thread_handling` parameter.</li>
<li>Supported source-replica buffer pool sync.</li>
<li>Supported monitoring of user connection status. Monitoring items include sync/async IO, memory, log size, CPU time, and lock duration.
</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the transaction subsystem to improve the high concurrency performance.</li>
<li>Optimized the time to start crash recovery for large transactions.</li>
<li>Optimized redo log flushing.</li>
<li>Optimized the buffer pool initialization time.</li>
<li>Optimized UTF8/UTF8MB4 string efficiency.</li>
<li>Optimized audit performance.</li>
<li>Revoked the restriction on the value of `gtid_purged` being empty.</li>
<li>Optimized the backup lock. `LOCK TABLES FOR BACKUP`, `LOCK BINLOG FOR BACKUP`, and `UNLOCK BINLOG` are supported. `FLUSH TABLES WITH READ LOCK` is used to take a backup of the database, but it blocks the whole database from providing service. In contrast, the three statements above use a lightweight backup lock to ensure data consistency during physical/logical backup while allowing the database to providing service.</li>
<li>Optimized the `drop table` operations on big tables.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the hang issue when querying `performance_schema`.</li>
<li>Fixed the overflow issue of the `digest_add_token` function.</li>
<li>Fixed the crash caused by ibuf access when the `TRUNCATE TABLE` command was executed.</li>
<li>Fixed the query correctness issue caused by const propagation when `LEFT JOIN` statement is used.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200930</td>
<td>
<ul><li>Performance optimizations</li><ul>
<li>Optimized the backup lock. `FLUSH TABLES WITH READ LOCK` is used to take a backup of the database, but it blocks the whole database from providing service. Therefore, a lightweight backup lock is provided in this version.</li>
<li>Optimized the `drop table` operations on big tables. The `innodb_fast_ahi_cleanup_for_drop_table` parameter helps significantly reduce the time it takes to clean up adaptive hash indexes when dropping big tables.
</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the crash caused by ibuf access when TRUNCATE TABLE was executed.</li>
<li>Fixed cold backup failures when the quick column adding feature was enabled.</li>
<li>Fixed performance degradation caused by frequently releasing InnoDB memory table objects.</li>
<li>Fixed the query correctness issue caused by const propagation when `LEFT JOIN` statement is used.</li>
<li>Fixed the core issue caused by rule class name conflict between SQL throttling and query rewrite.</li>
<li>Fixed the concurrent update issue caused by the `INSERT ON DUPLICATE KEY UPDATE` statement in multiple sessions.</li>
<li>Fixed the `duplicate key error` caused by concurrent INSERTs when `auto_increment_increment` is used.</li>
<li>Fixed the crashes caused by evicting InnoDB memory objects.</li>
<li>Fixed concurrency security issues caused by hotspot update.</li>
<li>Fixed the coredump issue when enabling the thread pool after jemalloc was upgraded to v5.2.1.</li>
<li>Fixed the incomplete audit log issue caused by fwrite error-free handling.</li>
<li>Fixed the issue where `mysqld_safe` failed to print logs when it was started by a root user.</li>
<li>Fixed the increase in the size of the DDL log file caused by `ALTER TABLE EXCHANGE PARTITION`.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200701</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the INNOBASE_SHARE index mapping error.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200630</td>
<td>
<ul><li>New features</li><ul>
<li>Supported using `NOWAIT` and `SKIP LOCKED` in `SELECT FOR UPDATE/SHARE` statements.</li>
<li>Supported large transaction optimization, which can solve such problems as source-replica delay and backup failures caused by large transactions.</li>
<li>Optimized audit performance to support async audit.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the overflow of the `digest_add_token` function.</li>
<li>Fixed the instance crash caused by `insert blob`.</li>
<li>Fixed the source-replica replication interruption when a hash scan failed to find the record while updating the same row in an event.</li>
<li>Fixed the hang issue when querying `performance_schema`.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200331</td>
<td>
<ul><li>New features</li><ul>
<li>Added the official MySQL 5.7.22 JSON series functions.</li>
<li>Supported the hotspot update feature as described in <a href="https://www.tencentcloud.com/document/product/1035/48638" target="_blank">Real-Time Session</a> for ecommerce flash sale scenarios.</li>
<li>Supported the SQL throttling feature as described in <a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">Real-Time Session</a>.</li>
<li>Supported encryption with custom KMS keys.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the crash caused by phrase search under multi-byte character sets in full-text index.</li>
<li>Fixed the crash of the CATS lock scheduling module in high-concurrency scenarios.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190830</td>
<td>
<ul><li>New features</li><ul>
<li>Supported skipping the corrupted data and continuing to parse when a binlog is corrupted. If the source instance and binlog are both damaged, this feature helps restore data from the replica database for use as much as possible.</li>
<li>Supported syncing data from non-GTID to GTID mode.</li>
<li>Supported querying the "user thread memory usage" by executing the `SHOW FULL PROCESSLIST` statement.</li>
<li>Supported quick column adding for tables as described in <a href="https://intl.cloud.tencent.com/document/product/236/35988" target="_blank">Overview</a>. This feature does not replicate the data or use disk capacity/IO, and can implement changes in real time during peak hours.</li>
<li>Supported persistent auto-increment values.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where replication would be interrupted if the column name in a `GRANT` statement contained reserved words.</li>
<li>Fixed the issue where SQL execution efficiency dropped when reverse scan was performed on a partitioned table.</li>
<li>Fixed the issue where the query result had an exception due to data inconsistency when using virtual column index and primary key.</li>
<li>Fixed the issue where data was missing due to InnoDB primary key range queries.</li>
<li>Fixed the issue where the system crashed when a DDL statement was executed for a table with spatial indexes.</li>
<li>Fixed the issue where source-replica disconnection occurred when the binlog size was too large and the file length in the heartbeat information exceeded the limit.</li>
<li>Fixed the issue where other events could not be executed as scheduled when an event was deleted.</li>
<li>Fixed the issue where the aggregate query result was incorrect.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190615</td>
<td>
<ul><li>New features</li><ul>
<li>Supported transparent data encryption (TDE).</li>
</ul>
</td>
</tr>

<tr>	
<td>20190430</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the issue where null pointer reference occurred when the LONGTEXT feature was used in subqueries.</li>
<li>Fixed the issue where source-replica disconnection occurred due to hash scan.</li>
<li>Fixed the issue where the replica I/O thread was interrupted due to source binlog switch.</li>
<li>Fixed the crash caused by the use of `NAME_CONST`.</li>
<li>Fixed the illegal mix of collation error caused by character set.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190203</td>
<td>
<ul><li>New features</li><ul>
<li>Supported async drop of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by dropping big tables. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported CATS lock scheduling.</li>
<li>Supported creating and dropping temp tables and CTS syntax in transactions when GTID is enabled. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported implicit primary keys. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported users without super privileges to kill sessions of other users by configuring the `cdb_kill_user_extra` parameter (default value: `root@%`).</li>
<li>Supported enterprise-grade encryption functions. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where replication was interrupted when binlog cache file ran out of space.</li>
<li>Fixed the hard error when `fsync` returned `EIO` and retries were made repeatedly.</li>
<li>Fixed the issue where replication was interrupted and could not be recovered due to GTID holes.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180918</td>
<td>
<ul><li>New features</li><ul>
<li>Supported automatic killing of idle transactions to reduce resource conflicts. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported automatically changing the storage engine from MEMORY to InnoDB: If the global variable `cdb_convert_memory_to_innodb` is `ON`, the engine will be changed from MEMORY to InnoDB when a table is created or modified.</li>
<li>Supported invisible indexes.</li>
<li>Supported memory management with jemalloc, which can replace the jlibc memory management module to reduce memory usage and improve allocation efficiency.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized binlog switch to reduce the `rotate` lock duration and improve system performance.</li>
<li>Accelerated the crash recovery.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where an event became invalid due to source-replica switch.</li>
<li>Fixed the crash caused by `REPLAY LOG RECORD`.</li>
<li>Fixed the issue where the query result was incorrect due to loose index scans.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180530</td>
<td>
<ul><li>New features</li><ul>
<li>Supported SQL auditing.</li>
<li>Supported table-level concurrent replication. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized replica instance locks to improve the sync performance of replica instances.</li>
<li>Optimized the pushdown of the `SELECT ... LIMIT` statement.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where switch failed due to inconsistent positions between `relay_log_pos` and `master_log_pos`.</li>
<li>Fixed the crash caused by `Crash on UPDATE ON DUPLICATE KEY`.</li>
<li>Fixed the `Invalid escape character in string.` error when a JSON column was imported.</li>
</ul>
</td>
</tr>

<tr>	
<td>20171130</td>
<td>
<ul><li>New features</li><ul>
<li>Supported the `information_schema.metadata_locks` view to query the MDL grant and wait status in the current instance.</li>
<li>Supported the `ALTER TABLE NO_WAIT | TIMEOUT` syntax to grant DDL operations wait timeout. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported thread pool. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the error of `innodb_buffer_pool_pages_data` parameter overflow by calculating it based on `bytes_data`.</li>
<li>Fixed the issue where speed limit plugin became unavailable in async mode.</li>
</ul>
</td>
</tr>

</tbody></table>
:::
::: MySQL 5.6 Kernel Version Release Notes
<table>
<thead><tr><th>Minor Version</th><th>Description</th></tr></thead>
<tbody>

<tr>	
<td>20220303</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the abnormal release when the memory allocated by `mem_strdup` was used for `row_mysql_truncate_t::file_name` during async drop of big tables.</li>
</ul>
</td>
</tr>

<tr>	
<td>20220302</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the memory leak issue in `sql_update.cc`.</li>
</ul>
</td>
</tr>

<tr>	
<td>20220301</td>
<td>
<ul><li>New features</li><ul>
<li>Supported dynamically configuring the spin cycle (0–100) with the dynamic parameter `innodb_spin_wait_pause_multiplier`. <br>This parameter is used for temporary adjustment and does not support fixing the change through the console.</li>
<li>Supported printing deadlock loop information.<br>After this feature is enabled through the parameter `innodb_print_dead_lock_loop_info`, when a deadlock occurs, you can run `show engine innodb status` to view the deadlock loop information.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the issue where anonymous GTID transactions were generated in memory tables after replica restart.</li>
<li>Fixed the issue where upgrade failed due to the missing `root@localhost` permission.</li>
<li>Fixed the issue where the values of monitoring variables such as `innodb_row_lock_current_waits` were abnormal.</li>
<li>Fixed the SQL type mapping error in the audit plugin.</li>
</ul>
</td>
</tr>

<tr>	
<td>20211030</td>
<td>
<ul><li>New features</li><ul>
<li>Supported large transaction replication optimization.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Accelerated the application of hash scan.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the OOM caused by a large number of table queries.</li>
<li>Fixed the infinite loop error caused by setting `innodb_thread_concurrecy` to 0.</li>
<li>Fixed the issue where there were no statistics information for long records.</li>
<li>Fixed the SBM jump error.</li>
<li>Fixed the `LOCK_binlog_end_pos hang` error.</li>
</ul>
</td>
</tr>

<tr>	
<td>20210630</td>
<td>
<ul><li>New features</li><ul>
<li>Supported large transaction replication optimization.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the incorrect copy when Index Merge was enabled.</li>
<li>Fixed the issue where the replication would be interrupted if the execution of CREATE TABLE SELECT was interrupted when `cdb_more_gtid_feature_supported` was enabled in row mode.</li>
<li>Fixed the bug that `max(id)` was greater than AUTO_INCREMENT in SHOW CREATE TABLE.</li>
</ul>
</td>
</tr>

<tr>	
<td>20201231</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the error (error code: 1032) caused by hash scans.</li>
<li>Fixed the issue where the source-replica auto-increment values were inconsistent due to the `REPLACE INTO` statement in `ROW` format.</li>
<li>Fixed the memory leak caused by not freeing up the memory requested for parsing SQL statements.</li>
<li>Fixed the issue where the sql_mode check is skipped when running `CREATE TABLE AS SELECT`.</li>
<li>Fixed the issue where the `sql_mode` check was skipped when inserting default values.</li>
<li>Fixed the issue where the `sql_mode` check was skipped when running UPDATE with bound parameters.</li>
</ul>
</td>
</tr>

<tr>	
<td>20200915</td>
<td>
<ul><li>New features</li><ul>
<li>Supported the SQL throttling feature as described in <a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">Real-Time Session</a>.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the initialization acceleration of buffer pool.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the hang issue of `rename table` on both source and replica.</li>
<li>Fixed the crash when `event_scheduler` was set to `disable` and `cdb_skip_event_scheduler` was changed from `on` to `off`.</li>
<li>Fixed the `sync_wait_array` assertion failure when the maximum number of connections of `tencentroot` was not counted in `srv_max_n_threads`.</li>
<li>Fixed the crash of source-replica parallel replication caused by the system table structure inconsistency between TencentDB for MySQL 5.6 and other cloud vendors' MySQL 5.6.</li>
<li>Fixed the `INSERT ON DUPLICATE KEY UPDATE THE WRONG ROW` error.</li>
<li>Fixed the `index_mapping` error.</li>
<li>Fixed the MTR failure.</li>
<li>Fixed the source-replica replication interruption when a hash scan failed to find the record while updating the same row in an event.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190930</td>
<td>
<ul><li>New features</li><ul>
<li>Supported querying the user thread memory usage by executing the `SHOW FULL PROCESSLIST` statement.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed GTID holes caused by the replication filter of the replica.</li>
<li>Fixed the issue where source-replica disconnection occurred when the binlog size was too large and the file length in the heartbeat information exceeded the limit.</li>
<li>Fixed the illegal mix of collation error caused by character set.</li>
<li>Fixed the issue where the source-replica disconnection occurred due to hash scan.</li>
<li>Fixed the crash caused by the use of `NAME_CONST`.</li>
<li>Fixed the issue where the replica I/O thread was interrupted due to source binlog switch.</li>
<li>Fixed the error of incompatible backups due to `innodb_log_checusum`.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190530</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the issue where dirty data might be read in RC mode.</li>
<li>Fixed the issue where replica instance replay might fail due to the drop of temp table.</li>
<li>Fixed the deadlock issue under high concurrency.</li>
</ul>
</td>
</tr>

<tr>	
<td>20190203</td>
<td>
<ul><li>New features</li><ul>
<li>Supported async drop of big tables. You can clear files asynchronously and slowly to avoid business performance fluctuation caused by dropping big tables. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported users without super privileges to kill sessions of other users by configuring the `cdb_kill_user_extra` parameter (default value: `root@%`).</li>
<li>Supported creating and dropping temp tables and CTS syntax in transactions when GTID is enabled. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Optimized the replication and replay of partitioned tables to improve efficiency.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the source-replica data inconsistency issue caused by insufficient temporary space.</li>
<li>Fixed the issue of suspended hot record updates.</li>
<li>Fixed the issue where the value of `Seconds_Behind_Master` was abnormal during concurrent replication.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180915</td>
<td>
<ul><li>New features</li><ul>
<li>Supported automatically changing the storage engine from MEMORY to InnoDB: If the global variable `cdb_convert_memory_to_innodb` is `ON`, the engine will be changed from MEMORY to InnoDB when a table is created or modified.</li>
<li>Supported automatic killing of idle transactions to reduce resource conflicts. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the crash caused by `REPLAY LOG RECORD`.</li>
<li>Fixed the error of time data inconsistency between source and replica due to decimal precision issues.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180130</td>
<td>
<ul><li>New features</li><ul>
<li>Supported thread pool. To apply for this feature, <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</li>
<li>Supported dynamically modifying replication filtering rules for replica nodes.</li>
</ul>

<li>Performance optimizations</li><ul>
<li>Reduced performance fluctuation caused by `DROP TABLE`.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the database crash caused by authentication password strings.</li>
</ul>
</td>
</tr>

<tr>	
<td>20180122</td>
<td>
<ul><li>New features</li><ul>
<li>Supported SQL auditing.</li>
</ul>

<li>Bug fixes</li><ul>
<li>Fixed the integer overflow issue.</li>
<li>Fixed the error caused by queries using full-text index.</li>
<li>Fixed the issue where the replica crashed during replication.</li>
</ul>
</td>
</tr>

<tr>	
<td>20170830</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the issue where binlog speed limit became invalid in async mode.</li>
<li>Fixed the issue where the `buffer_pool` status was abnormal.</li>
<li>Fixed the issue where `SEQUENCE` and implicit primary key conflicted.</li>
</ul>
</td>
</tr>

<tr>	
<td>20170228</td>
<td>
<ul><li>Bug fixes</li><ul>
<li>Fixed the character encoding bug in `DROP TABLE`.</li>
<li>Fixed the issue where a table contained symbols like decimal points or `replicate-wild-do-table` couldn't be used to filter databases correctly.</li>
<li>Fixed the issue where SQL threads exited too early after the replica had a `rotate` event.</li>
</ul>
</td>
</tr>

<tr>	
<td>20161130</td>
<td>
<ul><li>Performance optimizations</li><ul>
<li>Split the `lock_log` lock to reduce the time used by lock logs and improve the concurrency performance.</li>
<li>Separated the ACK thread of the source to reduce the response time.</li>
<li>Prohibited the user thread from being killed while waiting for ACK in order to prevent phantom reads.</li>
<li>Fixed the unnecessary `lock_sync` lock when `sync_binlog != 1`.</li>
</ul>
</td>
</tr>

</tbody></table>
:::
</dx-tabs>
