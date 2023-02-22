TencentDB for MySQL은 사용자가 인스턴스 실행 정보를 쉽게 조회하도록 다양한 성능 모니터링 항목과 편리한 모니터링 기능(사용자 정의 뷰, 시간 비교, 병합된 모니터링 메트릭 등). [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 관리 페이지의 **인스턴스 모니터링**에서 확인할 수 있습니다.
>?
>- [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881) API를 호출하거나 클라우드 모니터링에서 TencentDB for MySQL [모니터링 메트릭](https://intl.cloud.tencent.com/document/product/248/11006)을 사용하여 인스턴스 모니터링 메트릭을 얻을 수 있습니다.
>- 모니터링 메트릭을 위한 [Dashboard 생성](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10)을 통해 모니터링된 데이터를 동적으로 분석할 수 있습니다.
>- 단일 인스턴스의 테이블 수가 100만을 초과하면 데이터베이스 모니터링에 영향을 줄 수 있습니다. 단일 인스턴스의 테이블 수가 100만 미만인지 확인하십시오.

## 모니터링이 지원되는 인스턴스 유형
TencentDB for MySQL 원본, 읽기 전용 및 재해 복구 인스턴스와 데이터베이스 프록시 노드를 모니터링할 수 있으며 각 인스턴스에는 간편한 쿼리를 위해 별도의 모니터링 뷰가 제공됩니다.

## 모니터링 유형
TencentDB for MySQL은 리소스 모니터링, 엔진 모니터링(일반), 엔진 모니터링(확장) 및 배포 모니터링의 네 가지 모니터링 유형이 포함됩니다. 다양한 모니터링 유형의 메트릭을 확인하여 인스턴스 성능과 실행 상태를 빠르고 정확하게 파악할 수 있습니다.
>?TencentDB for MySQL 단일 노드 클라우드 디스크 에디션 인스턴스는 현재 리소스 모니터링 및 엔진 모니터링(일반)을 지원하지만 엔진 모니터링(확장) 및 배포 모니터링은 지원하지 않습니다.
>
- **리소스 모니터링**: CPU, 메모리, 디스크 및 네트워크의 모니터링 데이터를 제공합니다.
- **엔진 모니터링(일반)**: 연결, 잠금, 핫스팟 테이블 및 슬로우 쿼리 수에 대한 모니터링 데이터를 제공하여 문제를 해결하고 성능을 최적화하는 데 도움을 줍니다.
- **엔진 모니터링(확장)**: 다양한 엔진 관련 모니터링 메트릭을 제공하여 데이터베이스에 존재하거나 잠재하는 문제를 최대한 식별할 수 있도록 합니다.
- **배포 모니터링**: 원본-복제 딜레이와 관련된 모니터링 메트릭을 제공합니다. 배포 모니터링은 원본 모니터링과 복제본 모니터링으로 나뉩니다.
 - 인스턴스가 원본 인스턴스인 경우 인스턴스 배포 모니터링의 객체는 원본 인스턴스와 숨겨진 복제본 간의 연결이며, 배포 모니터링은 숨겨진 복제본의 IO 및 SQL 스레드 상태를 표시합니다. 원본-복제본 딜레이 거리(MB) 및 원본-복제본 딜레이 시간(초)은 원본 인스턴스와 숨겨진 복제본 간의 딜레이에 대한 것입니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5LFE331_11.png)
 - 인스턴스가 읽기 전용 인스턴스인 경우 인스턴스 배포 모니터링의 객체는 원본 인스턴스와 읽기 전용 인스턴스 간의 연결이며, 배포 모니터링은 읽기 전용 인스턴스의 IO, SQL 스레드 상태를 표시합니다. 원본-복제본 딜레이 거리(MB) 및 원본-복제본 딜레이 시간(초)은 읽기 전용 인스턴스와 원본 인스턴스 간의 딜레이에 대한 것입니다.
 - 인스턴스가 재해 복구 인스턴스인 경우:
 a. 인스턴스 배포 모니터링(원본)의 객체는 재해 복구 인스턴스와 원본 인스턴스 간의 연결이며, 배포 모니터링은 재해 복구 인스턴스의 IO, SQL 스레드 상태를 표시합니다. 원본-복제본 딜레이 거리(MB) 및 원본-복제본 딜레이 시간(초)은 재해 복구 인스턴스와 원본 인스턴스 간의 딜레이에 대한 것입니다.
    b. 인스턴스 배포 모니터링(복제본)의 객체는 재해 복구 인스턴스와 숨겨진 복제본 간의 연결이며 배포 모니터링은 숨겨진 복제본의 IO, SQL 스레드 상태를 표시합니다. 원본-복제본 딜레이 거리(MB) 및 원본-복제본 딜레이 시간(초)은 재해 복구 인스턴스와 숨겨진 복제본 간의 딜레이에 대한 것입니다.

## 모니터링 세분성
TencentDB for MySQL은 2018년 8월 11일부터 모니터링 세분성에 대해 어댑티브 정책을 채택했습니다. 즉, 당분간 모니터링 세분성을 원하는 대로 선택할 수 없습니다. 어댑티브 정책은 다음과 같습니다.

| 시간 범위 | 모니터링 세분성 | 어댑티브 설명 | 보관 기간 |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5s | 시간 범위는 4시간 미만이고 모니터링 세분성은 5초 | 1일 |
| (4h, 2d] | 1min | 시간 범위는 4시간 이상 2일 미만이며 모니터링 세분성은 1분 | 15일 |
| (2d, 10d] | 5min | 시간 범위는 2일 이상 10일 미만이며 모니터링 세분성은 5분 | 31일 |
| (10d, 30d] | 1h | 시간 범위는 10일 이상 30일 미만이며 모니터링 세분성은 1시간 | 62일 |

>?현재 TencentDB for MySQL의 지난 30일 동안의 모니터링 데이터를 볼 수 있습니다.

## 모니터링 메트릭
클라우드 모니터링은 인스턴스 차원에서 TencentDB for MySQL 인스턴스에 대해 다음과 같은 모니터링 메트릭을 제공합니다.

>?TencentDB 모니터링 메트릭 사용 방법에 대한 자세한 내용은 Cloud Monitor API 중의 [TencentDB for MySQL API](https://www.tencentcloud.com/document/product/248/48735)를 참고하십시오.

| 메트릭 중문명 | 메트릭 영문명 | 단위 |설명|
|---------|---------|---------|---------|
| 초당 쿼리 수 | qps | 회/초 | 초당 데이터베이스에서 실행한 SQL 문(insert, select, update, delete, replace) 수입니다. 이 메트릭은 주로 TencentDB 인스턴스의 실제 처리 능력을 나타냅니다. |
| 초당 트랜잭션 수 | tps | 회/초| 데이터베이스에서 초당 실행된 트랜잭션 수 |
| 슬로우 쿼리 수 |slow_queries | 회 | long_query_time 초 이상 실행된 쿼리 수 |
| 전체 테이블 스캔 수 |select_scan | 회/초 | 초당 실행되는 전체 테이블 스캔 수 |
| SELECT 쿼리 수             | select_count | 회/초 | 초당 실행되는 쿼리 수 |
| UPDATE 쿼리 수             | com_update | 회/초 | 초당 실행된 업데이트 수 |
| DELETE 쿼리 수             | com_delete  | 회/초 | 초당 실행된 삭제 수 |
| INSERT 쿼리 수             | com_insert   | 회/초 | 초당 실행되는 삽입 수 |
| REPLACE 쿼리 수             | om_replace  | 회/초 | 초당 실행되는 교체 횟수 |
| 총 쿼리 수        | queries      | 회/초 | set, show와 같은 실행된 모든 SQL 문 |
| 열린 연결 수 | threads_connected | 개 | 현재 열려 있는 연결 수 |
| 연결 이용률 | connection_use_rate | % | 열린 연결 수 / 최대 연결 수 |
| 쿼리 이용률       | query_rate                | %  | 실제 QPS/권장 QPS |
| 총 디스크 사용량 | capacity | MB | 여기에는 binlog, relaylog, undolog, errorlog, slowlog와 같은 MySQL의 데이터 디렉터리 및 로그가 포함 |
| 데이터가 사용하는 디스크 공간 | real_capacity | MB | 여기에는 MySQL의 데이터 디렉터리만 포함, binlog, relaylog, undolog, errorlog, slowlog 로그는 포함하지 않음 |
| 로그 파일이 사용하는 디스크 공간 | log_capacity  | MB | 여기에는 binlog, relaylog, undolog, errorlog, slowlog와 같은 MySQL의 로그만 포함 |
| 로그 파일이 사용하는 디스크 공간 | disk_log_used  | MB | 여기에는 MySQL의 binlog, relaylog, undolog만 포함 |
| 임시 파일이 사용하는 디스크 공간 | disk_tmp_used | MB | 여기에는 MySQL의 임시 파일만 포함 |
| 디스크 이용률      | volume_rate     | %         | 총 디스크 사용량 / 구매한 인스턴스 공간         |
| 프라이빗 아웃바운드 트래픽 | bytes_sent       | Byte/초 | 초당 전송 바이트 수 |
| 프라이빗 인바운드 트래픽 | bytes_received | Byte/초 | 초당 수신 바이트 수 |
| 쿼리 캐시 히트율 | qcache_hit_rate         | % | 쿼리 캐시 히트율 |
| 쿼리 캐시 사용률 | qcache_use_rate       | % | 쿼리 캐시 사용률 |
| 테이블 잠금 대기 수 | table_locks_waited | 회/초 | 테이블 잠금 요청이 즉시 승인되지 않아 대기가 필요한 횟수 |
| 임시 테이블 수 | created_tmp_tables   | 회/초 | 문을 실행하는 동안 서버에서 생성한 내부 임시 테이블의 수 |
| innodb 캐시 히트율 | innodb_cache_hit_rate  | % | Innodb 엔진 캐시 히트율 |
| innodb 캐시 사용률 | innodb_cache_use_rate | % | Innodb 엔진 캐시 사용률 |
| innodb 디스크 읽기 수 | innodb_os_file_reads    | 회/초 | Innodb 내의 읽기 스레드가 수행한 총 파일 읽기 횟수 |
| innodb 디스크 쓰기 수 | innodb_os_file_writes   | 회/초 | Innodb 내의 쓰기 스레드가 수행한 총 파일 쓰기 횟수 |
| innodb fsync 호출 수  | innodb_os_fsyncs         | 회/초 | Innodb가 초당 fsync 함수를 호출한 횟수 |
| InnoDB에 의해 열린 테이블 수 | innodb_num_open_files  | 개 | Innodb가 현재 열어 놓은 파일 수| 
| myisam 캐시 히트율  | key_cache_hit_rate  | %   | myisam 엔진 캐시 히트율 |
| myisam 캐시 사용률  | key_cache_use_rate | %   | myisam 엔진 캐시 사용률 |
| CPU 이용률              | cpu_use_rate            | %   | 유휴 리소스의 과도한 사용이 허용되면 CPU 사용률이 100%를 초과할 수 있음 |
| 메모리 이용률               | memory use rate     | %   | 유휴 리소스의 과도한 사용이 허용되면 메모리 사용률이 100%를 초과할 수 있음  |
| 메모리 사용량               |memory_use       | MB | 유휴 리소스의 과도한 사용이 허용되면 사용 메모리가 구매 사양을 초과할 수 있음 |
| 임시 파일 수량            | created_tmp_files    | 회/초 | 초당 생성되는 임시 파일 수 |
| 열려 있는 테이블 수        | opened_tables         | 개      | 열린 테이블 수 |
| COMMIT 문 수                    | com_commit            | 회/초 | 초당 제출 문 수 |
| 롤백 문 수                     | com_rollback           | 회/초 | 초당 롤백 문 수 |
| 생성된 스레드 수          | threads_created      | 개 | 연결을 처리하기 위해 생성된 스레드 수 |
| 실행된 스레드 수           | threads_running      | 개 | 활성화된(비수면 상태) 스레드 수 |
| 최대 연결 수                | max_connections    | 개 | 최대 연결 수 |
| 임시 디스크 테이블 수      | created_tmp_disk_tables | 회/초 |초당 디스크 임시 테이블 생성 횟수 |
| 다음 행 읽기 요청 수       | handler_read_rnd_next    | 회/초 | 데이터 파일에서 다음 행을 읽기 위한 요청 수 |
| 스토리지 엔진에서 수행된 롤백 수              | handler_rollback     | 스토리지 엔진이 롤백 작업을 수행하기 위한 요청 수 |
| 내부 COMMIT 문 수               | handler_commit     | 회/초 | 초당 내부 COMMIT 문 수 |
| InnoDB 빈 페이지 수         | innodb_buffer_pool_pages_free    | 개  | Innodb 버퍼 풀의 빈 페이지 수  |
| 총 InnoDB 페이지 수         | innodb_buffer_pool_pages_total  | 개  | Innodb 버퍼 풀의 전체 페이지 수  |
| InnoDB 논리적 읽기 수        | innodb_buffer_pool_read_requests  | 회/초  | 논리적 읽기 요청 수  |
| InnoDB 물리적 읽기 수         | innodb_buffer_pool_reads  | 회/초  | Innodb가 버퍼 풀에서 만족할 수 없고 디스크에서 직접 읽어야 하는 논리적 읽기 수  |
| InnoDB에서 데이터 읽기          | innodb_data_read         | Byte/초  | 초당 읽은 데이터의 양  |
| InnoDB 총 읽기 수      | innodb_data_reads      | 회/초    | 초당 총 데이터 읽기 수  |
| InnoDB 총 쓰기 수      | innodb_data_writes     | 회/초      | 초당 총 데이터 쓰기 수  |
| InnoDB에 작성된 데이터         | innodb_data_written     | Byte/초    | 초당 기록되는 데이터의 양  |
| InnoDB 행 삭제 수      | innodb_rows_deleted   | 회/초  | Innodb 테이블에서 삭제된 행 수  |
| InnoDB 행 삽입 수      | innodb_rows_inserted  | 회/초  | Innodb 테이블에 삽입된 행 수  |
| InnoDB 행 업데이트 수      | innodb_rows_updated  | 회/초  | Innodb 테이블에서 업데이트된 행 수  |
| InnoDB 행 읽기 수      | innodb_rows_read       | 회/초  | Innodb 테이블에서 읽은 행 수  |
| InnoDB 평균 행 잠금 획득 시간 | innodb_row_lock_time_avg  | 밀리초  | Innodb 테이블에 대한 행 잠금을 획득하는 평균 시간  |
| InnoDB 행 잠금 대기 횟수      | innodb_row_lock_waits       | 회/초 | Innodb 테이블에 대한 작업이 행 잠금을 기다려야 하는 횟수  |
| 키 캐시 미사용 블록 수   | key_blocks_unused              | 개     | myisam 키 캐시에서 사용하지 않는 키 블록 수  |
| 키 캐시 내 사용된 블록 수      | key_blocks_used                  | 개     | myisam 키 캐시에서 사용하는 키 블록 수  |
| 키 캐시에서 읽기 블록 횟수       | key_read_requests   | 회/초 | myisam 키 캐시에서 키 블록을 읽기 위한 요청 수  |
| 디스크에서 읽은 블록 횟수         | key_reads                | 회/초 | myisam 키 캐시에서 디스크 데이터 블록을 읽기 위한 요청 수|
| 키 캐시에 기록된 블록 횟수     | key_write_requests   | 회/초 | myisam 키 캐시에 키 블록 쓰기 요청 수|
| 디스크에 기록된 블록 횟수         | key_writes                | 회/초 | myisam 키 캐시에 디스크 데이터 블록을 쓰기 위한 요청 수|
| 원본-복제본 딜레이 거리     | master_slave_sync_distance  | MB | 복제본이 원본보다 딜레이된 데이터의 양  |
| 원본-복제본 딜레이 시간     | seconds_behind_master        |초   | 원본-복제본 딜레이 시간(초)  |
| IO 스레드 상태       | slave_io_running   | 상태값(0-Yes, 1-No, 2-Connecting) | IO 스레드 실행 상태     |
| SQL 스레드 상태    |slave_sql_running  |상태값(0-Yes, 1-No)                      | SQL 스레드 실행 상태  |
