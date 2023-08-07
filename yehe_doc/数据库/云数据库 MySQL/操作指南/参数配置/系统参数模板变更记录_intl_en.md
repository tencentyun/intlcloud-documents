
TencentDB for MySQL provides system parameter templates for batch parameter settings. The parameters in system parameter templates may be optimized and updated with MySQL iteration. This document describes the update history of the parameters in system parameter templates.
>?
>- If the parameters in the template are updated, the instance parameters are not updated unless they are manually re-applied to the instances. You can apply the parameter changes to single or multiple instances by importing a template.
>- For directions on how to use system parameter templates, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).

## January 2023
| Parameter | MySQL 5.7 | MySQL 8.0 | Change Description | 
|---------|---------|---------|---------|
| max_execution_time | &#10003; | &#10003;|  Dynamic setting is supported for `max_execution_time` <br><li>Restart required: No<br><li>Default value: `0`<br><li>Value range: 0–4294967295<br><li>Unit: ms |

## August 2022
| Parameter | MySQL 5.7 | MySQL 8.0 | Change Description | 
|---------|---------|---------|---------|
| innodb_buffer_pool_size | &#10003; | &#10003; | Dynamic setting is supported for `innodb_buffer_pool_size` <br><li> Restart required: No <br><li> Default value: {DBInitMemory * 786432}<br><li> Value range: {DBInitMemory * 524288} - {DBInitMemory * 943718}<br><li> DBinitMemory: An integer of instance memory size |

## July 2022
| Parameter | MySQL 5.7 | MySQL 8.0 | Change Description | 
|---------|---------|---------|---------|
| innodb_temp_data_file_path | &#10003; | &#10003; | Parameter modification is supported for `innodb_temp_data_file_path` (temp tablespace size) and the parameter properties are as follows: <br><li>Restart required: Yes <br><li> Default value: `ibtmp1:12M:autoextend`<br><li>Value range of `ibtmp`: 12 MB - 1024 MB. After you select `autoextend`, the maximum value can be set to 2097152 MB |

## March 2022
| Parameter | MySQL 5.6 | MySQL 5.7 | MySQL 8.0 | Change Description | 
|---------|---------|---------|---------|---------|
| innodb_open_files | &#10003; | &#10003; | &#10003; | Removed |
| innodb_stats_sample_pages | - | &#10003; | &#10003; | Removed |
| wait_timeout | &#10003; | &#10003; | &#10003; | New value range: 1–31536000 |
| thread_cache_size | &#10003; | &#10003; | &#10003; | New value range: 1–16384 |

## December 2021
| Parameter | MySQL 5.6 | MySQL 5.7 | MySQL 8.0 | Change Description | 
|---------|---------|---------|---------|---------|
| binlog_row_image | &#10003; | &#10003 | &#10003; | Default value: `FULL`. For the early created instances, the default value is `MINIMAL`. Manual modification is supported. |

## November 2020
| Parameter | MySQL 8.0 | Change Description | 
|---------|---------|---------|
| iinnodb_flush_log_at_trx_commit | &#10003; | Parameter added |
| sync_binlog | &#10003; | Parameter added |
| local_infile  | &#10003; | Parameter added |
| innodb_log_file_size | &#10003; | Parameter added |
| cdb_recycle_bin_enabled | &#10003; | Parameter added |
| binlog_format | &#10003; | New value range: `row` |
| innodb_autoinc_lock_mode | &#10003; | New default value: `2` |
| table_open_cache | &#10003; | New default value: `2000` |
| slave_pending_jobs_size_max | &#10003; | New default value: `1073741824` |
| time_zone | &#10003 | New value range: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections | &#10003 | New value range: 1–100000 |
| slave_rows_search_algorithms | &#10003 | New default value: TABLE_SCAN,INDEX_SCAN,HASH_SCAN |
| innodb_open_files | &#10003 | New default value: `10240` |
| slave_parallel_type | &#10003 | New value range: LOGICAL_CLOCK\|TABLE\|DATABASE |

## August 2020
| Parameter | MySQL 5.6 | MySQL 5.7 | Change Description | 
|---------|---------|---------|---------|
| log_warnings | &#10003; | &#10003; | Parameter added |
| innodb_flush_log_at_trx_commit | &#10003; | &#10003; | Parameter added |
| sync_binlog | &#10003; | &#10003; |Parameter added |
| local_infile | &#10003; | &#10003; | Parameter added |
| innodb_log_file_size | &#10003; | &#10003; | Parameter added |
| binlog_format | &#10003; | &#10003; | New range value: `row` |
| innodb_autoinc_lock_mode | &#10003; | &#10003; | New default value: `2` |
| innodb_open_files | &#10003; | &#10003; | New value range: 1–102400 |
| table_open_cache | &#10003; | &#10003; | New default value: `2000` |
| slave_pending_jobs_size_max | &#10003; | &#10003; | New default value: 1 GB |
| time_zone | &#10003; | &#10003; | New value range: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections | &#10003; | &#10003; | New value range: 1–100000 |
| cdb_more_gtid_feature_supported | - | &#10003; | All kernel features supported |
| cdb_more_gtid_feature_supported | &#10003 | - | New default value: `off` |
| slave_parallel_workers | - | &#10003; | All kernel features supported |
| tls_version | - | &#10003; | Removed |
| slave_rows_search_algorithms | &#10003;| &#10003; | New default value: TABLE_SCAN,INDEX_SCAN,HASH_SCAN |
| innodb_open_files | &#10003; | &#10003| New default value: `10240` |

## August 2020
| Parameter |  MySQL 5.5 | Change Description | 
|---------|---------|---------|
| innodb_autoinc_lock_mode | &#10003 | New default value: TABLE_SCAN,INDEX_SCAN,HASH_SCAN |
| innodb_open_files | &#10003 | New default value: `10240` |

