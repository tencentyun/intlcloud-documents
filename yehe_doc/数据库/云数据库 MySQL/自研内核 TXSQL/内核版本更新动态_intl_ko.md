본 문서에서는 MySQL 커널 버전 업데이트 동향에 대해 소개합니다. 업그레이드 하려면 [커널 마이너 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/36816)를 참고하십시오.

## MySQL 8.0
### 20220331

#### bug 수정:

- 스레드 풀(Thread Pool)에서 와일드 포인터의 역참조로 인한 crash 문제 수정.

### 20220330

#### 새로운 기능:

- 기본적으로 writeset 병렬 복사가 열려 있습니다.
- IO, 메모리 사용 비율 및 SQL 시간 초과 정책을 사용자 단위로 제어할 수 있는 확장된 리소스 그룹을 지원합니다.
- UNDO 시간 범위 내에서 언제든지 데이터를 쿼리할 수 있는 플래시백 쿼리 기능을 지원합니다.
- 이 statment에 의해 작동되는 데이터 행을 반환할 수 있는 delete/insert/replace/update의 returning 구문을 지원합니다.
- row 모드 gtid 복제 기능 확장을 지원합니다.
- 트랜잭션 잠금 최적화 기능을 지원합니다.
- 휴지통 향상, 휴지통에서 truncate table과 테이블 자동 정리를 지원합니다.
- parallel ddl 기능을 지원하여 3단계 병렬 처리를 통해 인덱스를 생성해야 하는 DDL 작업의 속도를 높였습니다.
- 인덱스 컬럼을 빠르게 수정하는 기능을 지원합니다.
- 자동 통계 수집 및 교차 시스템 통계 수집을 지원합니다.

#### 성능 최적화:

- binlog_order_commits 비활성화 시 트랜잭션이 제출될 때 gtid에 대한 잠금 충돌이 최적화되었습니다.
- InnoDB 실행 단계를 rseg의 단일 스레드 생성에서 멀티 스레드 생성으로 변경하여 MySQL 실행 시간을 최적화했습니다.

#### bug 수정:

- 교착 상태 또는 잠금 대기 후 연결이 끊어지면 트랜잭션이 종료되지 않는 문제 수정.
- innodb_row_lock_current_waits 등의 비정상적인 통계 수정.
- 감사 플러그 인 use database에 sql type이 없는 오류 수정.
- 큰 테이블의 비동기 삭제 기능에서 innodb_async_table_size보다 작은 테이블이 rename되는 문제 수정.
- 감사 플러그 인에서 잘못된 이스케이프 문자가 있는 오류 수정.
- 열을 빠르게 수정한 후 롤백되는 문제 수정.
- trx_sys close 시 xa가 있는 시나리오가 crash할 수 있는 문제 수정.
- merge derived table 시 발생하는 crash 수정.
- writeset이 활성화된 후 binlog_format을 수정하는 문제 수정.
- hash scan이 동일한 행에서 A->B->A->C를 업데이트할 때 발생하는 1032 문제 수정.
- Prepared Statement 모드에서 정렬 인덱스가 유효하지 않을 수 있는 문제 수정.
- 구체화된 결과를 소비하는 연산자는 구체화된 연산자의 반환 값 경로에 병합되어 실행 계획 이해 및 표시에 오류가 발생할 수 있는 문제 수정.
- 큰 테이블의 비동기식 삭제로 극단적인 상황의 비정상 동작 수정.
- sql filter 설정 시 비정상적인 오류 메시지가 발생하는 문제 수정.
- 저장 프로시저 구문 분석 오류의 문제 수정.
- 히스토그램 적용 불가 문제 수정.
- SHOW SLAVE HOSTS(show replicas)의 Role 열 표시로 인한 호환성 문제 수정.
- Item_in_subselect::single_value_transformer가 열 수에 오류가 있는 경우 crash 문제 수정.
- 서브 테이블의 virtual column과 외래 키 열, 캐스케이드 업데이트 과정에서 메모리 유출로 인한 인스턴스 crash 문제 수정.


### 20211202
#### 새로운 기능:
- 빠른 열 수정 기능을 지원합니다.
- 히스토그램 이전 버전 기능을 지원합니다.
- 물리적 테이블의 무작위 샘플을 얻기 위한 SQL2003 TABLESAMPLE(단일 테이블) 샘플링 제어 구문을 지원합니다.
- 보관되지 않은 키워드 추가: TABLESAMPLE BERNOULLI.
- 주어진 입력 필드에 대한 히스토그램을 작성하기 위해 HISTOGRAM() 함수를 추가했습니다.
- compressed 히스토그램 지원합니다.
- SQL throttling 기능 지원(DBbrian은 2022년 04월 지원 예정).
- MySQL 클러스터 역할 설정 기능을 지원하며 기본 역할은 CDB_ROLE_UNKNOWN입니다.
- 역할을 표시하기 위해 show replicas 명령의 표시 결과에 새로운 Role 열이 추가되었습니다.
- proxy를 지원합니다.

#### 성능 최적화:
- insert on duplicate key update로 인한 핫스팟 업데이트 문제를 최적화했습니다.
- event 같은 여러 개의 동일한 binlog event를 집계하여 hash scan의 애플리케이션 속도를 향상시켰습니다.
- plan cache가 열린 상태에서 스레드 풀(Thread Pool) 모드에서 prepare 명령의 메모리를 대폭 줄였습니다.

#### Bug 수정:
- 핫스팟 업데이트 최적화를 켠 후 성능이 불안정한 문제 수정.
- 'select count(*)' 병렬 스캔이 극단적인 경우 전체 테이블을 스캔하는 문제 수정.
- 다양한 경우에 통계 정보 0 읽기로 인한 실행 계획 변경으로 발생하는 성능 문제 수정.
- query가 오랫동안 query end 상태인 bug 수정.
- 긴 기록에서 통계 정보가 심각하게 과소평가되는 bug 수정.
- Temptable 엔진 사용 시 선택한 열의 집계 함수가 255를 초과하여 오류가 보고되는 bug 수정.
- json_table 함수에서 열 이름의 대소문자 구분 문제 수정.
- return true 시 표현식이 일찍 반환되어 윈도우 함수에서 정확성 문제를 일으키는 bug 수정.
- derived condition pushdown이 user variables를 포함할 때 발생하는 정확성 문제 수정.
- Rule 규칙이 namespace를 추가하지 않을 때 SQL filter가 crash하기 쉬운 문제 수정.
- 높은 동시성과 높은 충돌의 경우 스레드 풀(Thread Pool)을 여는 QPS 지터 수정.
- 프라이머리/세컨더리 bp 동기화가 극단적인 상황에서(호스트 파일 시스템 손상) 파일 핸들을 유출하는 문제 수정
- index mapping 문제 수정.
- 통계 정보 캐시 동기화 문제 수정.
- 정보를 지우지 않고 update 명령 또는 스토리지 프로시저의 이식 실행으로 인해 발생하는 crash 문제 수정.

### 20210830
#### 새로운 기능:
- 사전 로딩 라인 제한 기능을 지원합니다.
- 플랜 캐시 체크 최적화 기능을 지원합니다.
- 확장된 ANALYZE 구문(UPDATE HISTOGRAM c USING DATA 'json')을 지원하고 히스토그램을 직접 작성하는 기능을 지원합니다.

#### 성능 최적화:
- 인덱스 다운 대신 히스토그램을 사용하여 평가 오류 및 I/O 오버헤드를 줄입니다. 이 기능은 기본적으로 활성화되어 있지 않습니다.

#### Bug 수정:
- online-DDL 시 통계 정보가 0이 되는 현상 수정.
- 세컨더리의 generated column이 업데이트 되지 않는 현상 수정.
- binlog 압축 시 인스턴스 hang 문제 수정.
- 새로 생성된 binlog 파일의 previous_gtids event에서 gtid가 누락되는 문제 수정.
- 시스템 변수를 수정할 때 교착 상태가 발생할 수 있는 문제 수정.
- show processlist의 slave sql 스레드 info가 잘못 표시되는 문제 수정.
- 공식 8.0.23에서 hash join 관련 bugfix 이식.
- 공식 writeset 관련 bugfix 이식.
- 공식 8.0.24에서 쿼리 최적화 프로그램과 관련된 bugfix 이식.
- FAST DDL에서 flush list를 최적화하고 페이지 동시성을 해제하는 bug 수정.
- 데이터 사전을 업그레이드 시 많은 수의 테이블이 있는 인스턴스 대량 메모리 점유 문제 최적화.
- instant add column 후 새 기본 키를 생성할 때 발생하는 crash 문제 수정.
- 전체 텍스트 인덱스 쿼리에서 메모리 증가로 인해 발생하는 OOM 문제 수정.
- show processlist에 의해 반환된 결과 집합의 TIME 필드 -1 문제 수정.
- 히스토그램 호환성으로 인해 테이블이 열리지 않는 문제 수정.
- Singleton 히스토그램 생성 시 부동 소수점 누적 오류 수정.
- row 형식 로그의 테이블 이름에 긴 중국어 문자로 인해 복제가 중단되는 문제 수정.

### 20210330
#### 새로운 기능:
- 프라이머리/세컨더리 bp 동기화 기능 지원: HA가 발생하고 프라이머리/세컨더리 전환이 수행될 때 대기 데이터베이스는 일반적으로 buffer pool에 핫스팟 데이터를 warmup하고 로드하는 데 비교적 오랜 시간이 걸립니다. 대기 머신의 워밍업 속도를 높이기 위해 TXSQL은 프라이머리/세컨더리 bp 동기화 기능을 지원합니다.
- Sort Merge Join 기능을 지원합니다.
- FAST DDL 기능을 지원합니다.
- 사용자측 character_set_client_handshake 매개변수 쿼리를 통한 현재 값 표시 기능을 지원합니다.

#### 성능 최적화:
- 스캐닝 flush list 플러싱 최적화: 플러시 메커니즘을 최적화하여 인덱스 생성 프로세스의 성능 지터 문제를 해결하고 시스템 안정성을 개선하였습니다.

#### bug 수정:
- offline_mode 및 cdb_working_mode의 매개변수 수정 시 교착 상태 문제 수정.
- trx_sys의 max_trx_id의 동시성 문제 수정.

### 20201230
#### 새로운 기능:
- 공식 [8.0.19](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-19.html), [8.0.20](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-20.html), [8.0.21](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-21.html), [8.0.22](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-22.html) 변경 사항을 병합하였습니다.
- thread_handling 스레드 모드 또는 연결 풀 모드 동적 설정을 지원합니다.

#### 성능 최적화:
- BINLOG LOCK_done 락 충돌 최적화로 쓰기 성능을 향상시켰습니다.
- Lock Free Hash를 사용해 trx_sys mutex 충돌을 최적화하여 성능을 향상시켰습니다.
- redo log 플러시를 최적화하였습니다.
- buffer pool 초기화 시간을 최적화하였습니다.
- 대용량 테이블 drop table의 AHI 정리를 최적화하였습니다.
- 감사 성능을 최적화하였습니다.

#### bug 수정:
- innodb 임시 테이블 정리 시 성능 지터 발생 문제 수정.
- 코어 수가 많은 인스턴스의 read only 성능 저하 문제 수정.
- hash scan으로 인한 1032 발생 문제 수정.
- 핫스팟 업데이트 기능의 동시 접속 보안 문제 수정.

### 20200630
#### 새로운 기능:
- 비동기화 시 대용량 테이블 삭제 지원: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 유휴 작업을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 투명한 데이터 암호화 기능을 지원합니다.

#### bug 수정:
- relay_log_pos & master_log_pos 위치 불일치로 인한 교체 실패 문제 수정.
- 비동기화 디스크 저장으로 인한 데이터 파일 오류 문제 수정.
- fsync에서 EIO 리턴 시 반복적으로 무한 루프에 빠지려 하는 문제 수정.
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 있었던 crash 문제 수정.

## MySQL 5.7
### 20211230

#### 새로운 기능:

- 공식 [5.7.19](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-19.html)에서 [5.7.36](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-36.html)의 변경 사항을 병합하였습니다.
- 프라이머리/세컨더리 buffer pool이 동기화되어 HA 이후 성능 회복 속도가 빨라지고, 성능 회복 속도는 네이티브 모드에 비해 약 90초 정도 감소하였습니다.
- 백업 중 서비스 가용성을 향상시키기 위해 경량화된 메타데이터 잠금을 제공하는 backup lock 기능을 추가했습니다.

#### 성능 최적화:

- 인라인 utf8/utf8mb4 my_charpos 관련 함수는 read_write 시나리오에서 UTF_8 관련 함수의 성능을 최적화하였습니다.
- jemalloc 버전을 5.2.1로 업그레이드하였습니다.
- binlog rotate 시 파일 번호 가져오기를 최적화하였습니다.
- 반동기식 slave io를 최적화하였습니다.
- hash scan 집계를 최적화하였습니다.
- 대규모 트랜잭션 crash recover 실행 시간을 최적화하였습니다.

### 20211102
#### 새로운 기능:
- 타사 데이터 구독 툴 사용 시 내부 데이터 일관성 비교 SQL 구독으로 인해 데이터 구독 툴이 비정상적이었던 문제를 해결했습니다.
>?데이터베이스 인스턴스가 마이그레이션, 업그레이드 또는 장애 복구 후 시스템은 데이터 일관성을 보장하기 위해 데이터 일관성 비교를 수행합니다. 데이터베이스 비교 SQL은 'statement' 모드이며 일부 타사 구독 툴에서 'statement' 모드 SQL을 처리하면 이상 경고가 발생하기 쉽습니다. 이 버전의 커널로 업그레이드한 후 타사 구독 툴은 내부 데이터 일관성 비교 SQL을 구독하지 않습니다.

### 20211031
#### 새로운 기능:
- writeset 복사 기능을 지원합니다.

#### 성능 최적화:
- checkpoint를 수동으로 진행하여 백업 성공률을 높였습니다.
- hash scan 인덱스 선택을 최적화했습니다.
- 핫스팟 업데이트 성능 최적화로 insert on duplicate key update를 지원합니다.

#### Bug 수정:
- 핫스팟 업데이트를 켠 후 성능이 불안정한 문제 수정.
- instant ddl 이후 update 작업 롤백 시 발생하는 crash 문제 수정.
- 컬럼 압축 활성화 후 create table select 명령이 압축 속성을 상속하지 않는 문제 수정.
- skip-grant-table 옵션 활성화 후 show variables like 'tencent_root%’ 명령으로 인해 인스턴스 crash가 발생하는 문제 수정.
- read only 모드에서의 Query Rewriter 플러그인 crash 문제 수정.
- 파티션 테이블에서 hash scan의 1032 문제 수정.
- mts 모드에서 첫 번째 큰 트랜잭션 sbm이 0인 문제 수정.
- slave_preserve_commit_order=ON 및 slave_transaction_retries=0일 때 stop slave 랙 문제 수정.
- 여러 XA 트랜잭션 bug 수정.
- default 값을 가진 json 필드를 생성한 후 show create 시 SQL을 어셈블하는 오류 수정.
- 트랜잭션이 차단된 후 연결이 끊긴 트랜잭션을 롤백할 수 없는 문제 수정.
- innodb persistent 모드의 통계가 긴 레코드에서 0이 될 수 있는 문제 수정.
- 8.0을 이식하여 ANALYZE TABLE이 쿼리 힙을 유발할 수 있는 문제 수정.
- 변경 후 Server 계층에 innodb 통계를 제때 동기화할 수 없는 문제 수정.
- 통계 샘플링이 너무 오랫동안 쓰기를 차단하고 크래쉬를 일으킬 수 있는 문제 수정(Bug#31889883).
- 0을 읽을 수 있는 innodb 통계 업데이트 프로세스 수정(BUG#105224).
- MVCC에 복잡도가 O(N^2)인 동작 수정(Bug#28825617).
- 연결 해제 시 임시 테이블을 닫으면 binlog rotate를 트리거하여 crash가 발생하는 문제 수정.

### 20210630
#### 새로운 기능:
- slave가 재생한 binlog 타임스탬프를 표시하는 데 사용되는 새로운 명령 SHOW SLAVE DETAIL [FOR CHANNEL channel]을 추가했습니다.
- transaction_read_only/transaction_isolation 매개변수를 지원합니다.

#### 성능 최적화:
- hash scan의 애플리케이션 속도 최적화: slave 측에서 hash scan의 애플리케이션 속도는 event의 여러 동일한 binlog event를 집계하여 향상시켰습니다.

#### Bug 수정:
- 기본 키 중복, 열을 찾을 수 없는 문제, 업데이트 명령에 의해 트리거된 임시 테이블의 열 길이 문제 수정.
- DDL 과정에서 통계 정보가 0이 될 수 있는 문제 수정.
- 연결 상태 통계에서 정확하지 않은 undo log size 통계 문제 수정.
- Metadata_locks 테이블 쿼리 시 인스턴스 crash 문제 수정.
- of를 예약어가 아닌 키워드로 수정.
- 동적으로 수정된 버전 번호가 새 연결에서 유효하지 않은 문제 수정.
- 와일드 포인터에 대한 page_cache cleanning 액세스 문제 수정.
- alter table 명령을 실행하면 ‘Incorrect key file for table’ 오류가 보고되는 문제 수정.
- 파티션 테이블이 메모리를 과도히 사용하는 문제 수정.
- show processlist에 의해 반환된 결과 집합의 TIME 필드 -1 문제 수정.
- slave 노드에서 XA 트랜잭션 복제 잠금 대기 문제 수정.
- 파티션 테이블 equal range 쿼리 시 잘못된 잠금 문제 수정.

### 20210331
#### 새로운 기능:
- delete/insert/replace의 returning 명령이 지원되며, 해당 statment에서 작동하는 데이터 행을 반환할 수 있습니다. 이 중 delete 명령은 사전 미러링 이미지 데이터를 반환하고, insert/replace는 사후 미러링 이미지 데이터를 반환합니다.
- 컬럼 압축 기능 지원: 현재 행 형식에 대한 압축과 데이터 페이지에 대한 압축이 있지만 이 두 가지 압축 방법은 테이블의 일부 큰 필드와 기타 여러 작은 필드를 처리합니다. 동시에 작은 필드는 매우 자주 읽고 쓰는데, 큰 필드에 드물게 액세스하는 경우, 읽기 및 쓰기 액세스로 인해 컴퓨팅 리소스가 불필요하게 많이 낭비됩니다. 열 압축은 자주 액세스하지 않는 큰 필드를 압축하는 동시에 전체 필드 행의 저장 공간을 줄이고 읽기 및 쓰기 액세스의 효율성을 향상시킬 수 있습니다.
- 사용자측 character_set_client_handshake 매개변수 쿼리를 통한 현재 값 표시 기능을 지원합니다.
- 로그 파일이 차지하는 page cache 능동적 정리 지원: 이 기능은 슬라이딩 창 방식으로 posix_fadvise를 통해 로그 파일이 차지하는 page cache를 능동적으로 정리하여 운영 체제 메모리 압력을 줄이고 전체 시스템의 안정성을 향상시켰습니다.

#### 성능 최적화:
- CREATE INDEX 병렬화: CREATE INDEX 프로세스는 외부 병합 정렬을 수행해야 하므로 시간이 많이 걸립니다. 병렬 외부 병합 정렬 알고리즘을 도입하여 CREATE INDEX 소요시간을 50% 이상 축소했습니다.
- 스캐닝 flush list 플러싱 최적화: 플러시 메커니즘을 최적화하여 인덱스 생성 프로세스의 성능 지터 문제를 해결하고 시스템 안정성을 개선하였습니다.

#### bug 수정:
- 메모리 누수 문제 수정.
- json 사용의 안정성을 향상시키기 위해 json 버전 8.0의 수정 사항 이식.
- hash scan으로 인한 1032 발생 문제 수정.
- 핫스팟 업데이트 기능의 동시 접속 보안 문제 수정.
- 일괄 이식 공식 홈페이지 gcol bug 수정.
- 일부 시나리오에서 datetime 유형이 문자열과 비교되지 않는 문제 수정.
- 프라이머리-세컨더리 bp 동기화 기능의 파일 핸들이 해제되지 않는 bug 수정.
- offline_mode 설정과 동시에 새 연결이 생성되어 트리거되는 교착 상태 bug 수정.
- 동시 범위 쿼리 시나리오에서 m_end_range의 잘못된 설정으로 인해 발생하는 crash 문제 수정.
- groupby json 필드의 temporay table update 시간이 오래 걸리는 문제 수정.

### 20201231
#### 새로운 기능:
- SELECT FOR UPDATE/SHARE에서 NOWAIT 및 SKIP LOCKED 옵션 사용을 지원합니다.
- thread_handling 스레드 모드 또는 연결 풀 모드 동적 설정을 지원합니다.
- 프라이머리/세컨더리 buffer pool 동기화 기능을 지원합니다.
- 사용자 연결 상태 모니터링 기능의 모니터링 항목: 동기/비동기 IO, 메모리, 로그 양, CPU 시간, 점유 시간 락(Lock) 등 포함.

#### 성능 최적화:
- 트랜잭션 서브 시스템 최적화로 동시 접속 성능을 향상시켰습니다.
- 대규모 트랜잭션 crash recover 실행 시간을 최적화하였습니다.
- redo log 플러시를 최적화하였습니다.
- buffer pool 초기화 시간을 최적화하였습니다.
- utf8/utf8mb4 문자열 효율을 최적화하였습니다.
- 감사 성능을 최적화하였습니다.
- gtid_purged를 반드시 null로 설정해야 하는 제한을 삭제하였습니다.
- 백업 락(Lock) 최적화: LOCK TABLES FOR BACKUP, LOCK BINLOG FOR BACKUP, UNLOCK BINLOG 3개의 신규 SQL 명령어를 도입하였습니다. FLUSH TABLES WITH READ LOCK의 백업 락 방식은 전체 데이터베이스에 서비스 제공이 불가능하지만, 해당 3개 명령어는 데이터베이스에 대한 경량급 락 백업을 위해 백업 과정에서의 데이터 액세스를 지원합니다. 물리 백업이나 로직 백업 상관없이 해당 명령어를 사용해 백업의 일관성 구현이 가능합니다.
- 대용량 테이블의 drop table을 최적화하였습니다.

#### bug 수정:
- performance_schema 쿼리 시 hang되는 문제 수정.
- digest_add_token 함수 내의 overflow 문제 수정.
- MySQL 공식 홈페이지 truncate table 시 ibuf 액세스로 인한 crash 문제 수정.
- left join 명령어에서 const 사전 계산으로 인한 쿼리 정확성 문제 수정.

### 20200930
#### 성능 최적화:
- 백업 락을 최적화하였습니다. 
FLUSH TABLES WITH READ LOCK의 백업 락 방식으로 인해 전체 데이터베이스에 서비스 제공이 불가능하며, 이 버전에서는 데이터베이스에 대한 경량급 락 백업 방식을 제공합니다.
- 대용량 테이블의 drop table을 최적화하였습니다. 
신속한 어댑티브 해시 정리의 최적화(innodb_fast_ahi_cleanup_for_drop_table 제어)로 대용량 테이블 drop 시 어댑티브 해시 인덱스 정리 소모 시간 대폭 단축이 가능해졌습니다.

#### bug 수정:
- MySQL 공식 홈페이지 truncate table 시 ibuf 액세스로 인한 crash 문제 수정.
- 빠른 컬럼 추가 후 콜드 스탠바이로 풀링할 수 없는 문제 수정.
- innodb 메모리 테이블 객체의 빈번한 릴리스로 성능이 저하되는 문제 수정.
- left join 명령어에서 const 사전 계산으로 인한 쿼리 정확성 문제 수정.
- sql 제한 및 query rewrite 플러그 인에 Rule 클래스 이름 충돌로 core가 발생하는 문제 수정.
- 여러 session에서 insert on duplicate key update 명령어의 동시 업데이트 문제 수정.
- auto_increment_increment 동시 삽입 시 duplicate key error 실패가 발생하는 문제 수정.
- innodb 메모리 객체가 제거되어 시스템이 다운되는 문제 수정.
- 핫스팟 업데이트 기능의 동시 접속 보안 문제 수정.
- jemalloc 5.2.1 버전으로 업데이트 시 스레드 풀 활성화로 coredump가 트리거되는 문제 수정.
- fwrite 처리 오류가 없을 때 감사 로그가 불완전한 문제 수정.
- mysqld_safe를 root 사용자로 실행할 때 로그가 출력되지 않는 문제 수정.
- alter table exchange partition으로 인한 ddl log 파일 증가 문제 수정.

### 20200701
#### bug 수정:
- INNOBASE_SHARE index mapping 오류 문제 수정.

### 20200630
#### 새로운 기능:
- SELECT FOR UPDATE/SHARE 명령어의 NOWAIT 및 SKIP LOCKED 옵션 사용을 지원합니다.
- 대용량 트랜잭션 최적화 기능 지원을 통해 대용량 트랜잭션으로 인한 프라이머리/세컨더리 딜레이, 백업 실패 등 문제를 개선하였습니다.
- 감사 성능 최적화: 비동기 감사 기능을 지원합니다.

#### bug 수정:
- digest_add_token 함수 내의 오버플로우 문제 수정.
- insert blob으로 인한 인스턴스 crash 문제 수정.
- event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 프라이머리/세컨더리가 중단되는 문제 수정.
- performance_schema 쿼리 시 hang되는 문제 수정.

### 20200331
#### 새로운 기능:
- 공식 MySQL 5.7.22 버전의 JSON 시리즈 함수를 신규 추가하였습니다.
- 전자상거래의 타임세일 시나리오를 기반으로 한 [Real-Time Session](https://intl.cloud.tencent.com/document/product/1035/48638) 기능 지원.
- [SQL throttling](https://intl.cloud.tencent.com/document/product/1035/48638) 지원.
- 데이터 암호화 기능으로 KMS 사용자 지정 키 암호화를 지원합니다.

#### bug 수정:
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 있었던 crash 문제 수정.
- 동시 실행이 많을 때 CATS(Contention-Aware Transaction Scheduling) 락(Lock) 스케쥴링 모듈에 있었던 crash 문제 수정.

### 20190830
#### 새로운 기능:
- binlog 파일이 손상됐을 때 건너뛰고 이어서 리졸브하는 기능 지원. 프라이머리 인스턴스와 binlog가 모두 손상된 경우 백업 데이터베이스의 데이터를 최대한 복구하여 사용할 수 있도록 합니다.
- GTID 모드부터 GTID 외 모드까지의 데이터 동기화를 지원합니다.
- 사용자가 show full processlist를 통해 '사용자의 스레드 메모리 사용 정보'를 조회하도록 지원합니다.
- 테이블에 [빠른 칼럼 추가 기능](https://intl.cloud.tencent.com/document/product/236/35988)을 지원합니다. 데이터를 복사하거나 디스크 용량, 디스크 I/O를 차지하지 않으며 비즈니스 피크 기간에도 실시간으로 변경할 수 있습니다.
- 자동 자동 증가값(Auto_increment) 지속화를 지원합니다.

#### bug 수정:
- Grant에서 칼럼 이름에 예약어가 발견되어 복제가 중단되는 문제 수정.
- 파티션 테이블에서 역스캔을 실행하여 SQL 실행 효율이 낮아지는 문제 수정.
- 기본 키 테이블의 가상화 색인 데이터가 불일치함에 따른 쿼리 결과 오류 문제 수정.
- InnoDB 기본 키 범위 쿼리로 인한 데이터 결함 문제 수정.
- 용량 색인을 포함한 테이블에 DDL을 실행함에 따른 시스템 crash 문제 수정.
- binlog가 지나치게 클 때, 하트비트 메시지의 파일 길이 초과로 인해 프라이머리/세컨더리가 중단되는 문제 수정.
- event 삭제로 인해 다른 event가 제때 실행되지 않는 문제 수정.
- 집계 질의 결과 오류 문제 수정.

### 20190615
#### 새로운 기능:
- 투명한 데이터 암호화 기능을 지원합니다.

### 20190430
#### bug 수정:
- 서브 쿼리에서 긴 텍스트 기능을 사용할 때의 널 포인터 디레퍼런스 문제 수정.
- Hash Scan으로 인한 프라이머리/세컨더리 중단 문제 수정.
- 프라이머리 데이터베이스 binlog 교체로 인한 slave 노드 I/O 스레드 중단 문제 수정.
- NAME_CONST로 인한 crash 문제 수정.
- 문자 세트로 인한 illegal mix of collation 문제 수정.

### 20190203
#### 새로운 기능:
- 비동기화 시 대용량 테이블 삭제 지원: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- CATS 락(Lock) 스케쥴링 모드를 지원합니다.
- GTID를 실행할 때 트랜잭션에서 임시 테이블과 CTS 구문을 생성, 삭제할 수 있도록 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 내장 기본 키를 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill 할 수 있는 기능을 지원합니다. cdb_kill_user_extra 매개변수를 통해 설정하며, 기본값은 root@%입니다.
- 엔터프라이즈급 암호화 함수를 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### bug 수정:
- binlog 캐시 파일 용량 부족에 따른 복제 중단 문제 수정.
- fsync에서 EIO 리턴 시 반복적으로 무한 루프에 빠지려 하는 문제 수정.
- GTID 홀(Hole)로 인한 복제 중단 및 복구 불가 문제 수정.
  
### 20180918
#### 새로운 기능:
- 유휴 트랜잭션을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- Memory 엔진을 InnoDB 엔진으로 자동 교체: 전역 변수cdb_convert_memory_to_innodb가 ON이라면, 테이블 생성/수정 시 테이블 엔진을 Memory에서 InnoDB로 교체합니다.
- 색인 숨기기 기능을 지원합니다.
- Jemalloc 메모리 관리를 지원합니다. jlibc 메모리 관리 모듈을 교체하여 메모리 사용량이 감소하고, 메모리 할당 효율은 증가합니다.
  
#### 성능 최적화:
- binlog 교체 최적화로, rotate HOLDLOCK 시간을 줄이고 시스템 성능을 향상시켰습니다.
- Crash Recovery 속도를 향상시켰습니다.
  
#### bug 수정:
- 프라이머리/세컨더리 스위치로 인한 event 무효화 문제 수정.
- REPLAY LOG RECORD로 인한 Crash 문제 수정.
- Loose index scans로 인한 쿼리 결과 오류 문제 수정.

### 20180530
#### 새로운 기능:
- SQL 감사 기능을 지원합니다.
- 테이블 레벨별 동시 복제 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
  
#### 성능 최적화:
- slave 인스턴스의 락을 최적화하여, 해당 slave 인스턴스의 동기화 성능을 향상시켰습니다.   
- select ... limit의 푸시다운을 최적화하였습니다.
  
#### bug 수정:
- relay_log_pos & master_log_pos 위치 불일치로 인한 교체 실패 문제 수정.
- Crash on UPDATE ON DUPLICATE KEY로 인한 Crash 문제 수정.
- JSON 칼럼 가져오기에 따른 'Invalid escape character in string.' 오류 수정.
  
### 20171130
#### 새로운 기능:
- information_schema.metadata_locks 뷰를 지원합니다. 현재 인스턴스의 MDL 권한 및 대기 상태를 조회할 수 있습니다.
- ALTER TABLE NO_WAIT | TIMEOUT 구문을 지원하며 DDL 작업에 대기 타임아웃을 제공합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 스레드 풀을 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### bug 수정:
- bytes_data를 기준으로 innodb_buffer_pool_pages_data를 연산하여 해당 매개변수의 오버플로우(Overflow) 방지.
- 비동기화 모드에서 속도 제한 플러그 인을 사용할 수 없는 문제 수정.

## MySQL 5.6
### 20220302
#### Bug 수정:
- sql_update.cc에서 메모리 유출을 수정했습니다.

### 20220301
#### 새로운 기능:
- 스핀 주기의 동적 구성을 지원합니다. 스핀 주기(0~100)는 동적 매개변수 innodb_spin_wait_pause_multiplier를 통해 동적으로 조정할 수 있습니다.
이 매개변수는 임시 조정에 사용되며, 콘솔을 통한 고정된 수정은 지원하지 않습니다.
- 교착 상태 루프 정보 출력 기능을 지원합니다.
innodb_print_dead_lock_loop_info 매개변수를 통해 활성화하고 활성화 후 교착 상태가 발생하면 show engine innodb status를 사용하여 교착 상태 루프 정보를 확인합니다.

#### Bug 수정:
- slave 재시작 후 memory 테이블의 익명 GTID 트랜잭션 문제 수정.
- root@localhost 권한이 누락되어 업그레이드가 실패하는 문제 수정.
- innodb_row_lock_current_waits 등의 모니터링 변수 값이 비정상인 문제 수정.
- 감사 플러그 인의 sql type 매핑이 잘못된 문제 수정.

### 20211030
#### 새로운 기능:
- 대규모 트랜잭션 복제 최적화를 지원합니다.

#### 성능 최적화:
- hash scan의 애플리케이션 속도를 최적화했습니다.

#### Bug 수정:
- 다수의 테이블 쿼리로 인한 OOM 문제 수정.
- innodb_thread_concurrecy를 0으로 설정 시 발생하는 무한 루프 문제 수정.
- 긴 기록의 통계가 0인 문제 수정.
- sbm 점프 문제 수정.
- LOCK_binlog_end_pos hang 문제 수정.

### 20210630
#### 새로운 기능:
- 대규모 트랜잭션 복제 최적화를 지원합니다.

#### Bug 수정:
- index merge가 켜져 있을 때 복사의 정확성 문제 수정.
- row 모드에서 cdb_more_gtid_feature_supported가 켜져 있을 때 create table select 실행 중단으로 인해 복제가 중단되는 문제 수정.
- max(id)가 show create table 중 AUTO_INCREMENT 보다 큰 Bug 수정.

### 20201231
#### bug 수정:
- hash scan으로 인한 1032 문제 수정. 
- row 포맷의 replace into로 인한 프라이머리/세컨더리 auto increment 값 불일치 문제 수정.
- SQL 분석 신청 메모리가 릴리스되지 않아 메모리 유출이 발생하는 문제 수정.
- create table as select로 테이블 생성 시 sql mode 검사를 건너뛰는 문제 수정.
- Insert 명령어로 기본값 삽입 시 sql mode 검사를 건너뛰는 문제 수정.
- 매개변수를 바인딩하여 update 명령어를 실행할 때 sql mode 검사를 건너뛰는 문제 수정.

### 20200915
#### 새로운 기능:
- [SQL throttling](https://intl.cloud.tencent.com/document/product/1035/48638) 기능 지원

#### 성능 최적화:   
- buffer pool 초기화 가속을 최적화하였습니다.

#### bug 수정:
- 프라이머리/세컨더리 rename table이 모두 hang되는 문제 수정. 
- event_scheduler를 disable로 설정하고 cdb_skip_event_scheduler를 on에서 off로 변경할 때 발생하는 crash 문제 수정. 
- tencentroot 최대 링크 수에 srv_max_n_threads가 포함되지 않아 sync_wait_array 관련 어서션이 실패하는 문제 수정. 
- 기타 클라우드 서비스의 MySQL 5.6과 Tencent MySQL 5.6의 시스템 라이브러리에서 일부 테이블의 구조가 달라 프라이머리/세컨더리 동시 복사 활성화 시 crash가 발생하는 문제 수정. 
- INSERT ON DUPLICATE KEY UPDATE THE WRONG ROW 문제 수정. 
- index_mapping에 발생하는 오류 문제 수정. 
- mtr 실패 bug 문제 수정. 
- event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 프라이머리/세컨더리가 중단되는 문제 수정. 

### 20190930
#### 새로운 기능:
- 사용자의 show full processlist를 통한 '사용자 스레드 메모리 사용 정보' 조회를 지원합니다.  

#### bug 수정:
- 백업 데이터베이스 replication filter로 인한 gtid hole 문제 수정.
- Binlog가 지나치게 클 때, 하트비트 메시지의 파일 길이 초과로 인해 프라이머리/세컨더리가 중단되는 문제 수정.
- 문자 세트로 인한 illegal mix of collation 문제 수정.
- Hash Scan으로 인한 프라이머리/세컨더리 중단 문제 수정.
- 한 NAME_CONST 용법으로 인한 crash 문제 수정.
- 프라이머리 데이터베이스 binlog 교체로 인한 slave 노드 I/O 스레드 중단 문제 수정.
- innodb_log_checusum으로 인해 백업이 호환되지 않는 문제 수정.

### 20190530
#### bug 수정:
- RC 모드에서 오손 데이터를 읽는 문제 수정.
- 임시 테이블 삭제로 인한 세컨더리에서 다시보기 실패 문제 수정.
- 동시 실행이 많을 때의 데드 락 문제 수정.
  
### 20190203
#### 새로운 기능:
- 비동기화 시 대용량 테이블 삭제: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 막을 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill 할 수 있는 기능을 지원합니다. cdb_kill_user_extra 매개변수를 통해 설정하며, 기본값은 root@%입니다.
- GTID를 실행할 때 트랜잭션에서 임시 테이블과 CTS 구문을 생성, 삭제할 수 있도록 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
  
#### 성능 최적화:   
- 파티션 테이블의 복제 다시보기를 최적화하여 다시보기 속도를 향상시켰습니다.
  
#### bug 수정:
- 임시 용량 부족으로 인한 프라이머리/세컨더리 불일치 문제 수정.
- 핫스팟 기록 업데이트 오류 문제 수정.
- 병행 복제 시 Seconds_Behind_Master 값 오류 문제 수정.

### 20180915
#### 새로운 기능:
- MEMORY 엔진을 InnoDB 엔진으로 자동 교체: 전역 변수cdb_convert_memory_to_innodb가 ON이라면, 테이블 생성/수정 시 테이블 엔진을 MEMORY에서 InnoDB로 전환합니다.
- 유휴 트랜잭션을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
  
#### bug 수정:
- REPLAY LOG RECORD로 인한 crash 문제 수정.
- decimal 정확성 문제로 인한 프라이머리/세컨더리 시간 데이터 불일치 문제 수정.

### 20180130
#### 새로운 기능:
- 스레드 풀을 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- slave 노드에서 복제한 필터링 조건을 동적으로 수정할 수 있도록 지원합니다.

#### 성능 최적화:
- drop table로 인한 성능 지터.
  
#### bug 수정:
- 비밀번호 문자열 인증으로 인한 데이터베이스 crash 문제 수정.
  
### 20180122
#### 새로운 기능:
- SQL 감사 기능을 지원합니다.

#### bug 수정:
- 정수 오버플로우 문제 수정.
- 전체 텍스트 인덱스 쿼리 오류 문제 수정.
- 복제 시 세컨더리 기기의 crash 문제 수정.
	
### 20170830
#### bug 수정:
- 비동기화 모드에서 binlog 속도 제한 무효화 문제 수정.
- buffer_pool 상태 오류 문제 수정.
- SEQUENCE와 내장 기본 키가 충돌하는 문제 수정.
  
### 20170228
#### bug 수정:
- drop table 중의 문자 인코딩 bug 수정.
- replicate-wild-do-table에서 db 혹은 table에 포함된 소수점 등의 특수문자를 정확히 필터링할 수 없는 문제 수정.
- 백업 데이터베이스에 rotate 이벤트가 발생한 이후 SQL 스레드가 미리 종료되는 문제 수정.
  
### 20161130
#### 성능 최적화:
- lock_log 락을 해제하여 lock log의 사용 시간을 단축하고, 동시 실행 성능을 향상시켰습니다.
- 프라이머리 데이터베이스의 ACK 스레드가 독립되어 응답 시간이 향상되었습니다.
- 사용자 스레드가 ACK를 기다리는 과정에서 kill 기능을 사용하지 못하도록 하여 가상 판독(Phantom Read)을 방지하였습니다.
- sync_binlog != 1에 따른 불필요한 lock_sync 락 문제를 수정하였습니다.
