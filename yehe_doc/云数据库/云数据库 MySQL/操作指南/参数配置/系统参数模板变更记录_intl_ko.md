
TencentDB for MySQL은 매개 변수 일괄 설정에 사용되는 시스템 매개변수 템플릿을 제공하며 관련 매개변수는 버전 업그레이드에 맞춰 최적화됩니다. 본 문서는 시스템 매개변수 템플릿의 매개변수 변경 레코드에 대해 소개합니다.
>?
>- 시스템 매개변수 템플릿의 매개변수 변경은 해당 매개변수 템플릿을 사용했던 데이터베이스 인스턴스에 영향을 주지 않습니다. 새로운 매개변수를 대량의 인스턴스에 적용해야 하는 경우, 대량 매개변수 설정 시 템플릿 가져오기를 통해 적용할 수 있습니다.
>- 시스템 매개변수 템플릿 사용에 관한 자세한 내용은 [매개변수 템플릿 사용](https://intl.cloud.tencent.com/document/product/236/31906)을 참고하십시오. 

## MySQL 8.0
### 2020년 11월

| 매개변수 이름                       | 변경 유형   | 매개변수 설명                                                     |
| ------------------------------ | ---------- | ------------------------------------------------------------ |
| innodb_flush_log_at_trx_commit | 추가       | Determines Innodb transaction durability                     |
| sync_binlog                    | 추가       | Sync binlog (MySQL flush to disk or rely on OS)              |
| local_infile                   | 추가       | Controls whetther LOCAL is supported for LOAD DATA INFILE    |
| innodb_log_file_size           | 추가       | The size in bytes of each log file in a log group            |
| cdb_recycle_bin_enabled        | 추가       | Control whether the deleted table  is placed in the recycle bin |
| binlog_format                  | 범위 값 업데이트 | 매개변수 범위 값을 [row]로 업데이트                                      |
| innodb_autoinc_lock_mode       | 기본값 업데이트 | 매개변수 기본값을 2로 업데이트                                          |
| table_open_cache               | 기본값 업데이트 | 매개변수 기본값을 2000으로 업데이트                                       |
| slave_pending_jobs_size_max    | 기본값 업데이트 | 매개변수 기본값을 1073741824로 업데이트                                |
| time_zone                      | 범위 값 업데이트 | 매개변수 범위 값을[SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]으로 업데이트 |
| max_connections                | 범위 값 업데이트 | 매개변수 범위 값을 [1-100000]으로 업데이트                                  |
| slave_rows_search_algorithms   | 기본값 업데이트 | 매개변수 기본값을 TABLE_SCAN,INDEX_SCAN,HASH_SCAN으로 업데이트            |
| innodb_open_files              | 기본값 업데이트 | 매개변수 기본값을 10240으로 업데이트                                      |
| slave_parallel_type            | 범위 값 업데이트 | 매개변수 범위 값을 [LOGICAL_CLOCK\|TABLE\|DATABASE]로 업데이트           |


## MySQL 5.7
### 2020년 08월

| 매개변수 이름                       | 변경 유형   | 매개변수 설명                                                     |
| ------------------------------- | ------------ | --------------------------------------------------------- |
| log_warnings                    | 추가         | Controls whether to produce additional warning messages   |
| innodb_flush_log_at_trx_commit  | 추가         | Determines Innodb transaction durability                  |
| sync_binlog                     | 추가         | Sync binlog (MySQL flush to disk or rely on OS)           |
| local_infile                    | 추가         | Controls whetther LOCAL is supported for LOAD DATA INFILE |
| innodb_log_file_size            | 추가         | The size in bytes of each log file in a log group         |
| binlog_format                   | 범위 값 업데이트   |   매개변수 범위 값을 [row]로 업데이트                                                           |
| innodb_autoinc_lock_mode        | 기본값 업데이트   |    매개변수 기본값을 2로 업데이트      |
| innodb_open_files               | 범위 값 업데이트   |   매개변수 범위 값을 [1 - 102400]으로 업데이트                |
| table_open_cache                | 기본값 업데이트   |    매개변수 기본값을 2000으로 업데이트       |
| slave_pending_jobs_size_max     | 기본값 업데이트   |   매개변수 기본값을 1GB으로 업데이트   |
| time_zone                       | 범위 값 업데이트   |  매개변수 범위 값을 [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]으로 업데이트       |
| max_connections                 | 범위 값 업데이트   |   매개변수 범위 값을 [1-100000]으로 업데이트           |
| cdb_more_gtid_feature_supported | 전체 커널 기능 | -          |
| 병렬 작업 활성화                    | 전체 커널 기능 |    -                                                       |
| tls_version                     | 매개변수 삭제     |     -                                                      |
| slave_rows_search_algorithms    | 기본값 업데이트   | 매개변수 기본값을 TABLE_SCAN,INDEX_SCAN,HASH_SCAN으로 업데이트 |
| innodb_open_files               | 기본값 업데이트   |    매개변수 기본값을 10240으로 업데이트          |

## MySQL 5.6
### 2020년 08월

| 매개변수 이름                       | 변경 유형   | 매개변수 설명                                                     |
| ------------------------------- | ---------- | --------------------------------------------------------- |
| log_warnings                    | 추가       | Controls whether to produce additional warning messages   |
| innodb_flush_log_at_trx_commit  | 추가       | Determines Innodb transaction durability                  |
| sync_binlog                     | 추가       | Sync binlog (MySQL flush to disk or rely on OS)           |
| local_infile                    | 추가       | Controls whetther LOCAL is supported for LOAD DATA INFILE |
| innodb_log_file_size            | 추가       | The size in bytes of each log file in a log group         |
| binlog_format                   | 범위 값 업데이트 |  매개변수 범위 값을 [row]로 업데이트                                                         |
| innodb_autoinc_lock_mode        | 기본값 업데이트 |  매개변수 기본값을 2로 업데이트       |
| innodb_open_files               | 범위 값 업데이트 |  매개변수 범위 값을 [1 - 102400]으로 업데이트                               |
| table_open_cache                | 기본값 업데이트 |  매개변수 기본값을 2000으로 업데이트         |
| slave_pending_jobs_size_max     | 기본값 업데이트 |  매개변수 기본값을 1GB로 업데이트     |
| time_zone                       | 범위 값 업데이트 |   매개변수 범위 값을[SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00]으로 업데이트      |
| max_connections                 | 범위 값 업데이트 |  매개변수 범위 값을 [1-100000]으로 업데이트      |
| cdb_more_gtid_feature_supported | 기본값 업데이트 |  매개변수 기본값을 on으로 업데이트    |
| slave_rows_search_algorithms    | 기본값 업데이트 |   매개변수 기본값을 TABLE_SCAN,INDEX_SCAN,HASH_SCAN으로 업데이트 |
| innodb_open_files               | 기본값 업데이트 |   매개변수 기본값을 10240으로 업데이트      |


## MySQL 5.5
### 2020년 08월

| 매개변수 이름                       | 변경 유형   | 매개변수 설명                                                     |
| ------------------------ | ---------- | -------- |
| innodb_autoinc_lock_mode | 기본값 업데이트 |  매개변수 기본값을 TABLE_SCAN,INDEX_SCAN,HASH_SCAN으로 업데이트     |
| innodb_open_files        | 범위 값 업데이트 |  매개변수 기본 값을 10240으로 업데이트        |
