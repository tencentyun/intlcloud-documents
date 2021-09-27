
TencentDB for MySQL provides system parameter templates for batch parameter settings. The parameters in system parameter templates may be optimized and updated with MySQL iteration. This document describes the update history of the parameters in system parameter templates.
>?
>- The changes of the parameters in a system parameter template do not affect the database instances that already applied the template. If you need to apply new parameters to a batch of instances, you can import the updated template when setting parameters in batches.
>- For directions on how to use system parameter templates, see [Managing Parameter Templates](https://intl.cloud.tencent.com/document/product/236/31906).

## MySQL 8.0
### November 2020

| Parameter Name                       | Update Category   | Parameter Description                                                     |
| ------------------------------ | ---------- | ------------------------------------------------------------ |
| innodb_flush_log_at_trx_commit  | New parameter supported         | Determines InnoDB transaction durability                  |
| sync_binlog                     | New parameter supported         | Controls how often the MySQL server synchronizes the binary log to disk           |
| local_infile                    | New parameter supported         | Controls whether LOCAL is supported for LOAD DATA INFILE |
| innodb_log_file_size            | New parameter supported         | The size in bytes of each log file in a log group         |
| cdb_recycle_bin_enabled        | New parameter supported       | Controls whether the deleted table is placed in the recycle bin |
| binlog_format                  | Value range updated | New value range: [row]                                      |
| innodb_autoinc_lock_mode       | Default value updated | New default value: 2                                          |
| table_open_cache               | Default value updated | New default value: 2000                                          |
| slave_pending_jobs_size_max    | Default value updated | New default value: 1073741824                                          |
| time_zone                      | Value range updated | New value range: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections                | Value range updated | New value range: [1-100000]                                 |
| slave_rows_search_algorithms   | Default value updated | New default value: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files              | Default value updated | New default value: 10240                                      |
| slave_parallel_type            | Value range updated | New value range: [LOGICAL_CLOCK\|TABLE\|DATABASE]           |


## MySQL 5.7
### August 2020

| Parameter Name                       | Update Category   | Parameter Description                                                     |
| ------------------------------- | ------------ | --------------------------------------------------------- |
| log_warnings                    | New parameter supported         | Controls whether to produce additional warning messages   |
| innodb_flush_log_at_trx_commit  | New parameter supported         | Determines InnoDB transaction durability                  |
| sync_binlog                     | New parameter supported         | Controls how often the MySQL server synchronizes the binary log to disk           |
| local_infile                    | New parameter supported         | Controls whether LOCAL is supported for LOAD DATA INFILE |
| innodb_log_file_size            | New parameter supported         | The size in bytes of each log file in a log group         |
| binlog_format                  | Value range updated | New value range: [row]                                      |
| innodb_autoinc_lock_mode       | Default value updated | New default value: 2                                          |
| innodb_open_files               | Value range updated   |   New value range: [1 - 102400]                |
| table_open_cache               | Default value updated | New default value: 2000                                          |
| slave_pending_jobs_size_max     | Default value updated   |   New default value: 1GB   |
| time_zone                       | Value range updated   |  New value range: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]       |
| max_connections                | Value range updated | New value range: [1-100000]                                 |
| cdb_more_gtid_feature_supported | All kernel features supported (including the parameter) | -          |
| slave_parallel_works                    | All kernel features supported (including the parameter) |    -                                                       |
| tls_version                     | Parameter deprecated     |     -                                                      |
| slave_rows_search_algorithms   | Default value updated | New default value: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files              | Default value updated | New default value: 10240                                      |

## MySQL 5.6
### August 2020

| Parameter Name                       | Update Category   | Parameter Description                                                     |
| ------------------------------- | ---------- | --------------------------------------------------------- |
| log_warnings                    | New parameter supported         | Controls whether to produce additional warning messages   |
| innodb_flush_log_at_trx_commit  | New parameter supported         | Determines InnoDB transaction durability                  |
| sync_binlog                     | New parameter supported         | Controls how often the MySQL server synchronizes the binary log to disk           |
| local_infile                    | New parameter supported         | Controls whether LOCAL is supported for LOAD DATA INFILE |
| innodb_log_file_size            | New parameter supported         | The size in bytes of each log file in a log group         |
| binlog_format                  | Value range updated | New value range: [row]                                      |
| innodb_autoinc_lock_mode       | Default value updated | New default value: 2                                          |
| innodb_open_files               | Value range updated   |   New value range: [1 - 102400]                |
| table_open_cache               | Default value updated | New default value: 2000                                          |
| slave_pending_jobs_size_max     | Default value updated |  New default value: 1GB     |
| time_zone                       | Value range updated |   New value range: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]      |
| max_connections                | Value range updated | New value range: [1-100000]                                 |
| cdb_more_gtid_feature_supported | Default value updated |  New default value: on    |
| slave_rows_search_algorithms   | Default value updated | New default value: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files              | Default value updated | New default value: 10240                                      |


## MySQL 5.5
### August 2020

| Parameter Name                       | Update Category   | Parameter Description                                                     |
| ------------------------ | ---------- | -------- |
| innodb_autoinc_lock_mode   | Default value updated | New default value: TABLE_SCAN,INDEX_SCAN,HASH_SCAN            |
| innodb_open_files        | Default value updated |  New default value: 10240        |
