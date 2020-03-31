## Parameter Template Overview
You can use parameters in a parameter template to manage configuration of a database engine. A database parameter set is just like a container of engine configuration values which can be applied to one or more database instances.
  
If you have already created a database parameter template and want to include most of its custom parameters and values in the new template, simply copy the parameter template.

If you want to use your own database parameter template, you only need to create it, modify the desired parameters, and configure your database instance to use it. It should be noted that all database instances that have applied a parameter template will not get all parameter updates of the template. If you want to apply new parameters to a batch of database instances, you can apply them by importing a template during batch parameter settings.

## Managing Parameter Templates
A parameter template supports the following features, you can log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql) and select an instance to enter its management page and configure the template features:
- Specify the default parameter template.
- Create templates by modifying the default parameters to generate custom parameter optimization schemes.
- Generate templates by importing parameters from configuration file `my.conf`.
- Save parameter settings as templates.
- Import parameters from templates when setting parameters for one or multiple instances.
![](https://main.qcloudimg.com/raw/e70f5f40e72ddeed2830d9f14702a98a.png)

## Parameter Description
- Parameters are initialized by default when an instance is created.
- You can modify instance parameters through entries such as parameter template and parameter configuration.
- Parameters of different instances are isolated from and will not affect one another.
- To avoid faulty operations, only common parameters can be set. If you need other parameters, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application and specify the "instance ID and parameter names to be added".

| Parameter Name | Restart Required (0: No; 1: Yes) | Default Value | Current Value (Configurable) | Valid Values |
|:--:|:--:|:--:|:--:|:--:|
|auto_increment_increment|0|1|1|[1-65535]|
|auto_increment_offset|0|1|1|[1-65535]|
|autocommit|0|ON|ON|[ON, OFF]|
|character_set_server|0|utf8|utf8|[utf8, latin1, gbk, utf8mb4]|
|connect_timeout|0|10|10|[1-3600]|
|default_week_format|0|0|0|[0-7]|
|delay_key_write|0|ON|ON|[ON, OFF, ALL]|
|delayed_insert_limit|0|100|100|[1-4294967295]|
|delayed_insert_timeout|0|300|300|[1-3600]|
|delayed_queue_size|0|1000|1000|[1-4294967295]|
|div_precision_increment|0|4|4|[0-30]|
|group_concat_max_len|0|1024|1024|[4-18446744073709547520]|
|innodb_concurrency_tickets|0|5000|5000|[100-10000]|
|innodb_large_prefix|0|OFF|OFF|[OFF, ON]|
|innodb_lock_wait_timeout|0|50|50|[1-1073741824]|
|innodb_max_dirty_pages_pct|0|10|70|[10-90]|
|innodb_old_blocks_pct|0|37|37|[5-95]|
|innodb_old_blocks_time|0|1000|1000|[0-1000]|
|innodb_purge_batch_size|0|300|300|[1-1024]|
|innodb_read_ahead_threshold|0|56|56|[0-64]|
|innodb_stats_method|0|nulls_equal|nulls_equal|[nulls_equal, nulls_unequal, nulls_ignored]|
|innodb_stats_on_metadata|0|OFF|OFF|[ON, OFF]|
|innodb_stats_sample_pages|0|8|8|[1-4294967296]|
|innodb_strict_mode|0|OFF|OFF|[ON, OFF]|
|innodb_table_locks|0|ON|ON|[ON, OFF]|
|innodb_thread_concurrency|0|0|0|[0-128]|
|innodb_thread_sleep_delay|0|10000|10000|[1-3600000]|
|interactive_timeout|0|28800|28800|[10-86400]|
|key_cache_age_threshold|0|300|300|[100-4294967295]|
|key_cache_block_size|0|1024|1024|[512-16384]|
|key_cache_division_limit|0|100|100|[1-100]|
|lock_wait_timeout|0|5|5|[1-31536000]|
|log_queries_not_using_indexes|0|OFF|OFF|[ON, OFF]|
|long_query_time|0|1.000000|1.000000|[0.5-10]|
|low_priority_updates|0|OFF|OFF|[OFF, ON]|
|max_allowed_packet|0|134217728|1073741824|[16384-1073741824]|
|max_connect_errors|0|2000|2000|[1-4096]|
|max_connections|0|4096|4096|[1-32768]|
|myisam_sort_buffer_size|0|4194304|4194304|[262144-16777216]|
|net_buffer_length|0|16384|16384|[4096, 8192, 16384, 32768, 65536, 1048576]|
|net_read_timeout|0|30|30|[1-3153600]|
|net_retry_count|0|10|10|[1-4294967295]|
|net_write_timeout|0|60|60|[1-3153600]|
|query_alloc_block_size|0|8192|8192|[1024-16384]|
|query_cache_limit|0|1048576|1048576|[1-1048576]|
|query_cache_size|0|0|0|[0-104857600]|
|query_cache_type|0|OFF|OFF|[OFF, ON, DEMAND]|
|query_prealloc_size|0|8192|8192|[8192-1048576]|
|slow_launch_time|0|2|2|[1-1024]|
|sort_buffer_size|0|2097152|2097152|[32768-1073741824]|
|sqlasyn|0|ON|ON|[ON, OFF]|
|sqlasyntimeout|0|10|30|[10-100]|
|table_definition_cache|0|400|400|[400-2048]|
|table_open_cache|0|1024|10240|[400-524288]|
|tmp_table_size|0|33554432|33554432|[262144-67108864]|
|tx_isolation|0|REPEATABLE-READ|REPEATABLE-READ|[REPEATABLE-READ, SERIALIZABLE, READ-COMMITTED, READ-UNCOMMITTED]|
|wait_timeout|0|28800|28800|[60-259200]|


## TencentDB for MariaDB System Variable Description
- [Index of Categories](https://mariadb.com/kb/en/mariadb/system-variables)
- [Index of All Variables](https://mariadb.com/kb/en/mariadb/full-list-of-mariadb-options-system-and-status-variables)

