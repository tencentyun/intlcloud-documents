
TencentDB for MySQLは、バルクパラメータ設定用のシステムパラメータテンプレートを提供します。システムパラメータテンプレートのパラメータは、バージョンのイテレーションによって最適化、更新される場合があります。ここでは、システムパラメータテンプレートのパラメータの変更についてご説明します。
>?
>- システムパラメータテンプレートのパラメータ変更は、このパラメータテンプレートを使用したことのあるデータベースインスタンスには影響を与えません。バルクインスタンスに新しいパラメータを適用する必要がある場合は、バルクパラメータの設定中にテンプレートをインポートすることでそれらを再適用できます。
>- システムパラメータテンプレートを使用するには、[パラメータテンプレートの使用](https://intl.cloud.tencent.com/document/product/236/31906)をご参照ください。

## MySQL 8.0
### 2020年11月

| パラメータ名                       | タイプの変更   | パラメータの説明                                                     |
| ------------------------------ | ---------- | ------------------------------------------------------------ |
| innodb_flush_log_at_trx_commit | 追加       | Determines Innodb transaction durability                     |
| sync_binlog                    | 追加       | Sync binlog (MySQL flush to disk or rely on OS)              |
| local_infile                   | 追加       | Controls whetther LOCAL is supported for LOAD DATA INFILE    |
| innodb_log_file_size           | 追加       | The size in bytes of each log file in a log group            |
| cdb_recycle_bin_enabled        | 追加       | Control whether the deleted table  is placed in the recycle bin |
| binlog_format                  | 範囲値の更新 | パラメータ範囲値を[row]に更新                                      |
| innodb_autoinc_lock_mode       | デフォルト値の更新 | パラメータデフォルト値を「2」に更新                                          |
| table_open_cache               | デフォルト値の更新 | パラメータデフォルト値を「2000」に更新                                       |
| slave_pending_jobs_size_max    | デフォルト値の更新 | パラメータデフォルト値を「1073741824」に更新                                 |
| time_zone                      | 範囲値の更新 | パラメータ範囲値を[SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]に更新 |
| max_connections                | 範囲値の更新 | パラメータ範囲値を[1～100000]に更新                                 |
| slave_rows_search_algorithms   | デフォルト値の更新 | パラメータデフォルト値を「TABLE_SCAN,INDEX_SCAN,HASH_SCAN」に更新            |
| innodb_open_files              | デフォルト値の更新 | パラメータデフォルト値を「10240」に更新                                       |
| slave_parallel_type            | 範囲値の更新 | パラメータ範囲値を[LOGICAL_CLOCK\|TABLE\|DATABASE] に更新          |


## MySQL 5.7
### 2020年8月

| パラメータ名                        | タイプの変更     | パラメータの説明                                                  |
| ------------------------------- | ------------ | --------------------------------------------------------- |
| log_warnings                    | 追加         | Controls whether to produce additional warning messages   |
| innodb_flush_log_at_trx_committ  | 追加         | Determines Innodb transaction durability                     |
| sync_binlog                     | 追加         | Sync binlog (MySQL flush to disk or rely on OS)           |
| local_infile                    | 追加         | Controls whetther LOCAL is supported for LOAD DATA INFILE |
| innodb_log_file_size            | 追加         | The size in bytes of each log file in a log group         |
| binlog_format                   | 範囲値の更新   |   パラメータ範囲値を[row]に更新                                                           |
| innodb_autoinc_lock_mode        | デフォルト値の更新   |    パラメータデフォルト値を「2」に更新      |
| innodb_open_files               | 範囲値の更新   |   パラメータ範囲値を[1～102400]に更新                |
| table_open_cache                | デフォルト値の更新   |    パラメータデフォルト値を「2000」に更新       |
| slave_pending_jobs_size_max    | デフォルト値の更新   |   パラメータデフォルト値を「1GB」に更新                                 |
| time_zone                       | 範囲値の更新   |  パラメータ範囲値を[SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]に更新 |
| max_connections                 | 範囲値の更新   |   パラメータ範囲値を[1～100000]に更新           |
| cdb_more_gtid_feature_supported |完全なカーネル機能 | -          |
| 並列レプリケーションを有効にする                    | 完全なカーネル機能 |    -                                                       |
| tls_version                     | パラメータオフライン     |     -                                                      |
| slave_rows_search_algorithms    | デフォルト値の更新   | パラメータデフォルト値を「TABLE_SCAN,INDEX_SCAN,HASH_SCAN」に更新            |
| innodb_open_files               | デフォルト値の更新   |    パラメータデフォルト値を「10240」に更新          |

## MySQL 5.6
### 2020年8月

| パラメータ名                        | タイプの変更   | パラメータの説明                                                  |
| ------------------------------- | ---------- | --------------------------------------------------------- |
| log_warnings                    | 追加       | Controls whether to produce additional warning messages   |
| innodb_flush_log_at_trx_commit  | 追加       | Determines Innodb transaction durability                  |
| sync_binlog                     | 追加       | Sync binlog (MySQL flush to disk or rely on OS)           |
| local_infile                    | 追加       | Controls whetther LOCAL is supported for LOAD DATA INFILE |
| innodb_log_file_size            | 追加       | The size in bytes of each log file in a log group         |
| binlog_format                   | 範囲値の更新 |  パラメータ範囲値を[row]に更新                                                         |
| innodb_autoinc_lock_mode        | デフォルト値の更新 |  パラメータデフォルト値を「2」に更新       |
| innodb_open_files               | 範囲値の更新 |  パラメータ範囲値を[1～102400]に更新                               |
| table_open_cache                | デフォルト値の更新 |  パラメータデフォルト値を「2000」に更新         |
| slave_pending_jobs_size_max    | デフォルト値の更新 |  パラメータデフォルト値を「1GB」に更新                                 |
| time_zone                       | 範囲値の更新 |   パラメータ範囲値を[SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]に更新 |
| max_connections                 | 範囲値の更新 |  パラメータ範囲値を[1～100000]に更新      |
| cdb_more_gtid_feature_supported | デフォルト値の更新 |  パラメータデフォルト値を「on」に更新    |
| slave_rows_search_algorithms    | デフォルト値の更新 |   パラメータデフォルト値を「TABLE_SCAN,INDEX_SCAN,HASH_SCAN」に更新 |
| innodb_open_files               | デフォルト値の更新 |  パラメータデフォルト値を「10240」に更新      |


## MySQL 5.5
### 2020年8月

| パラメータ名                        | タイプの変更   | パラメータの説明 |
| ------------------------ | ---------- | -------- |
| innodb_autoinc_lock_mode | デフォルト値の更新 |  パラメータ範囲値を「TABLE_SCAN,INDEX_SCAN,HASH_SCAN」に更新    |
| innodb_open_files               | 範囲値の更新 |  パラメータデフォルト値を「10240」に更新      |
