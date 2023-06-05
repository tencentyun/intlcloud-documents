This document describes FAQs about the quick migration.
## FAQs
#### 1. Will TDSQL-C for MySQL support the advanced feature parameters of TencentDB for MySQL after the quick migration?
No. TDSQL-C for MySQL will be compatible with those monitoring items gradually. For more information on parameters of TDSQL-C for MySQL, see the following table:

<dx-tabs>
::: TencentDB for MySQL 5.7
| TencentDB for MySQL Parameter Name | TencentDB for MySQL Parameter Value | Supported by TDSQL-C for MySQL |
|---------|---------|---------|
| cdb_recycle_bin_enabled | OFF | No |
| information_schema_stats_expiry | 86400 | No |
| binlog_row_event_max_size | 8192 | No |
| innodb_backquery_history_limit | 8000000 | No |
| innodb_ddl_threads | 4 | No |
| innodb_parallel_ddl | OFF | No |
| innodb_adaptive_hash_index | OFF | No |
| cdb_plan_cache | OFF | No | 
| innodb_table_drop_mode | sync_drop | No |
| cdb_recycle_bin_retention | 604800 | No |
| slave_net_timeout | 120 | No |
| innodb_backquery_enable | OFF | No |
| innodb_fast_ddl | OFF | No |
| max_length_for_sort_data | 1024 | No |
| slave_parallel_type | LOGICAL_CLOCK | No |
| cdb_optimize_large_trans_binlog | OFF | No |
| innodb_fast_ahi_cleanup_for_drop_table | OFF | No |
| txsql_parallel_exchange_buffer_size | 1048576 | No |
| innodb_temp_data_file_path | ibtmp1:12M:autoextend | No |
| slave_rows_search_algorithms | TABLE_SCAN,INDEX_SCAN,HASH_SCAN | No |
| cdb_recycle_scheduler_interval | 0 | No |
| innodb_ddl_buffer_size | 10485760 | No |
| cdb_kill_idle_trans_timeout | 0 | No |
| collation_server | utf8_tolower_ci | Yes |
| delay_key_write | ON | No |
| innodb_async_truncate_size | 128 | No |
| cdb_more_gtid_feature_supported | OFF | No |
| cdb_opt_outline_enabled | OFF | No |
| innodb_txsql_parallel_partitions_per_worker | 13 | No |
| cdb_kill_user_extra | root@% | No |
| slave_parallel_workers | 0 | No |
| innodb_backquery_window | 900 | No |
:::
::: TencentDB for MySQL 8.0
| TencentDB for MySQL Parameter Name | TencentDB for MySQL Parameter Value | Supported by TDSQL-C for MySQL |
|---------|---------|---------|
| cdb_recycle_bin_enabled | OFF | No |
| information_schema_stats_expiry | 86400 | No |
| binlog_row_event_max_size | 8192 | No |
| innodb_backquery_history_limit | 8000000 | No |
| innodb_ddl_threads | 4 | No |
| innodb_parallel_ddl | OFF | No |
| innodb_adaptive_hash_index | OFF | No |
| cdb_plan_cache | OFF | No | 
| innodb_table_drop_mode | sync_drop | No |
| cdb_recycle_bin_retention | 604800 | No |
| slave_net_timeout | 120 | No |
| innodb_backquery_enable | OFF | No |
| innodb_fast_ddl | OFF | No |
| max_length_for_sort_data | 1024 | No |
| slave_parallel_type | LOGICAL_CLOCK | No |
| cdb_optimize_large_trans_binlog | OFF | No |
| innodb_fast_ahi_cleanup_for_drop_table | OFF | No |
| txsql_parallel_exchange_buffer_size | 1048576 | No |
| innodb_temp_data_file_path | ibtmp1:12M:autoextend | No |
| slave_rows_search_algorithms | TABLE_SCAN,INDEX_SCAN,HASH_SCAN | No |
| cdb_recycle_scheduler_interval | 0 | No |
| innodb_ddl_buffer_size | 10485760 | No |
| cdb_kill_idle_trans_timeout | 0 | No |
| collation_server | utf8_tolower_ci | Yes |
| delay_key_write | ON | No |
| innodb_async_truncate_size | 128 | No |
| cdb_more_gtid_feature_supported | OFF | No |
| cdb_opt_outline_enabled | OFF | No |
| innodb_txsql_parallel_partitions_per_worker | 13 | No |
| cdb_kill_user_extra | root@% | No |
| slave_parallel_workers | 0 | No |
| innodb_backquery_window | 900 | No |
:::
</dx-tabs>


#### 2. Will TDSQL-C for MySQL support the IOPS monitoring items of TencentDB for MySQL after the quick migration?
No. TDSQL-C for MySQL will be compatible with those monitoring items gradually.