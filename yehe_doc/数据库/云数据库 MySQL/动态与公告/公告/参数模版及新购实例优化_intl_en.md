
Starting from November 22, 2021, TencentDB for MySQL will optimize parameter-related features and instance delivery process, including creating and applying parameter templates, comparing parameters, modifying modifiable parameters, and purchasing instances.

>?If you want to try out the optimized parameter capabilities and delivery process in advance, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for beta test eligibility after September 27, 2021.
Parameter capabilities are applicable only to two-node and three-node TencentDB for MySQL 5.6, 5.7, and 8.0.

## Instance Purchase Process Optimization
Compared with the original instance purchase process, the initialization step is canceled, and you can select the character set, configure the table name case sensitivity, and enter the databases access port and root password on the instance purchase page.

For more information, see [Creating TencentDB for MySQL Instance (New)](https://cloud.tencent.com/document/product/236/61667).

## Parameter Optimization
### Parameter application
Certain parameters can be defined in a formula to change along with the specification, ensuring that the database always runs with the optimal configuration.
Expression syntax is supported as follows:

| Supported Type | Description | Sample |
| ------ | ------------------------------------------------------------ | --------------------- |
| Variable   | <li>DBinitMemory: memory size of instance specification, which is an integer. For example, if the memory size of the instance specification is 4,000 MB, the value of `DBinitMemory` will be 4000.<li>DBInitCpu: number of CPU cores of instance specification, which is an integer. Note: the value of the `innodb_buffer_pool_size` parameter in TencentDB for MySQL must be between 50% and 90% of the memory size. If the configured value is above 90% or below 50%, it will be automatically configured to 90% or 50% respectively. | {DBinitMemory*786432} |
| Operator | Formula syntax: it should be enclosed in braces ({}).  <li>Division operator (/): it divides the dividend by the divisor and returns an integer quotient. If the calculation result is a decimal number, only the integer part will be retained. Decimal numbers are not supported; for example, `{MIN(DBInitMemory/4+500,1000000)}` instead of `{MIN(DBInitMemory\*0.25+500,1000000)}` is supported.<li>Multiplication operator (*): it multiplies two numbers and returns an integer product. If the calculation result is a decimal number, only the integer part will be retained. Decimal number calculation is not supported. |  -                     |
| Function   | <li>MAX(): it returns the greatest value in an integer or parameter formula list. <li>MIN(): it returns the smallest value in an integer or parameter formula list.</li> | {MAX(DBInitCpu/2,4)}  |

For detailed parameter settings, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/236/35793).

### Parameter template creation
For parameter template creation, the original one parameter template type is changed to two types (high-performance parameter template and high-stability template), and the default template type option is added.
<img src="https://main.qcloudimg.com/raw/a93abb9d05b05c0018c46d5efa027221.png"  style="zoom:90%;">

Comparison of parameters between template types:

|   Changed Parameter           | Default Template                  | High-Performance Parameter Template       | High-Stability Template              |
| -------------------- | ------------------------- | ------------------------ | -------------------------- |
| innodb_read_io_threads          | 12            | {MAX(DBInitCpu/2,4)}              | {MAX(DBInitCpu/2,4)}             |
| innodb_write_io_threads         | 12            | {MAX(DBInitCpu/2,4)}              | {MAX(DBInitCpu/2,4)}                |
| max_connections       | 800    | {MIN(DBInitMemory/4+500,100000)} | {MIN(DBInitMemory/4+500,100000)} |
| table_definition_cache                 | 768                       | {MAX(DBInitMemory*512/1000,2048)} | {MAX(DBInitMemory*512/1000,2048)} |
| table_open_cache                       | 2000                      | {MAX(DBInitMemory*512/1000,2048)} | {MAX(DBInitMemory*512/1000,2048)} |
| table_open_cache_instances             | 16                        | {MIN(DBInitMemory/1000,16)}       | {MIN(DBInitMemory/1000,16)}       |
| innodb_disable_sort_file_cache         | OFF                       | OFF                               | ON                    |
| innodb_log_compressed_pages            | ON                        | OFF                               | ON                   |
| innodb_print_all_deadlocks             | OFF                       | OFF                               | ON                    |
| sync_binlog                            | 0                         | 1000                              | 1                                 |
| thread_handling                        | one-thread-per-connection | pool-of-threads                   | one-thread-per-connection         |
| innodb_flush_redo_using_fdatasync      | FALSE                     | TRUE                   | FALSE                 |
| innodb_fast_ahi_cleanup_for_drop_table | FALSE                     | TRUE        | FALSE                             |
| innodb_adaptive_hash_index             | FALSE                     | TRUE                   | FALSE                      |
| innodb_table_drop_mode                 | SYNC_DROP                 | ASYNC_DROP             | SYNC_DROP         |
| innodb_flush_log_at_trx_commit         | 2                         | 2                                 | 1                                 |

For more information on template parameters, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).

### New modifiable parameters

| Parameter                                               |  TencentDB for MySQL 5.6  | TencentDB for MySQL 5.7  | TencentDB for MySQL 8.0  |
| ------------------------------------------------ | -------- | ---- | ---- |
| character_set_client                           |     -            |  &#10003;    |  -    |
| default_password_lifetime                   |      -          |  &#10003;    |  &#10003;    |
| innodb_alter_table_default_algorithm   |      -          |  &#10003;    |   -   |
| innodb_async_truncate_size                |      -          |  &#10003;    |  &#10003;    |
| innodb_async_truncate_work_enabled  |     -          | &#10003;     |    -  |
| innodb_buffer_pool_instances              |  &#10003; |  &#10003;   |  &#10003;   |
| innodb_buffer_pool_size                      |  &#10003; |  &#10003;   |  &#10003;   |
| innodb_default_row_format                  |       -         | &#10003;     | &#10003;    |
| innodb_fast_ahi_cleanup_for_drop_table |     -        |      -             | &#10003;     |
| innodb_flush_redo_using_fdatasync     |       -         | &#10003;     | &#10003;    |
| innodb_page_cleaners                         |       -        | &#10003;     | &#10003;     |
| innodb_table_drop_mode                     |      -         |      -             | &#10003;     |
| innodb_temp_tablespace_fast_cleanup |       -        |       -            | &#10003;     |
| internal_tmp_mem_storage_engine       |       -        |      -            | &#10003;    |
| slave_net_timeout                               |  &#10003; | &#10003;     |   -   |
| slave_parallel_type                             |  &#10003; |          -        |  -    |
| slave_parallel_workers                        |  &#10003; | &#10003;   |&#10003;    |
| sort_buffer_size                                  |  &#10003; |    -              |  -    |
| temptable_use_mmap                          |           -      |      -            | &#10003;    |
| thread_handling                                  |   &#10003; | &#10003;   |&#10003;   |
| thread_handling_switch_mode             |        -          |         -          | &#10003;   |
| thread_pool_oversubscribe                  |   &#10003; | &#10003;    |&#10003;    |
| thread_pool_size                                |        -          | &#10003;    | &#10003;   |
| tx_isolation                                        |          -        | &#10003;    | &#10003;    |

### Performance test on template types
The test results are as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0f1aadfa080a43281fd98bea342812e6.png)
![](https://qcloudimg.tencent-cloud.cn/raw/29c6c04452626abe48e32c8370fe3aef.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3ed85cff088505c9f6979c42d5aadf20.png)
。

### How to retain the default parameter template
After the new parameter system is released, the original default parameter template will be replaced by the high-performance and high-stability parameter templates. Before then, you still can retain the default parameter template settings by creating a parameter template. For more information, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).

### Parameter comparison
Parameter comparison between different templates are provided for you to view the parameter difference between different templates.
![](https://qcloudimg.tencent-cloud.cn/raw/8529618ea8427864dea55f10b675ecb4.png)
Click **Compare** on the parameter template page and select the templates to be compared in the pop-up window. Only templates for databases on the same version can be compared. The result is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/aad046642c7bec92ccacfda616887781.png"  style="zoom:80%;">

## Contact Us
[Contact us](https://console.cloud.tencent.com/workorder/category) if you have any questions. Thank you for your support for Tencent Cloud. We will continue to provide you with more cost-effective products.

