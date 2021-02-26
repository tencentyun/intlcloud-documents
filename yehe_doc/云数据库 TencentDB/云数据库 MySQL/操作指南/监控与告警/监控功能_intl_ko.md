TencentDB for MySQL은 사용자가 인스턴스 운용 정보 조회와 관리를 손쉽게 할 수 있도록 다양한 성능 모니터링 옵션과 간편한 모니터링 기능(사용자 정의 뷰, 시간 비교, 모니터링 항목 결합 등)을 제공합니다. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하면 인스턴스 관리 페이지에 접근하여 [인스턴스 모니터링]을 확인할 수 있습니다.
>?
>- Cloud Monitoring API의 [지표 모니터링 데이터 풀링](https://intl.cloud.tencent.com/document/product/248/33881), [TencentDB for MySQL 모니터링 지표](https://intl.cloud.tencent.com/document/product/248/11006)를 통해 인스턴스 모니터링 지표를 확인할 수 있습니다.
>- [ Dashboard를 생성](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10)을 통한 지표 모니터링 데이터의 동적 분석도 가능합니다.
>- 단일 인스턴스의 테이블 수량이 100만 개를 초과하면 데이터베이스 모니터링에 영향을 미칠 수 있으므로 테이블 수량을 합리적인 수준으로 적용하시고, 단일 인스턴스 테이블 수량이 100만 개를 넘지 않도록 제어하시기 바랍니다.

## 모니터링을 지원하는 인스턴스 유형
TencentDB for MySQL은 마스터 인스턴스, 읽기 전용 인스턴스 및 재해 복구 인스턴스를 지원하며, 각 인스턴스에 대한 독립적인 모니터링 이미지를 제공합니다.

## 모니터링 분류
TencentDB for MySQL의 모니터링 유형은 리소스 모니터링, 엔진 모니터링(일반), 엔진 모니터링(확장), 배포 모니터링의 4종으로 구분됩니다. 각 유형의 모니터링 지표를 이용하면 인스턴스 성능과 실행 상태를 빠르고 정확하게 파악할 수 있습니다.
- **리소스 모니터링**: CPU, 메모리, 디스크 및 네트워크 관련 모니터링 데이터를 제공합니다.
- **엔진 모니터링(일반)**: 연결 수, lock 정보, 핫스팟 테이블, 슬로우 쿼리 등과 관련된 모니터링 데이터를 제공하여 편리하게 장애 진단과 성능 최적화를 진행할 수 있도록 합니다.
- **엔진 모니터링(확장)**: 다양한 엔진 관련 모니터링 지표를 제공하여 데이터베이스에 존재하거나 잠재하는 문제를 최대한도로 탐지할 수 있도록 합니다.
- **배포 모니터링**: 마스터/슬레이브 딜레이와 관련된 모니터링 지표를 제공합니다. 배포 모니터링은 CVM과 슬레이브로 구분됩니다.
 - 배포 모니터링 for CVM: 모니터링 인스턴스가 마스터 인스턴스일 경우, 해당 마스터 인스턴스는 어떠한 인스턴스의 슬레이브 인스턴스도 아니므로 해당 CVM에서의 복사 관련 모니터링 데이터는 유효하지 않습니다. 이때 IO, SQL 스레드는 미실행 상태입니다. 오직 모니터링 인스턴스가 재해 복구 인스턴스와 읽기 전용 인스턴스일 경우에만 복사 관련 모니터링 데이터가 유효하며, IO, SQL 스레드는 실행 상태가 됩니다.
 
 - 배포 모니터링 for 슬레이브: 고가용 버전과 파이낸스 버전의 마스터 인스턴스와 재해 복구 인스턴스의 기본 설정은 마스터/슬레이브 아키텍처이므로, 모니터링 인스턴스가 마스터 인스턴스 또는 재해 복구 인스턴스일 경우에만 해당 슬레이브에서의 복사 관련 모니터링 데이터가 유효합니다. 마스터 인스턴스, 재해 복구 인스턴스를 숨겨진 백업 노드의 지연 거리 또는 시간에 반영할 경우에는 슬레이브 내 관련 데이터에 유의하시기 바랍니다. 마스터 인스턴스 또는 재해 복구 인스턴스에 장애가 있을 경우, 모니터링 인스턴스의 숨겨진 백업 노드를 빠르게 마스터 인스턴스로 승격할 수 있습니다.
 
![](https://main.qcloudimg.com/raw/183cebeb93cdeaca2dedeb228ab8f0be.png)

## 모니터링 간격
2018년 08월 11일부로 TencentDB for MySQL 모니터링 간격에 자가 적응 정책이 적용되어 일시적으로 모니터링 데이터 분할 정도의 사용자 정의 선택이 지원되지 않습니다. 모니터링 데이터 분할 정도 자가 적응 정책은 다음과 같습니다.

| 시간 간격 | 모니터링 간격 | 자가 적응 설명 | 보관 기간 |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5s | 시간 범위는 4시간 이내, 모니터링 간격은 5초 | 1일 |
| (4h, 2d] | 1min | 시간 범위는 4시간 이내이나 2일 내 모니터링 간격은 1분으로 조정 | 15일 |
| (2d, 10d] | 5min | 시간 범위는 2일 이내이나 10일 내 모니터링 간격은 5분으로 조정 | 31일 |
| (10d, 30d] | 1h | 시간 범위는 10일 이내이나 30일 내 모니터링 간격은 1시간으로 조정 | 62일 |

>? 현재 TencentDB for MySQL은 최장 30일 내의 모니터링 데이터 조회를 지원합니다.



## 모니터링 지표
Tencent Cloud 클라우드 모니터링은 인스턴스 차원에서부터 TencentDB for MySQL 인스턴스에 다음 모니터링 지표를 제공합니다.

>? 더 많은 CDB 모니터링 지표 사용 방법 사용 방법은 Cloud Monitoring API의 [TencentDB for MySQL 인터페이스](https://intl.cloud.tencent.com/document/product/248/11006)를 참조 바랍니다.

| 지표 중문명 | 지표 영문명 | 단위 |지표 설명|
|---------|---------|---------|---------|
|초당 실행하는 작업 수|qps|회/초|데이터베이스가 초당 실행하는 SQL 수( insert, select, update, delete, replace 등), QPS 지표는 주로 TencentDB 인스턴스의 실제 프로세스를 구현함|
|초당 실행하는 비즈니스 수| tps |회/초|데이터베이스가 초당 전송하는 비즈니스 프로세스 개수|
|슬로우 쿼리 수|slow_queries|회|조회 시간 초과 long_query_time 초의 조회 개수|
|전체 테이블 스캔 수|select_scan|회/초|전체 테이블 검색 조회 실행 수|
|조회 수|select_count|회/초|초당 조회 수|
|업데이트 수|com_update|회/수|초당 업데이트 수|
|삭제 수|com_delete|회/초|초당 삭제 수|
|삽입 수|com_insert|회/초|초당 삽입 수|
|덮어쓰기 수|com_replace|회/초|초당 덮어쓰기 수|
|총 요청 수|queries|회/초|모든 실행한 SQL 명령, set, show 등|
|현재 열린 연결 수|threads_connected|개|현재 열린 연결 수량|
|연결 수 이용률|connection_use_rate|%|현재 열린 연결 수/최대 연결 수   |
|쿼리 사용률|query_rate|%|초당 실행된 작업 수 QPS/추천 초당 작업 수|
|디스크 사용 공간|real_capacity|MB|MySQL 데이터 목록만 포함, binlog, relaylog, undolog, errorlog, slowlog 로그 용량은 제외|
|디스크 점유 공간|capacity|MB|MySQL 데이터 목록 및 binlog, relaylog, undolog, errorlog, slowlog 로그 용량 포함|
|내부 네트워크 아웃바운드 트래픽|bytes_sent|Byte/초|초당 보내는 바이트 수|
|내부 네트워크 인바운드 트래픽|bytes_received|Byte/초|초당 받는 바이트 수|
|디스크 이용률|volume_rate|%|디스크 사용 용량/인스턴스 구매 용량|
|캐시 조회 히트율|qcache_hit_rate|%|캐시 조회 히트율|
|캐시 조회 사용률|qcache_use_rate|%|캐시 조회 사용률|
|대기 테이블 잠근 횟수|table_locks_waited|회/초|즉시 획득할 수 없는 테이블의 잠금 횟수|
|임시 테이블 수량|created_tmp_tables|회/수|생성된 임시 테이블의 수량|
|innodb 캐시 히트율|innodb_cache_hit_rate|%|Innodb 엔진의 캐시 히트율|
|innodb 캐시 사용률|innodb_cache_use_rate|%|Innodb 엔진의 캐시 사용률|
|innodb 읽기 디스크 수량|innodb_os_file_reads|회/초|Innodb 엔진 초당 읽기 디스크 수량|
|innodb 쓰기 디스크 수량|innodb_os_file_writes|회/초|Innodb 엔진 초당 쓰기 디스크 수량|
|innodb fsync 수량|innodb_os_fsyncs|회/초|Innodb 엔진 초당 호출 fsync 함수 횟수|
|현재 Innodb 열린 테이블 수량 |innodb_num_open_files|개| Innodb 엔진 현재 열린 테이블 수량|
|myisam 캐시 히트율|key_cache_hit_rate|%|myisam 엔진의 캐시 히트율|
|myisam 캐시 사용률|key_cache_use_rate|%|myisam 엔진의 캐시 사용률|
|CPU 이용률|cpu_use_rate|%|유휴 초과 사용을 허용하여 CPU 이용률이 100% 이상이 될 수 있음|
|메모리 이용률|memory use rate| %|유휴 초과 사용을 허용하여 메모리 이용률이 100% 이상이 될 수 있음|
|메모리 점유|memory_use|MB|유휴 초과 사용을 허용하여 실제 메모리 점용이 구매 스펙보다 높을 수 있음|
|임시 파일 수량|created_tmp_files|회/초|초당 임시 파일 생성 횟수|
|이미 열린 테이블 수|opened_tables|개|인스턴스 차원|이미 열린 테이블 개수|
|제출 수|com_commit|회/수|초당 제출 횟수|
|롤백 수|com_rollback|회/초|초당 롤백 횟수|
|이미 생성된 스레드 수|threads_created|개|연결을 처리하기 위해 생성된 스레드 수|
|실행된 스레드 수|threads_running|개|활성화된(비수면 상태) 스레드 수|
|최대 연결 수|max_connections|개|최대 연결 수|
|디스크 임시 테이블 수량|created_tmp_disk_tables|회/초|초당 디스크 임시 테이블 생성 횟수|
|다음 행 읽기 요청 수|handler_read_rnd_next|회/초|초당 다음 행 읽기 요청 횟수|
|내부 롤백 수|handler_rollback|회/초|초당 트랜잭션 롤백 횟수|
|내부 제출 수|handler_commit|회/초|초당 트랜잭션 제출 횟수|
|InnoDB 빈 페이지 수|innodb_buffer_pool_pages_free|개|Innodb 엔진 메모리 빈 페이지 수|
|InnoDB 총 페이지 수|innodb_buffer_pool_pages_total|개|Innodb 엔진 점유 메모리 총 페이지 수|
|InnoDB 논리적 읽기|innodb_buffer_pool_read_requests|회/초|Innodb 엔진이 완료한 초당 논리적 읽기 요청 횟수|
|InnoDB 물리적 읽기|innodb_buffer_pool_reads|회/초|Innodb 엔진이 완료한 초당 물리적 읽기 요청 횟수|
|InnoDB 읽기 수|innodb_data_read|Byte/초|Innodb 엔진이 완료한 초당 데이터 읽기 바이트 수|
|InnoDB 총 읽기 수|innodb_data_reads|회/초|Innodb 엔진이 완료한 초당 데이터 읽기 횟수|
|InnoDB 총 쓰기 수|innodb_data_writes|회/초|Innodb 엔진이 완료한 초당 데이터 쓰기 횟수|
|InnoDB 쓰기 수|innodb_data_written|Byte/초|Innodb 엔진이 완료한 초당 데이터 쓰기 바이트 수|
|InnoDB 행 삭제 수|innodb_rows_deleted|회/초|Innodb 엔진 초당 삭제 행수|
|InnoDB 행 삽입 수|innodb_rows_inserted|회/초|Innodb 엔진 초당 삽입 행수|
|InnoDB 행 업데이트 수|innodb_rows_updated|회/초|Innodb 엔진 초당 업데이트 행수|
|InnoDB 행 읽기 수|innodb_rows_read|회/초|Innodb 엔진 초당 읽은 행수|
|InnoDB 평균 행 잠금 획득 시간|innodb_row_lock_time_avg|밀리세컨드|Innodb 엔진 행 잠금 평균 시간|
|InnoDB 행 잠금 대기 수|innodb_row_lock_waits|회/초|Innodb 엔진 초당 행 잠금 대기 수|
|키 캐시 내 사용하지 않은 블록 수량|key_blocks_unused|개|myisam 엔진이 사용하지 않은 키 캐시 모듈 개수|
|키 캐시 내 사용한 블록 수량|key_blocks_used|개|myisam 엔진이 사용한 키 캐시 모듈 개수|
|키 캐시 읽기 디스크 블록 횟수|key_read_requests|회/초|myisam 엔진 초당 키 캐시 모듈 읽기 횟수|
|디스크 읽기 디스크 블록 횟수|key_reads|회/초|myisam 엔진 초당 디스크 데이터 모듈 읽기 횟수|
|키보드 버퍼에 데이터 블록 쓰기 수|key_write_requests|회/초|myisam 엔진 초당 키 캐시 모듈 쓰기 횟수|
|데이터 블록이 디스크에 쓰기 횟수|key_writes|회/초|myisam 엔진 초당 디스크 데이터 블록 쓰기 횟수|
|마스터/슬레이브 지연 거리|master_slave_sync_distance|MB|마스터/슬레이브 binlog 거리|
|마스터/슬레이브 지연 시간|	seconds_behind_master|	초|마스터/슬레이브 지연 시간|
|IO 스레드 상태|	slave_io_running|	상태값(0-Yes, 1-No, 2-Connecting)|IO 스레드 실행 상태|
|SQL 스레드 상태|	slave_sql_running|	상태값(0-Yes, 1-No)|SQL 스레드 실행 상태|
