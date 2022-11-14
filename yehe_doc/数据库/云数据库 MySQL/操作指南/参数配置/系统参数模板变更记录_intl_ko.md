
TencentDB for MySQL은 배치 매개변수 설정을 위한 시스템 매개변수 템플릿을 제공합니다. 시스템 매개변수 템플릿의 매개변수는 MySQL 반복을 통해 최적화되고 업데이트될 수 있습니다. 본 문서는 시스템 매개변수 템플릿에 있는 매개변수의 업데이트 이력에 대해 설명합니다.
>?
>- 시스템 매개변수 템플릿의 매개변수 변경 사항은 이미 템플릿을 적용한 데이터베이스 인스턴스에 영향을 미치지 않습니다. 인스턴스 배치에 새 매개변수를 적용해야 하는 경우 매개변수를 배치로 설정할 때 업데이트된 템플릿을 가져올 수 있습니다.
>- 시스템 매개변수 템플릿 사용법은 [매개변수 템플릿 사용](https://intl.cloud.tencent.com/document/product/236/31906)을 참고하십시오.

## 2022년 08월
| 매개변수 | MySQL 5.7 | MySQL 8.0 |  변경 설명 | 
|---------|---------|---------|---------|
| innodb_buffer_pool_size | &#10003; | &#10003;|  innodb_buffer_pool_size 매개변수는 동적 구성 지원<br><li>재시작 필요: 아니오<br><li>기본값: {DBInitMemory * 786432}<br><li>매개변수 수정 가능 값: {DBInitMemory * 524288} - {DBInitMemory * 943718}<br><li>DBinitMemory는 인스턴스 사양의 메모리 크기에 대한 정수 |

## 2022년 07월
| 매개변수 | MySQL 5.7 | MySQL 8.0 |  변경 설명 | 
|---------|---------|---------|---------|
| innodb_temp_data_file_path | &#10003; | &#10003;| innodb_temp_data_file_path(임시 테이블 공간 크기) 매개변수 수정 지원, 매개변수 속성은 다음과 같음: <br><li>재시작 필요: 예<br><li>기본값: ibtmp1:12M:autoextend<br><li>매개변수 수정 가능: ibtmp1은 12 - 1024MB, autoextend 선택 후 설정할 수 있는 max 최대값은 2097152MB |

## 2022년 03월
| 매개변수 |  MySQL 5.6 |  MySQL 5.7 |  MySQL 8.0 |  변경 설명 | 
|---------|---------|---------|---------|---------|
| innodb_open_files | &#10003; | &#10003; | &#10003; | 제거됨 |
| innodb_stats_sample_pages | - | &#10003; | &#10003; | 제거됨 |
| wait_timeout | &#10003; | &#10003; | &#10003; | 새 값 범위: 1 - 31536000 |
| thread_cache_size | &#10003; | &#10003; | &#10003; | 새 값 범위: 1 - 16384 |

## 2021년 12월
| 매개변수 |  MySQL 5.6 |  MySQL 5.7 |  MySQL 8.0 |  변경 설명 | 
|---------|---------|---------|---------|---------|
| binlog_row_image | &#10003; | &#10003; | &#10003; | 매개변수의 기본값은 FULL로 통합되어 있으며, 이 매개변수의 기본값은 이전에 생성된 인스턴스의 경우 MINIMAL이며 수동 수정이 지원된다는 점에 주의하십시오. |

## 2020년 11월
| 매개변수 |  MySQL 8.0 |  변경 설명 | 
|---------|---------|---------|
| iinnodb_flush_log_at_trx_commit | &#10003; | 새 매개변수 |
| sync_binlog | &#10003; | 새 매개변수 |
| local_infile  | &#10003; | 새 매개변수 |
| innodb_log_file_size | &#10003; | 새 매개변수 |
| cdb_recycle_bin_enabled | &#10003; | 새 매개변수 |
| binlog_format| &#10003; | 유효한 새 값: row |
| innodb_autoinc_lock_mode | &#10003; | 새 기본값: 2 |
| table_open_cache | &#10003; | 새 기본값: 2000 |
| slave_pending_jobs_size_max | &#10003; | 새 기본값: 1073741824 |
| time_zone | &#10003; | 새 유효 값: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections | &#10003; | 새 값 범위: 1 - 100000 |
| slave_rows_search_algorithms | &#10003; | 새 기본값: TABLE_SCAN,INDEX_SCAN,HASH_SCAN |
| innodb_open_files | &#10003; | 새 기본값: 10240 |
| slave_parallel_type | &#10003; | 새 유효한 값: LOGICAL_CLOCK\|TABLE\|DATABASE |

## 2020년 08월
| 매개변수 | MySQL 5.6 | MySQL 5.7 |  변경 설명 | 
|---------|---------|---------|---------|
| log_warnings | &#10003; | &#10003; | 새 매개변수 |
| innodb_flush_log_at_trx_commit | &#10003; | &#10003; | 새 매개변수 |
| sync_binlog | &#10003; | &#10003; | 새 매개변수 |
| local_infile | &#10003; | &#10003; | 새 매개변수 |
| innodb_log_file_size | &#10003; | &#10003; | 새 매개변수 |
| binlog_format | &#10003; | &#10003; | 유효한 새 값: row |
| innodb_autoinc_lock_mode | &#10003; | &#10003; | 새 기본값: 2 |
| innodb_open_files | &#10003; | &#10003; | 새 값 범위: 1 - 102400 |
| table_open_cache | &#10003; | &#10003; | 새 기본값: 2000 |
| slave_pending_jobs_size_max | &#10003; | &#10003; | 새 기본값: 1GB |
| time_zone | &#10003; | &#10003; | 새 유효 값: [SYSTEM\|-12:00\|-11:00\|-10:00\|-09:00\|-08:00\|-07:00\|-06:00\|<br>-05:00\|-04:00\|-03:00\|-02:00\|-01:00\|\+00:00\|\+01:00\|\+02:00\|\+03:00\|\+04:00\|\+05:00\|<br>\+05:30\|\+06:00\|\+06:30\|\+07:00\|\+08:00\|\+09:00\|\+10:00\|\+11:00\|\+12:00\|\+13:00] |
| max_connections | &#10003; | &#10003; | 새 값 범위: 1 - 100000 |
| cdb_more_gtid_feature_supported | - | &#10003; | 지원되는 모든 커널 기능(매개변수 포함) |
| cdb_more_gtid_feature_supported | &#10003; | - | 새 기본값: OFF |
| slave_parallel_workers | - | &#10003; | 지원되는 모든 커널 기능(매개변수 포함) |
| tls_version | - | &#10003; | Removed |
| slave_rows_search_algorithms | &#10003; | &#10003; | 새 기본값: TABLE_SCAN,INDEX_SCAN,HASH_SCAN |
| innodb_open_files | &#10003; | &#10003; | 새 기본값: 10240 |

## 2020년 08월
| 매개변수 |  MySQL 5.5 |  변경 설명 | 
|---------|---------|---------|
| innodb_autoinc_lock_mode | &#10003; | 새 기본값: TABLE_SCAN,INDEX_SCAN,HASH_SCAN |
| innodb_open_files | &#10003;| 새 기본값: 10240 |

