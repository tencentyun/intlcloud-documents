## 기능 소개
row 모드에서는 하나의 명령으로 여러 행을 갱신하는 대규모 트랜잭션이 행당 1개의 event를 생성하는데, 한편으로는 많은 수의 binlog가 생성되는 반면, 복제 시 백업 데이터베이스 apply 속도가 비교적 느려, 결과적으로 백업 데이터베이스 복제가 지연됩니다.
Tencent Cloud 커널 팀은 대규모 트랜잭션 복제 시나리오의 분석 및 최적화를 통해 이 기능을 개발했습니다. 대용량 트랜잭션 복제 최적화 기능은 대용량 트랜잭션을 자동으로 식별하고 row 모드 binlog를 statement 형식 binlog로 변환하여 binlog를 줄이고 복제 효율성을 향상시킵니다.

## 지원 버전
- 커널 버전 MySQL 5.6 20210630 이상
- 커널 버전 MySQL 5.7 20200630 이상
- 커널 버전 MySQL 8.0 20200830 이상

## 적용 시나리오
- 이 기능은 주로 row 모드에서 기본 키 테이블이 없는 대용량 트랜잭션의 재생 속도를 향상시킵니다. 기본 키가 없어 딜레이가 발생하는 경우 활성화합니다.
- 이 기능은 주로 row 모드에서 대규모 트랜잭션이 있고 복제가 느린 경우에 적합합니다.

## 성능 데이터
update 복제 시간은 85%, insert는 약 30% 단축됩니다.

## 사용 설명
대규모 트랜잭션 복제의 최적화 기능은 SQL의 과거 실행 통계를 기반으로 대규모 트랜잭션일 가능성 여부를 판단하는 것입니다. 대용량 트랜잭션으로 인식되어 최적화될 수 있는 경우 격리 수준을 자동으로 RR(반복 읽기) 수준으로 업그레이드하고 binlog를 Statement 형식으로 완료하여 대용량 트랜잭션 백업 데이터베이스의 실행 시간을 단축시킵니다. 그 중:
- cdb_optimize_large_trans_binlog는 이 기능의 스위치입니다.
- cdb_sql_statistics는 SQL 연산에 대한 통계 스위치입니다.
- cdb_optimize_large_trans_binlog_last_affected_rows_threshold 및 cdb_optimize_large_trans_binlog_aver_affected_rows_threshold는 대규모 트랜잭션에 대한 임계값 조건을 공동 구성합니다.
- cdb_sql_statistics_info_threshold는 메모리에 저장된 과거 통계 데이터의 수입니다.

트랜잭션의 실행을 더 잘 모니터링하기 위해, 트랜잭션 현황 통계 쿼리에 사용할 수 있는 information_schema 데이터베이스의 테이블 CDB_SQL_STATISTICS도 추가되었습니다.

#### 신규 매개변수

| 이름                                                         | 상태 | 유형      | 기본값 | 설명                                      |
| :----------------------------------------------------------- | :------ | :-------- | :------ | :----------------------------------------------- |
| cdb_optimize_large_trans_binlog                              | true    | bool      | false   | binlog 대규모 트랜잭션 최적화 스위치                           |
| cdb_optimize_large_trans_binlog_last_affected_rows_threshold | true    | ulonglong | 10000   | 대용량 트랜잭션 최적화 조건: 지난 번 행 수에 영향을 미친 임계값              |
| cdb_optimize_large_trans_binlog_aver_affected_rows_threshold | true    | ulonglong | 10000   | 대용량 트랜잭션 최적화 조건: 평균 행 수에 영향을 주는 임계값              |
| cdb_sql_statistics                                           | true    | bool      | false   | SQL 연산에 대한 통계 시작 여부            |
| cdb_sql_statistics_info_threshold                            | true    | ulonglong | 10000   | CDB_SQL_STATISTICS map에 가장 많은 통계가 저장된 SQL의 수 |

#### information_schema.CDB_SQL_STATISTICS 테이블 추가

| 이름                           | 유형                | 설명                                             |
| :----------------------------- | :------------------ | :------------------------------------------------------ |
| DIGEST_MD5                     | MYSQL_TYPE_STRING   | 해당 SQL의 digest에서 변환된 MD5                            |
| DIGEST_TEXT                    | MYSQL_TYPE_STRING   | SQL digest 텍스트 형식                                   |
| SQL_COMMAND                    | MYSQL_TYPE_STRING   | SQL 명령어 유형                                           |
| FIRST_UPDATE_TIMESTAMP         | MYSQL_TYPE_DATETIME | 해당 통계 정보 최초 생성 시간                            |
| LAST_UPDATE_TIMESTAMP          | MYSQL_TYPE_DATETIME | 해당 통계 정보의 마지막 업데이트 시간                              |
| LAST_ACCESS_TIMESTAMP          | MYSQL_TYPE_DATETIME | 해당 통계에 마지막으로 액세스한 시간                          |
| EXECUTE_COUNT                  | MYSQL_TYPE_LONGLONG | 해당 유형의 SQL 실행 횟수                                       |
| TOTAL_AFFECTED_ROWS            | MYSQL_TYPE_LONGLONG | 영향을 받는 총 행 수                                            |
| AVER_AFFECTED_ROWS             | MYSQL_TYPE_LONGLONG | 영향을 받는 평균 행 수                                          |
| LAST_AFFECTED_ROWS             | MYSQL_TYPE_LONGLONG | 마지막으로 영향을 받은 행 수                                          |
| STMT_BINLOG_FORMAT_IF_POSSIBLE | MYSQL_TYPE_STRING   | 해당 유형의 SQL을 statement 형식의 binlog로 완성 가능 여부: TRUE 또는 FALSE |

