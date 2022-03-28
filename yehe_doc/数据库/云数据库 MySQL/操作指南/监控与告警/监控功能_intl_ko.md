TencentDB for MySQL은 사용자가 인스턴스 실행 정보를 쉽게 조회하도록 다양한 성능 모니터링 항목과 편리한 모니터링 기능(사용자 정의 뷰, 시간 비교, 통합 모니터링 항목 등)을 제공합니다. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 관리 페이지의 **인스턴스 모니터링**에 접속하면 조회할 수 있습니다.
>?
>- Cloud Monitoring API의 [지표 모니터링 데이터 풀링](https://intl.cloud.tencent.com/document/product/248/33881), [TencentDB for MySQL 모니터링 지표](https://intl.cloud.tencent.com/document/product/248/11006)를 통해 인스턴스 모니터링 지표를 확인할 수 있습니다.
>- [Dashboard 생성](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10)을 통한 지표 모니터링 데이터의 동적 분석도 가능합니다.
>- 단일 인스턴스의 테이블 수량이 100만 개를 초과하면 데이터베이스 모니터링에 영향을 미칠 수 있으므로 테이블 수량을 합리적인 수준으로 적용하고, 단일 인스턴스 테이블 수량이 100만 개를 넘지 않도록 제어하시기 바랍니다.

## 모니터링을 지원하는 인스턴스 유형
TencentDB for MySQL은 프라이머리 인스턴스, 읽기 전용 인스턴스, 재해 복구 인스턴스를 지원하며, 뿐만 아니라 데이터베이스 프록시 노드의 모니터링, 각 인스턴스에 대한 독립적인 모니터링 이미지를 제공합니다.

## 모니터링 분류
TencentDB for MySQL의 모니터링 유형은 리소스 모니터링, 엔진 모니터링(일반), 엔진 모니터링(확장), 배포 모니터링으로 구분됩니다. 각 유형의 모니터링 지표를 이용하면 인스턴스 성능과 실행 상태를 빠르고 정확하게 파악할 수 있습니다.
- **리소스 모니터링**: CPU, 메모리, 디스크 및 네트워크 관련 모니터링 데이터를 제공합니다.
- **엔진 모니터링(일반)**: 연결 수, lock 정보, 핫스팟 테이블, 슬로우 쿼리 등과 관련된 모니터링 데이터를 제공하여 장애 진단과 성능 최적화를 편리하게 진행할 수 있습니다.
- **엔진 모니터링(확장)**: 다양한 엔진 관련 모니터링 지표를 제공하여 데이터베이스에 존재하거나 잠재하는 문제를 최대한 탐지할 수 있도록 합니다.
- **배포 모니터링**: 프라이머리/세컨더리 딜레이와 관련된 모니터링 지표를 제공합니다. 배포 모니터링은 호스트와 세컨더리로 구분됩니다.
 - 인스턴스가 프라이머리 인스턴스인 경우 인스턴스 배포 모니터링의 객체는 프라이머리 인스턴스와 숨겨진 세컨더리 간의 링크이며, 배포 모니터링은 숨겨진 세컨더리의 IO 및 SQL 스레드 상태를 표시합니다. 프라이머리/세컨더리 딜레이 거리 및 프라이머리/세컨더리 딜레이 시간은 프라이머리 인스턴스와 숨겨진 세컨더리 사이입니다.
 - 인스턴스가 읽기 전용 인스턴스인 경우 인스턴스 배포 모니터링의 객체는 프라이머리 인스턴스와 읽기 전용 인스턴스 간의 링크이며, 배포 모니터링은 읽기 전용 인스턴스의 IO, SQL 스레드 상태를 표시합니다. 프라이머리/세컨더리 딜레이 거리 및 프라이머리/세컨더리 딜레이 시간은 읽기 전용 인스턴스와 프라이머리 인스턴스 사이를 뜻합니다.
 - 인스턴스가 재해 복구 인스턴스인 경우:
 a. 재해 복구 인스턴스 배포 모니터링(호스트)의 객체는 재해 복구 인스턴스와 프라이머리 인스턴스 간의 링크이며, 배포 모니터링은 재해 복구 인스턴스의 IO, SQL 스레드 상태를 표시합니다. 프라이머리/세컨더리 딜레이 거리 및 프라이머리/세컨더리 딜레이 시간은 재해 복구 인스턴스와 프라이머리 인스턴스 사이를 뜻합니다.
 b. 재해 복구 인스턴스 배포 모니터링(세컨더리)의 객체는 재해 복구 인스턴스와 숨겨진 세컨더리 간의 링크이며 배포 모니터링은 숨겨진 세컨더리의 IO, SQL 스레드 상태를 표시합니다. 프라이머리/세컨더리 딜레이 거리 및 프라이머리/세컨더리 딜레이 시간은 재해 복구 인스턴스와 숨겨진 세컨더리 사이를 뜻합니다.

## 모니터링 데이터 분할 정도
2018년 08월 11일 부터 TencentDB for MySQL 모니터링 데이터 분할 정도에 자동 맞춤 정책이 시행되어 현재 모니터링 데이터 분할 정도에 대한 사용자 정의가 지원되지 않습니다. 모니터링 데이터 분할 정도에 관한 자동 맞춤 정책은 다음과 같습니다.

| 시간 간격 | 모니터링 데이터 분할 정도 | 자동 맞춤 설명 | 보관 기간 |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5s | 시간 간격은 4시간 이내, 모니터링 데이터 분할 정도는 5초 | 1일 |
| (4h, 2d] | 1min | 시간 간격은 4시간 이상이나 2일 내에 모니터링 데이터 분할 정도를 1분으로 조정 | 15일 |
| (2d, 10d] | 5min | 시간 간격은 2일 이상이나 10일 내에 모니터링 데이터 분할 정도를 5분으로 조정 | 31일 |
| (10d, 30d] | 1h | 시간 간격은 10일 이상이나 30일 내 모니터링 데이터 분할 정도를 1시간으로 조정 | 62일 |

>?현재 TencentDB for MySQL은 최장 30일의 모니터링 데이터 조회를 지원합니다.

## 모니터링 지표
Tencent Cloud 클라우드 모니터링은 인스턴스 차원에서 TencentDB for MySQL 인스턴스에 다음 모니터링 지표를 제공합니다.

>?더 많은 CDB 모니터링 지표 사용 방법 사용 방법은 Cloud Monitoring API의 [TencentDB for MySQL 인터페이스](https://intl.cloud.tencent.com/document/product/248/11006)를 참고 바랍니다.

| 지표 중문명 | 지표 영문명 | 단위 |지표 설명|
|---------|---------|---------|---------|
| 초당 실행하는 작업 수 | qps | 회/초 | 데이터베이스가 초당 실행하는 SQL 수(insert, select, update, delete, replace 등), QPS 지표는 주로 TencentDB 인스턴스의 실제 처리 능력을 구현 |
| 초당 실행하는 트랜잭션 수 | tps | 회/초| 데이터베이스가 초당 전송하는 트랜잭션 처리 수 |
| 슬로우 쿼리 수 |slow_queries | 회 | 조회 시간이 long_query_time초를 초과하는 쿼리 수 |
| 전체 테이블 스캔 수 |select_scan | 회/초 | 전체 테이블 검색 조회 실행 수 |
| 쿼리 수             | select_count | 회/초 | 초당 쿼리 수 |
| 업데이트 수             | com_update | 회/초 | 초당 업데이트 수 |
| 삭제 수             | com_delete  | 회/초 | 초당 삭제 수 |
| 삽입 수             | com_insert   | 회/초 | 초당 삽입 수 |
| 덮어쓰기 수             | om_replace  | 회/초 | 초당 덮어쓰기 수 |
| 총 요청 수        | queries      | 회/초 |  set, show 등 실행한 모든 SQL 명령 |
| 현재 열린 연결 수 | threads_connected | 개 | 현재 열린 연결 수 |
| 연결 수 이용률 | connection_use_rate | % | 현재 열린 연결 수 / 최대 연결 수   |
| 쿼리 사용률       | query_rate                | %  | 초당 작업 수 QPS/초당 권장 작업 수 |
| 디스크 총 사용 공간 | capacity | MB | MySQL 데이터 디렉터리 및 binlog, relaylog, undolog, errorlog, slowlog 로그 공간 포함 |
| 데이터 사용 공간 | real_capacity | MB | MySQL 데이터 디렉터리만 포함, binlog, relaylog, undolog, errorlog, slowlog 로그 공간은 포함하지 않음 |
| 로그 사용 공간 | log_capacity  | MB | binlog, relaylog, undolog, errorlog, slowlog 로그 공간만 포함 |
| 로그 파일 사용 공간 | disk_log_used  | MB | MySQL binlog, relaylog, undolog, 로그 공간만 포함 |
| 임시 파일 사용 공간 | disk_tmp_used | MB | MySQL 실행 시 생성된 임시 파일만 포함 |
| 디스크 이용률      | volume_rate     | %         | 사용된 총 디스크 공간 / 인스턴스 구입 공간         |
| 내부 네트워크 아웃바운드 트래픽 | bytes_sent       | Byte/초 | 초당 전송 바이트 수 |
| 내부 네트워크 인바운드 트래픽 | bytes_received | Byte/초 | 초당 수신 바이트 수 |
| 캐시 히트율 조회 | qcache_hit_rate         | % | 캐시 히트율 조회 |
| 캐시 사용률 조회  | qcache_use_rate       | % | 캐시 사용률 조회 |
| 대기 테이블 잠금 횟수 | table_locks_waited | 회/초 | 즉시 획득할 수 없는 테이블의 잠금 횟수 |
| 임시 테이블 수량 | created_tmp_tables   | 회/초 | 생성된 임시 테이블 수량 |
| innodb 캐시 히트율 | innodb_cache_hit_rate  | % | Innodb 엔진의 캐시 히트율 |
| innodb 캐시 사용률 | innodb_cache_use_rate | % | Innodb 엔진의 캐시 사용률 |
| innodb 디스크 읽기 수 | innodb_os_file_reads    | 회/초 | Innodb 엔진이 초당 디스크 파일을 읽는 횟수 |
| innodb 디스크 쓰기 수 | innodb_os_file_writes   | 회/초 | Innodb 엔진이 초당 디스크 파일을 쓰는 횟수 |
| innodb fsync 수량  | innodb_os_fsyncs         | 회/초 | Innodb 엔진이 초당 fsync 함수를 호출하는 횟수 |
| 현재 Innodb에서 열린 테이블 수량 | innodb_num_open_files  | 개 | Innodb 엔진에서 현재 열린 테이블 수량|
| myisam 캐시 히트율  | key_cache_hit_rate  | %   | myisam 엔진의 캐시 히트율 |
| myisam 캐시 사용률  | key_cache_use_rate | %   | myisam 엔진의 캐시 사용률 |
| CPU 이용률              | cpu_use_rate            | %   | 유휴 시간 초과 사용 허용, CPU 이용률 100% 초과 가능 |
| 메모리 이용률               | memory use rate     | %   | 유휴 시간 초과 사용 허용, 메모리 이용률이 100%보다 클 수 있음  |
| 메모리 점유율               |memory_use       | MB | 유휴 시간 초과 사용 허용, 실제 메모리 점유율이 구매한 사양보다 클 수 있음 |
| 임시 파일 수량            | created_tmp_files    | 회/초 | 초당 임시 파일 생성 횟수 |
| 열려 있는 테이블 수        | opened_tables         | 개      | 인스턴스 차원|열려 있는 테이블 수 |
| 제출 수                    | com_commit            | 회/초 | 초당 제출 횟수 |
| 롤백 수                     | com_rollback           | 회/초 | 초당 롤백 횟수 |
| 생성된 스레드 수          | threads_created      | 개 | 연결을 처리하기 위해 생성된 스레드 수 |
| 실행된 스레드 수           | threads_running      | 개 | 활성화된(비수면 상태) 스레드 수 |
| 최대 연결 수                | max_connections    | 개 | 최대 연결 수 |
| 디스크 임시 테이블 수량      | created_tmp_disk_tables | 회/초 | 초당 임시 테이블 생성 횟수 |
| 다음 행 읽기 요청 수       | handler_read_rnd_next    | 회/초 | 초당 다음 행 읽기 요청 수 |
| 내부 롤백 수              | handler_rollback     | 회/초 | 초당 트랜잭션 롤백 횟수 |
| 내부 제출 수               | handler_commit     | 회/초 | 초당 트랜잭션 제출 횟수 |
| InnoDB 빈 페이지 수         | innodb_buffer_pool_pages_free    | 개  | Innodb 엔진 메모리의 빈 페이지 수  |
| InnoDB 총 페이지 수         | innodb_buffer_pool_pages_total  | 개  | Innodb 엔진이 점유한 메모리 총 페이지 수  |
| InnoDB 논리적 읽기        | innodb_buffer_pool_read_requests  | 회/초  | Innodb 엔진이 초당 완료한 논리적 읽기 요청 수  |
| InnoDB 물리적 읽기         | innodb_buffer_pool_reads  | 회/초  | Innodb 엔진이 초당 완료한 물리적 읽기 요청 수  |
| InnoDB 읽기 수          | innodb_data_read         | Byte/초  | Innodb 엔진이 초당 완료한 데이터 읽기 바이트 수  |
| InnoDB 총 읽기 수      | innodb_data_reads      | 회/초    | Innodb 엔진이 초당 완료한 데이터 읽기 횟수  |
| InnoDB 총 쓰기 수      | innodb_data_writes     | 회/초      | Innodb 엔진이 초당 완료한 데이터 쓰기 횟수  |
| InnoDB 쓰기 수         | innodb_data_written     | Byte/초    | Innodb 엔진이 초당 완료한 데이터 쓰기 바이트 수  |
| InnoDB 행 삭제 수      | innodb_rows_deleted   | 회/초  | Innodb 엔진이 초당 삭제한 행 수  |
| InnoDB 행 삽입 수      | innodb_rows_inserted  | 회/초  | Innodb 엔진이 초당 삽입한 행 수  |
| InnoDB 행 업데이트 수      | innodb_rows_updated  | 회/초  | Innodb 엔진이 초당 업데이트한 행 수  |
| InnoDB 행 읽기 수      | innodb_rows_read       | 회/초  | Innodb 엔진이 초당 읽은 행 수  |
| InnoDB 평균 행 잠금 획득 시간 | innodb_row_lock_time_avg  | 밀리초  | Innodb 엔진의 평균 행 잠금 시간  |
| InnoDB 행 잠금 대기 횟수      | innodb_row_lock_waits       | 회/초 | Innodb 엔진의 초당 행 잠금 대기 횟수  |
| 키 캐시 미사용 블록 수량   | key_blocks_unused              | 개     | myisam 엔진 미사용 키 캐시 블록 수  |
| 키 캐시 내 사용된 블록 수량      | key_blocks_used                  | 개     | myisam 엔진 사용된 키 캐시 블록 수  |
| 키 캐시 데이터 블록 읽기 횟수       | key_read_requests   | 회/초 | myisam 엔진의 초당 키 캐시 블록 읽기 횟수  |
| 디스크 데이터 블록 읽기 횟수         | key_reads                | 회/초 | myisam 엔진의 초당 디스크 데이터 블록 읽기 횟수|
| 키보드 버퍼에 데이터 블록 쓰기 횟수     | key_write_requests   | 회/초 | myisam 엔진의 초당 키 캐시 블록 쓰기 횟수|
| 데이터 블록 디스크 쓰기 횟수         | key_writes                | 회/초 | myisam 엔진 초당 디스크 데이터 블록 쓰기 횟수|
| 프라이머리/세컨더리 딜레이 거리     | master_slave_sync_distance  | MB | 프라이머리/세컨더리 binlog 거리  |
| 프라이머리/세컨더리 딜레이 시간     | seconds_behind_master        |초   | 프라이머리/세컨더리 딜레이 시간  |
| IO 스레드 상태       | slave_io_running   | 상태값(0-Yes, 1-No, 2-Connecting) | IO 스레드 실행 상태     |
| SQL 스레드 상태    |slave_sql_running  |상태값(0-Yes, 1-No)                      | SQL 스레드 실행 상태  |
