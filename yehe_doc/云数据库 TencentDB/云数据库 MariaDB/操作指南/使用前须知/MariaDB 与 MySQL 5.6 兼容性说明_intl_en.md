## Compatibility of TencentDB for MariaDB with Open-source MariaDB
TencentDB for MariaDB is fully compatible with open-source MariaDB.

## Compatibility of TencentDB for MariaDB with MySQL 5.6
TencentDB for MariaDB is highly compatible with MySQL 5.6; therefore, code, applications, drivers, and tools that apply to MySQL databases can be directly used in TencentDB for MariaDB with no or only slight change required.
- Data files and table definition files are binary compatible.
- All client APIs and protocols are compatible.
- All filenames, binary files, paths, and port numbers are the same.
- All connectors (including those for PHP, Perl, Python, Java, .NET, Ruby, and MySQL) can be used in TencentDB for MariaDB with no modification required.
- You can use a MySQL client to connect to TencentDB for MariaDB.

## Incompatibility of TencentDB for MariaDB with MySQL 5.6
Binlogs in TencentDB for MariaDB are in row format, while in native MySQL and MariaDB, they are in statement format by default.

### 1. GTID incompatibility
`GTID` of TencentDB for MariaDB is incompatible with that of MySQL 5.6, i.e., MySQL cannot be used as a slave database of TencentDB for MariaDB.

### 2. Different default binlog configurations
Binlogs in TencentDB for MariaDB are in row format, while in MySQL and MariaDB, they are in statement format by default.

### 3. Row-based or command-based replication of the `CREAT TABLE ... SELECT` command
To ensure that the `CREAT TABLE ... SELECT` command can work properly in both row-based and command-based replication, this command in TencentDB for MariaDB will be converted to and executed as the `CREAT OR RPLACE` command in a slave database. The advantage of this mechanism is that the slave database can run properly after recovery from downtime.

#### 3.1. Default value deduction
When you create tables by using the `Create table ... Select from` statement, the differences between the default values of fields in `varchar(N)` type are as follows:
- The fields do not have a default value in MariaDB 10.1.
- The default value in MySQL 5.7 is `NULL`.
- The default value in MySQL 5.5 or 5.6 is an empty string ('').

Default value of a decimal column: in MySQL 5.5 and 5.6, it is deduced to 0.00; in MariaDB 10.1, it is deduced to NULL.

Sample code:
```
---------------- MySQL 5.5 -----------------------
create table t1
select least(_latin1'a',_latin2'b',_latin5'c' collate latin5_turkish_ci) as f1; 
show create table t1; 
Table   Create Table
t1  CREATE TABLE `t1` (
  `f1` varchar(1) CHARACTER SET latin5 NOT NULL DEFAULT ''
) ENGINE=MyISAM DEFAULT CHARSET=latin1
-------------------- MySQL 5.7 ---------------------------------
create table t1
select least(_latin1'a',_latin2'b',_latin5'c' collate latin5_turkish_ci) as f1; 
show create table t1; 
Table   Create Table
t1  CREATE TABLE `t1` (
  `f1` varchar(1) CHARACTER SET latin5 DEFAULT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1
------------------- MariaDB 10.1* --------------------------------
create table t1
select least(_latin1'a',_latin2'b',_latin5'c' collate latin5_turkish_ci) as f1; 
show create table t1; 
Table   Create Table
t1  CREATE TABLE `t1` (
  `f1` varchar(1) CHARACTER SET latin5 NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1


```

#### 3.2. Differences in processing `select` statements in subqueries
In this statement: `SELECT a AS x, ROW(11, 12) = (SELECT MAX(x), 12), ROW(11, 12) IN (SELECT MAX(x), 12) FROM t1;`

- In MySQL 5.5 and 5.6, the subquery `SELECT MAX(x), 12` is considered as `SELECT MAX(x), 12 from t1` if it is located after `in`; it is considered as `SELECT x, 12` if it is located after `=`, where "x" is the alias of `a` in the current row.
- In MySQL 5.7 and MariaDB 10.1.*, the subquery `SELECT MAX(x), 12` always equals `SELECT x, 12`, where `x` is the alias of `a` in the current row.

Sample code:
```
----------------- MySQL 5.5/5.6 -----------------------
CREATE TABLE t1 (a INT);
INSERT INTO t1 VALUES (1), (2), (11);
SELECT a AS x, ROW(11, 12) = (SELECT MAX(x), 12), ROW(11, 12) IN (SELECT MAX(x), 12) FROM t1;
x   ROW(11, 12) = (SELECT MAX(x), 12)   ROW(11, 12) IN (SELECT MAX(x), 12)
1   0   1
2   0   1
11  1   1
--------------------------- MariaDB 10.1.* or MySQL 5.7------------------------------
CREATE TABLE t1 (a INT);
INSERT INTO t1 VALUES (1), (2), (11);
SELECT a AS x, ROW(11, 12) = (SELECT MAX(x), 12), ROW(11, 12) IN (SELECT MAX(x), 12) FROM t1;
x   ROW(11, 12) = (SELECT MAX(x), 12)   ROW(11, 12) IN (SELECT MAX(x), 12)
1   0   0
2   0   0
11  1   1
```

#### 3.3. Processing of `NULL` for `ALL` and `SOME`
In MySQL 5.5, the `NULL` in `10 >=  ALL (NULL, 1, 10)` or `1 <= ALL (NULL, 1, 10)` is skipped, i.e., it is considered as non-existent, because `NULL` is incomparable.
In MySQL 5.7 and TencentDB for MariaDB, `NULL` is an unknown value and the result in the comparisons above is unknown too; therefore, `NULL` will be returned.

#### 3.4. `alter table inplace` operation
When `alter table` is used to change the sequence of columns only, the `inplace` algorithm can be used in TencentDB for MariaDB but not in MySQL.
When `inplace alter table` is executed in TencentDB for MariaDB, the result of running `show create table t1` will be the same as that of running `ALGORITHM=COPY` in MySQL.

### 4. Undefined behavior in MySQL and TencentDB for MariaDB
Undefined behavior is a feature of behavior that can be implemented through any method in MySQL or TencentDB for MariaDB, which may vary by version without the need to notify users or be specified. Implementation of undefined behaviors by MySQL and TencentDB for MariaDB may produce the same or different results.

For such same or different results in the current and future versions, TencentDB for MariaDB does not guarantee the results or ensure the same kernel optimization. For more information, please see [official description of undefined behaviors](https://mariadb.com/kb/en/mariadb/mariadb-vs-mysql-compatibility/).


#### 4.1. Case-insensitive sorting of character-type columns
Sorting (`order by` clause) of character-type columns is generally case-insensitive, which means that the order of fields with the same content but different letter cases will be undefined after sorting. You can use the `BINARY` keyword to force implement case-sensitive sorting, i.e., `ORDER BY BINARY column name`.

Sample code:
```
The sorting of the following samples in MySQL and TencentDB for MariaDB may be completely random:
mysql> SELECT email FROM t2 LEFT JOIN t1  ON kid = t2.id WHERE t1.id IS NULL order by email;

+-------+
| email |
+-------+
| email |
| eMail |
| EMail |
+-------+
3 rows in set (0.00 sec)
```

#### 4.2. Differences in processing `Auto_increment` field overflow
Undefined behavior specific to InnoDB:
- In all auto-increment column lock modes (0, 1, 2), the auto-increment behavior will be considered undefined if you set the auto-increment column field to a negative value.
- In all auto-increment column lock modes (0, 1, 2), the auto-increment behavior will be considered undefined if the value of the auto-increment column field is greater than the maximum integer that can be stored as integer type in the column.

>Do not insert (incorrect) numbers into an auto-increment column.

#### 4.3. Differences in statistics collection method for `FOUND ROWS`
The returned value of `FOUND_ROWS()` will be accurate only when `UNION ALL` is used in the query statement.
If **only `UNION` is used without `ALL`, TencentDB for MariaDB will remove duplicates in the statistics, while MySQL will retain duplicates**. If the `UNION` query statement is used without the `LIMIT` clause, the `SQL_CALC_FOUND_ROWS` keyword will be ignored, and the returned result of `FOUND_ROWS()` will be the number of rows in the temporary table created when `UNION` is executed.

#### 4.4. Differences in locking sequence of the `LOCK TABLES` statement
The `LOCK TABLES` statement locks tables in the following method: first, all tables that need to be locked are sorted based on the internally-defined method; however, from user's perspective, the sorting order in MySQL and TencentDB for MariaDB is undefined. For example, if you write `LOCK TABLES t1, t2, t3`, TencentDB for MariaDB and MySQL will not lock the tables according to the sequence of `t1, t2, t3`.
This behavior is undefined in MySQL and TencentDB for MariaDB; therefore, they may use different methods to sort t1, t2, and t3 and lock them based on the resulting sequence.

Therefore, you should not rely on locking sequence to ensure accuracy in your stored procedures or query code, as this may cause deadlock.

#### 4.5. Timing for running the `RESET MASTER` statement
You cannot run `RESET MASTER` when any duplicate slave server is running; otherwise, the behaviors of master and slave servers will be undefined (and not supported) in TencentDB for MariaDB and MySQL. Various predictable errors may or may not occur during execution of `RESET MASTER`. The official development teams of TencentDB for MariaDB and MySQL do not consider these errors as bugs and are not responsible for any errors that actually occur in this way. 

#### 4.6. Conversion of date and time types to year type
In MySQL 5.5, when variables in year and date types are compared, the date type will be converted to the year type. For example, "2011-01-01" will be converted to "2011".

In MySQL 5.7 and TencentDB for MariaDB, variables in date type will stay unchanged; therefore, comparisons with variables in year type are different.
Similarly, TencentDB for MariaDB cannot convert the time type to year type, while MySQL 5.6 uses the year part in the timestamp of the current session as the year value for every value in time type, which means that the year in the timestamp of the current session will be used every time a time-type value needs to be converted to year type.

#### 4.7. Processing method of unknown characters
- Character encoding conversion is implemented in different ways in different versions of MySQL and TencentDB for MariaDB. For example, if an encoding byte string is not recognized by `unhex`, an empty string ('') will be returned in MySQL 5.5/5.6/5.7, while a question mark character (?) will be returned in MariaDB 10.1.
- The `UPDATE t1 SET a=unhex(code) ORDER BY code` statement assigns a value to field `a` in table t1; however, some of the assignment operations will fail as `unhex` can only recognize and convert byte strings within a certain range.
 - The default storage engine in MySQL 5.5 is MyISAM, which does not support transactions. Therefore, the statement will exit when it fails to assign a value to `a` in any row in t1; however, all assigned values will be still stored in t1.
 - The default storage engine in MySQL 5.7 is InnoDB; therefore, the transaction will be rolled back when the statement fails to assign a value to `a` in any row in t1, i.e., all assigned values will be rolled back as well.
 - The default storage engine in TencentDB for MariaDB is InnoDB. When `unhex` is unable to find a corresponding character for a byte string, a question mark (?, i.e., 0x3F) will be returned; therefore, the operation will always succeed no matter whether the storage engine is InnoDB or MyISAM.
- When inserting a hexadecimal string using the `insert into` statement, if the corresponding `utf8mb4` character is not found:
 - If the HEAP storage engine is used in MySQL 5.5/5.6, this unknown character will be ignored.
 - MariaDB 10.1 and MySQL 5.7 will use 0x3F (i.e., question mark "?") to replace this character.
- For an invalidly encoded string field, MySQL with the InnoDB storage engine will directly return an error, while TencentDB for MariaDB will replace the field with 3F and then insert it.

#### 4.8. Precision of time type
``` 
SELECT CAST(CAST('10:11:12.098700' AS TIME) AS DECIMAL(20,6));
CAST(CAST('10:11:12.098700' AS TIME) AS DECIMAL(20,6))
``` 	
When the above statements are used, the ways to process them are different in MySQL 5.5/5.6 and MySQL 5.7/MariaDB 10.1:
- In MySQL 5.5/5.6, 101112.098700 will be returned and the precision will still be retained.
- In MySQL 5.7 and MariaDB 10.1, 101112.000000 will be returned. This is because the statement does not specify a precision for `TIME` and the default precision of `TIME` is 0; therefore, the values after the decimal point of `CAST('10:11:12.098700' AS TIME)` will be lost.

You can use the following statement to keep the time precision.
```
SELECT CAST(CAST('10:11:12.098700' (6)) AS DECIMAL(20,6));
+-----------------------------------------------------------+
| CAST(CAST('10:11:12.098700' AS TIME(6)) AS DECIMAL(20,6)) |
+-----------------------------------------------------------+
| 101112.098700 |
+-----------------------------------------------------------+
```
>The default precision of `TIME` is not consistent. If time precision is required, you should specify a precision of time for upgrade or migration.

```
CREATE TABLE t1(f1 TIME);
INSERT INTO t1 VALUES ('23:38:57');
SELECT TIMESTAMP(f1,'1') FROM t1;
```
In MySQL 5.5/5.6, `NULL` will be returned; in MariaDB 10.1 and MySQL 5.7, `2016-08-03 23:38:58` will be returned.
- If the first parameter of `TIMESTAMP()` is in time type, the returned value will be `NULL` as MySQL 5.5 cannot automatically convert it to timestamp type.
- In MySQL 5.7 and TencentDB for MariaDB, values in time type will be automatically converted to timestamp type, i.e., current date + entered time variable.

### 5. Appendix: TencentDB for MariaDB parameters and MySQL parameters

#### 5.1. Different parameters with the same variable name
Parameters with the same variable name have the same main feature.

<table>

<tr>
<th width="20%">Parameter Name</th>
<th width="30%">MariaDB 10.1</th>
<th width="30%">MySQL 5.6</th>
</tr>

<tr>
<td>old_passwords</td>
<td>OFF</td>
<td>0</td>
</tr>

<tr>
<td>tmpdir</td>
<td>/tmp/5cXm2hHsWi/mysqld.1</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/tmp/mysqld.1</td>
</tr>

<tr>
<td>version</td>
<td>10.1.9-MariaDB-log</td>
<td>5.6.31-log</td>
</tr>

<tr>
<td>slow_query_log_file</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/build_dongzhi/mysql-test/var/mysqld.1/mysqld-slow.log</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/mysqld.1/mysqld-slow.log</td>
</tr>

<tr>
<td>table_definition_cache</td>
<td>400</td>
<td>1400</td>
</tr>

<tr>
<td>datadir</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/build_dongzhi/mysql-test/var/mysqld.1/data/</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/mysqld.1/data/</td>
</tr>

<tr>
<td>pid_file</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/build_dongzhi/mysql-test/var/run/mysqld.1.pid</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/run/mysqld.1.pid</td>
</tr>

<tr>
<td>max_seeks_for_key</td>
<td>4294967295</td>
<td>18446744073709500000</td>
</tr>

<tr>
<td>slave_load_tmpdir</td>
<td>/tmp/5cXm2hHsWi/mysqld.1</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/tmp/mysqld.1</td>
</tr>

<tr>
<td>secure_file_priv</td>
<td>	/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/build_dongzhi/mysql-test/var/</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/</td>
</tr>

<tr>
<td>sql_mode</td>
<td>NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION	</td>
<td>NO_ENGINE_SUBSTITUTION</td>
</tr>

<tr>
<td>ssl_cert</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/mysql-test/std_data/server-cert.pem</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/mysql-test/std_data/server-cert.pem</td>
</tr>

<tr>
<td>ssl_ca</td>
<td>	/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/mysql-test/std_data/cacert.pem</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/mysql-test/std_data/cacert.pem</td>
</tr>

<tr>
<td>open_files_limit</td>
<td>1024</td>
<td>4161</td>
</tr>

<tr>
<td>binlog_checksum</td>
<td>NONE</td>
<td>CRC32</td>
</tr>

<tr>
<td>basedir</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6</td>
</tr>

<tr>
<td>query_alloc_block_size</td>
<td>16384</td>
<td>8192</td>
</tr>

<tr>
<td>innodb_max_dirty_pages_pct</td>
<td>75.000000</td>
<td>75</td>
</tr>

<tr>
<td>ssl_key</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/mysql-test/std_data/server-key.pem</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/mysql-test/std_data/server-key.pem</td>
</tr>

<tr>
<td>myisam_sort_buffer_size</td>
<td>134216704</td>
<td>8388608</td>
</tr>

<tr>
<td>skip_name_resolve</td>
<td>ON</td>
<td>OFF</td>
</tr>

<tr>
<td>pseudo_thread_id</td>
<td>3</td>
<td>2</td>
</tr>

<tr>
<td>character_sets_dir</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/sql/share/charsets/</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/sql/share/charsets/</td>
</tr>

<tr>
<td>innodb_adaptive_flushing_lwm</td>
<td>10</td>
<td>10</td>
</tr>

<tr>
<td>myisam_recover_options</td>
<td>DEFAULT</td>
<td>OFF</td>
</tr>

<tr>
<td>performance_schema_max_statement_classes</td>
<td>179</td>
<td>168</td>
</tr>

<tr>
<td>innodb_version</td>
<td>5.6.26-74.0</td>
<td>5.6.31</td>
</tr>

<tr>
<td>max_write_lock_count</td>
<td>4294967295</td>
<td>18446744073709500000</td>
</tr>

<tr>
<td>thread_cache_size</td>
<td>0</td>
<td>9</td>
</tr>

<tr>
<td>innodb_checksum_algorithm</td>
<td>INNODB</td>
<td>innodb</td>
</tr>

<tr>
<td>optimizer_switch</td>
<td>
index_merge=on,<br>index_merge_union=on,<br>index_merge_sort_union=on,<br>index_merge_intersection=on,<br>index_merge_sort_intersection=off,<br>engine_condition_pushdown=off,<br>index_condition_pushdown=on,<br>derived_merge=on,<br>derived_with_keys=on,<br>firstmatch=on,<br>loosescan=on,<br>materialization=on,<br>in_to_exists=on,<br>semijoin=on,<br>partial_match_rowid_merge=on,<br>partial_match_table_scan=on,<br>subquery_cache=on,<br>mrr=off,<br>mrr_cost_based=off,<br>mrr_sort_keys=off,<br>outer_join_with_cache=on,<br>semijoin_with_cache=on,<br>join_cache_incremental=on,<br>join_cache_hashed=on,<br>join_cache_bka=on,<br>optimize_join_buffer_size=off,<br>table_elimination=on,<br>extended_keys=on,<br>exists_to_in=on
</td>
<td>
index_merge=on,<br>index_merge_union=on,<br>index_merge_sort_union=on,<br>index_merge_intersection=on,<br>engine_condition_pushdown=on,<br>index_condition_pushdown=on,<br>mrr=on,<br>mrr_cost_based=on,<br>block_nested_loop=on,<br>batched_key_access=off,<br>materialization=on,<br>semijoin=on,<br>loosescan=on,<br>firstmatch=on,<br>subquery_materialization_cost_based=on,<br>use_index_extensions=on
</td>
</tr>

<tr>
<td>timestamp</td>
<td>1471938276</td>
<td>1471937901</td>
</tr>

<tr>
<td>general_log_file</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/build_dongzhi/mysql-test/var/mysqld.1/mysqld.log</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/mysqld.1/mysqld.log</td>
</tr>

<tr>
<td>myisam_stats_method</td>
<td>NULLS_UNEQUAL</td>
<td>nulls_unequal</td>
</tr>

<tr>
<td>innodb_log_compressed_pages</td>
<td>OFF</td>
<td>ON</td>
</tr>

<tr>
<td>query_prealloc_size</td>
<td>24576</td>
<td>0</td>
</tr>

<tr>
<td>rand_seed2</td>
<td>297895171</td>
<td>0</td>
</tr>

<tr>
<td>rand_seed1</td>
<td>605568929</td>
<td>0</td>
</tr>

<tr>
<td>socket</td>
<td>/tmp/5cXm2hHsWi/mysqld.1.sock</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/mysql-test/var/tmp/mysqld.1.sock</td>
</tr>

<tr>
<td>innodb_max_dirty_pages_pct_lwm</td>
<td>0.001</td>
<td>0</td>
</tr>

<tr>
<td>lc_messages_dir</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/build_dongzhi/sql/share/</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/build_dongzhi/sql/share/</td>
</tr>

<tr>
<td>max_relay_log_size</td>
<td>1073741824</td>
<td>0</td>
</tr>

<tr>
<td>plugin_dir</td>
<td>/data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/lib/plugin/</td>
<td>/data/home/tdengine/dongzhi/src/mysql-server-5.6/lib/plugin/</td>
</tr>

<tr>
<td>thread_stack</td>
<td>294912</td>
<td>262144</td>
</tr>

</table>


#### 5.2. Variables unique to TencentDB for MariaDB

- aria_block_size     8192
- aria_checkpoint_interval     30
- aria_checkpoint_log_activity     1048576
- aria_encrypt_tables     OFF
- aria_force_start_after_recovery_failures     0
- aria_group_commit     none
- aria_group_commit_interval     0
- aria_log_file_size     1073741824
- aria_log_purge_type     immediate
- aria_max_sort_file_size     9223372036853727232
- aria_page_checksum     ON
- aria_pagecache_age_threshold     300
- aria_pagecache_buffer_size     134217728
- aria_pagecache_division_limit     100
- aria_pagecache_file_hash_size     512
- aria_recover     NORMAL
- aria_repair_threads     1
- aria_sort_buffer_size     268434432
- aria_stats_method     nulls_unequal
- aria_sync_log_dir     NEWFILE
- aria_used_for_temp_tables     ON
- autoremoverelaylog     ON
- binlog_annotate_row_events     OFF
- binlog_commit_wait_count     0
- binlog_commit_wait_usec     100000
- binlog_optimize_thread_scheduling     ON
- deadlock_search_depth_long     15
- deadlock_search_depth_short     4
- deadlock_timeout_long     50000000
- deadlock_timeout_short     10000
- debug_no_thread_alarm     OFF
- default_master_connection      
- default_regex_flags      
- encrypt_binlog     OFF
- encrypt_tmp_disk_tables     OFF
- encrypt_tmp_files     OFF
- enforce_storage_engine      
- expensive_subquery_limit     100
- extra_max_connections     20
- extra_port     0
- flush_relay_logs_for_strong_consistency     ON
- gtid_binlog_pos      
- gtid_binlog_state      
- gtid_current_pos      
- gtid_domain_id     0
- gtid_ignore_duplicates     OFF
- gtid_seq_no     0
- gtid_slave_pos      
- gtid_strict_mode     OFF
- histogram_size     0
- histogram_type     SINGLE_PREC_HB
- in_transaction     0
- innodb_adaptive_hash_index_partitions     1
- innodb_background_scrub_data_check_interval     3600
- innodb_background_scrub_data_compressed     OFF
- innodb_background_scrub_data_interval     604800
- innodb_background_scrub_data_uncompressed     OFF
- innodb_buf_dump_status_frequency     0
- innodb_buffer_pool_populate     OFF
- innodb_cleaner_lsn_age_factor     HIGH_CHECKPOINT
- innodb_compression_algorithm     none
- innodb_corrupt_table_action     assert
- innodb_default_encryption_key_id     1
- innodb_defragment     OFF
- innodb_defragment_fill_factor     0.900000
- innodb_defragment_fill_factor_n_recs     20
- innodb_defragment_frequency     40
- innodb_defragment_n_pages     7
- innodb_defragment_stats_accuracy     0
- innodb_disallow_writes     OFF
- innodb_empty_free_list_algorithm     BACKOFF
- innodb_encrypt_log     OFF
- innodb_encrypt_tables     OFF
- innodb_encryption_rotate_key_age     1
- innodb_encryption_rotation_iops     100
- innodb_encryption_threads     0
- innodb_fake_changes     OFF
- innodb_fatal_semaphore_wait_threshold     600
- innodb_force_primary_key     OFF
- innodb_foreground_preflush     EXPONENTIAL_BACKOFF
- innodb_idle_flush_pct     100
- innodb_immediate_scrub_data_uncompressed     OFF
- innodb_instrument_semaphores     OFF
- innodb_kill_idle_transaction     0
- innodb_locking_fake_changes     ON
- innodb_log_arch_dir     ./
- innodb_log_arch_expire_sec     0
- innodb_log_archive     OFF
- innodb_log_block_size     512
- innodb_log_checksum_algorithm     INNODB
- innodb_max_bitmap_file_size     104857600
- innodb_max_changed_pages     1000000
- innodb_mtflush_threads     8
- innodb_prefix_index_cluster_optimization     OFF
- innodb_sched_priority_cleaner     19
- innodb_scrub_log     OFF
- innodb_scrub_log_speed     256
- innodb_show_locks_held     10
- innodb_show_verbose_locks     0
- innodb_simulate_comp_failures     0
- innodb_stats_modified_counter     0
- innodb_stats_traditional     ON
- innodb_track_changed_pages     OFF
- innodb_use_atomic_writes     OFF
- innodb_use_fallocate     OFF
- innodb_use_global_flush_log_at_trx_commit     ON
- innodb_use_mtflush     OFF
- innodb_use_stacktrace     OFF
- innodb_use_trim     OFF
- join_buffer_space_limit     2097152
- join_cache_level     2
- key_cache_file_hash_size     512
- key_cache_segments     0
- last_gtid      
- log_slow_filter     admin,filesort,filesort_on_disk,full_join,full_scan,query_cache,query_cache_miss,tmp_table,tmp_table_on_disk
- log_slow_rate_limit     1
- log_slow_verbosity      
- log_tc_size     24576
- loglevel     3
- max_long_data_size     4194304
- max_statement_time     0.000000
- mrr_buffer_size     262144
- myisam_block_size     1024
- mysql56_temporal_format     ON
- old_mode      
- optimizer_selectivity_sampling_limit     100
- optimizer_use_condition_selectivity     1
- plugin_maturity     unknown
- progress_report_time     5
- query_cache_strip_comments     OFF
- relay_log_sync_threshold     134217728
- relay_log_sync_timeout     200
- relay_log_sync_txn_count     5
- replicate_annotate_row_events     OFF
- replicate_do_db      
- replicate_do_table      
- replicate_events_marked_for_skip     REPLICATE
- replicate_ignore_db      
- replicate_ignore_table      
- replicate_wild_do_table      
- replicate_wild_ignore_table      
- rowid_merge_buff_size     8388608
- rpl_semi_sync_master_enabled     OFF
- rpl_semi_sync_master_timeout     10000
- rpl_semi_sync_master_trace_level     32
- rpl_semi_sync_master_wait_no_slave     ON
- rpl_semi_sync_master_wait_point     AFTER_COMMIT
- rpl_semi_sync_slave_enabled     OFF
- rpl_semi_sync_slave_trace_level     32
- skip_parallel_replication     OFF
- skip_replication     OFF
- slave_current_parallel_transactions     0
- slave_ddl_exec_mode     IDEMPOTENT
- slave_domain_parallel_threads     0
- slave_max_parallel_transactions     0
- slave_parallel_max_queued     131072
- slave_parallel_mode     conservative
- slave_parallel_threads     0
- slave_run_triggers_for_rbr     NO
- sqlasyn     OFF
- sqlasyntimeout     10
- sqlasynwarntimeout     3
- strict_password_validation     ON
- thread_pool_high_prio_mode     transactions
- thread_pool_high_prio_tickets     4294967295
- thread_pool_idle_timeout     60
- thread_pool_max_threads     1000
- thread_pool_oversubscribe     3
- thread_pool_oversubscribe_parall     1
- thread_pool_size     8
- thread_pool_stall_limit     500
- use_stat_tables     NEVER
- userstat     OFF
- version_malloc_library     system
- version_ssl_library     OpenSSL 1.0.2d 9 Jul 2015
- wsrep_auto_increment_control     ON
- wsrep_causal_reads     OFF
- wsrep_certify_nonpk     ON
- wsrep_cluster_address      
- wsrep_cluster_name     my_wsrep_cluster
- wsrep_convert_lock_to_trx     OFF
- wsrep_data_home_dir     /data/home/tdengine/dongzhi/src/tdsql-mariadb-10.1.9-release1/build_dongzhi/mysql-test/var/mysqld.1/data/
- wsrep_dbug_option      
- wsrep_debug     OFF
- wsrep_desync     OFF
- wsrep_dirty_reads     OFF
- wsrep_drupal_282555_workaround     OFF
- wsrep_forced_binlog_format     NONE
- wsrep_gtid_domain_id     0
- wsrep_gtid_mode     OFF
- wsrep_load_data_splitting     ON
- wsrep_log_conflicts     OFF
- wsrep_max_ws_rows     131072
- wsrep_max_ws_size     1073741824
- wsrep_mysql_replication_bundle     0
- wsrep_node_address      
- wsrep_node_incoming_address     AUTO
- wsrep_node_name      
- wsrep_notify_cmd      
- wsrep_on     OFF
- wsrep_osu_method     TOI
- wsrep_patch_version     wsrep_25.11
- wsrep_provider     none
- wsrep_provider_options      
- wsrep_recover     OFF
- wsrep_replicate_myisam     OFF
- wsrep_restart_slave     OFF
- wsrep_retry_autocommit     1
- wsrep_slave_fk_checks     ON
- wsrep_slave_threads     1
- wsrep_slave_uk_checks     OFF
- wsrep_sst_auth      
- wsrep_sst_donor      
- wsrep_sst_donor_rejects_queries     OFF
- wsrep_sst_method     rsync
- wsrep_sst_receive_address     AUTO
- wsrep_start_position     00000000-0000-0000-0000-000000000000:-1
- wsrep_sync_wait     0

#### 5.3. Variables unique to MySQL 5.6

- avoid_temporal_upgrade     OFF
- bind_address     *
- binlog_error_action     IGNORE_ERROR
- binlog_gtid_simple_recovery     OFF
- binlog_max_flush_queue_time     0
- binlog_order_commits     ON
- binlog_rows_query_log_events     OFF
- binlogging_impossible_mode     IGNORE_ERROR
- block_encryption_mode     aes-128-ecb
- core_file     ON
- disconnect_on_expired_password     ON
- end_markers_in_json     OFF
- enforce_gtid_consistency     OFF
- eq_range_index_dive_limit     1
- gtid_executed      
- gtid_mode     OFF
- gtid_next     AUTOMATIC
- gtid_owned      
- gtid_purged      
- innodb_tmpdir      
- log_bin_use_v1_row_events     OFF
- log_slow_admin_statements     OFF
- log_slow_slave_statements     OFF
- log_throttle_queries_not_using_indexes     0
- master_info_repository     FILE
- new     OFF
- optimizer_trace     enabled=off,one_line=off
- optimizer_trace_features     greedy_search=on,range_optimizer=on,dynamic_range=on,repeated_subselect=on
- optimizer_trace_limit     1
- optimizer_trace_max_mem_size     16384
- optimizer_trace_offset     -1
- relay_log_info_repository     FILE
- rpl_stop_slave_timeout     31536000
- server_id_bits     32
- server_uuid     9078a55d-6904-11e6-bfa9-ecf4bbcdc829
- sha256_password_private_key_path     private_key.pem
- sha256_password_public_key_path     public_key.pem
- show_old_temporals     OFF
- simplified_binlog_gtid_recovery     OFF
- slave_allow_batching     OFF
- slave_checkpoint_group     512
- slave_checkpoint_period     300
- slave_parallel_workers     0
- slave_pending_jobs_size_max     16777216
- slave_rows_search_algorithms     TABLE_SCAN,INDEX_SCAN
- table_open_cache_instances     1
- transaction_allow_batching     OFF

