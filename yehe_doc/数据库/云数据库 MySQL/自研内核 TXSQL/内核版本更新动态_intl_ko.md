본문은 MySQL 커널 버전 업데이트 동향에 대해 소개합니다. 업그레이드를 하려면 [커널 마이너 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/36816)를 참고하시기 바랍니다.

## MySQL 8.0
### 20210330
#### 새로운 기능
- 마스터/슬레이브 bp 동기화 기능 지원: HA가 발생하여 마스터/슬레이브 전환이 필요한 경우, 백업 데이터베이스는 핫 스팟 데이터를 buffer pool로 로딩하는 warmup 작업에 긴 시간이 소모됩니다. 백업 DB의 프리패치 시간을 단축하기 위해 TXSQL은 마스터/슬레이브 bp 동기화 기능을 지원합니다. 
- Sort Merge Join 기능 지원.
- FAST DDL 기능 지원.
- 사용자 측 character_set_client_handshake 매개변수를 쿼리하여 현재 값 보기 기능 지원.

#### 성능 최적화
- flush list 더티 페이지 스캐닝 및 플러시 최적화: 더티 플러시 메커니즘을 최적화하여 인덱스 생성 과정의 성능 지터 문제 해결 및 시스템 안정성 향상.

#### Bug 수정
- offline_mode、cdb_working_mode 매개변수 변경 시 발생하는 데드락 문제 수정.
- trx_sys의max_trx_id 영구 동시 접속 문제 수정.

### 20201230
#### 새로운 기능
- 공식 업데이트 버전 [8.0.19](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-19.html), [8.0.20](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-20.html), [8.0.21](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-21.html), [8.0.22](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-22.html) 지원.
- thread_handling 스레드 모드 또는 연결 풀 모드 동적 설정 지원.

#### 성능 최적화
- BINLOG LOCK_done 락 충돌 최적화로 쓰기 성능 향상.
- Lock Free Hash를 사용해 trx_sys mutex 충돌을 최적화하여 성능 향상.
- redo log 플러시 최적화.
- buffer pool 초기화 시간 최적화.
- 대용량 테이블 drop table의 AHI 정리 최적화.
- 감사 성능 최적화.

#### Bug 수정
- innodb 임시 테이블 정리 시 성능 지터 발생 문제 수정.
- 코어 수가 많은 인스턴스의 read only 성능 저하 문제 수정.
- hash scan으로 인한 1032 발생 문제 수정.
- 핫스팟 업데이트 기능의 동시 접속 보안 문제 수정.

### 20200630
#### 새로운 기능
- 비동기화 시 대용량 테이블 삭제 지원: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 통해 신청해야 합니다.
- 유휴 작업을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 투명한 데이터 암호화 기능 지원.

#### Bug 수정
- relay_log_pos & master_log_pos 위치 불일치로 인한 교체 실패 문제 수정.
- 비동기화 디스크 저장으로 인한 데이터 파일 오류 문제 수정.
- fsync에서 EIO 리턴 시 반복적으로 무한 루프에 빠지려 하는 문제 수정.
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 있었던 crash 문제 수정.

## MySQL 5.7
### 20210331
#### 새로운 기능
- delete/insert/replace의 returning 구문을 지원하여 해당 statment가 작업한 데이터 데이터 행을 반환할 수 있습니다. delete 구문은 사전 이미지 데이터를 반환하고 insert/replace는 사후 이미지 데이터를 반환합니다.
- 열 압축 기능 지원: 현재의 행 포맷의 압축 및 데이터 페이지 압축 방식은 동일 테이블의 일부 큰 필드 및 다른 여러 작은 필드를 처리합니다. 작은 필드의 읽기/쓰기가 빈번하게 발생하지만 큰 필드 액세스가 빈번하지 않은 상황에서 이런 읽기/쓰기 액세스는 불필요한 컴퓨팅 리소스 낭비를 초래합니다. 열 압축 기능을 통해 액세스가 빈번하지 않은 큰 필드를 압축하고 전체 행 필드의 저장 공간을 줄이고 읽기/쓰기 액세스 효율을 향상시킬 수 있습니다.
- 사용자 측 character_set_client_handshake 매개변수를 쿼리하여 현재 값 보기 기능 지원.
- 로그 파일이 차지하는 page cache 자체 정리 지원: 해당 기능은 슬라이드 창 방식을 사용하여 posix_fadvise를 통해 로그 파일이 차지하는 page cache를 자체적으로 정리하여 운영 체제의 메모리 부하를 줄이고 시스템의 전체적인 안정성을 높였습니다.

#### 성능 최적화
- CREATE INDEX 병렬화: CREATE INDEX 과정에서 외부 분류와 정렬을 실행하는 건 오랜 시간이 걸립니다. 이번에 외부 분류 및 정렬 알고리즘을 도입하여 CREATE INDEX  소모 시간을 50% 이상 축소했습니다. 
- flush list 더티 페이지 스캐닝 및 플러시 최적화: 더티 플러시 메커니즘을 최적화하여 인덱스 생성 과정의 성능 지터 문제 해결 및 시스템 안정성 향상.

#### Bug 수정
- 메모리 유출 문제 수정.
- 8.0 버전 json 이식 문제를 수정하여 보다 안정적으로 json 사용 가능.
- hash scan으로 인한 1032 발생 문제 수정.
- 핫스팟 업데이트 기능의 동시 접속 보안 문제 수정.
- 공식 gcol 대량 이식 bug 수정.
- datetime 유형이 일부 시나리오에서 문자열과 비교 실패 문제 수정.
- 마스터/슬레이브 bp 동기화 기능 파일 핸들이 릴리스 되지 않는 bug 수정.
- offline_mode 설정과 동시에 연결을 생성할 경우 데드락이 트리거 되는 bug 수정.
- 범위 쿼리 동시 접속 시나리오에서 m_end_range 설정이 정확하지 않을 경우 발생하는 crash 문제 해결.
- groupby json 필드에 있는 temporay table의 긴 update 소모 시간 문제 수정.

### 20201231
#### 새로운 기능
- SELECT FOR UPDATE/SHARE에서 NOWAIT 및 SKIP LOCKED 옵션 사용 지원.
- thread_handling 스레드 모드 또는 연결 풀 모드 동적 설정 지원.
- 마스터/슬레이브 buffer pool 동기화 기능 지원.
- 사용자 연결 상태 모니터링 기능의 모니터링 항목에 동기/비동기 IO, 메모리, 로그 양, CPU 시간, 점유 시간 락(Lock) 등 포함.

#### 성능 최적화
- 트랜잭션 서브 시스템 최적화로 동시 접속 성능 향상.
- 대규모 트랜잭션 crash recover 실행 시간 최적화.
- redo log 플러시 최적화.
- buffer pool 초기화 시간 최적화.
- utf8/utf8mb4 문자열 효율 최적화.
- 감사 성능 최적화.
- gtid_purged를 반드시 null로 설정해야 하는 제한 삭제.
- 백업 락(Lock) 최적화: LOCK TABLES FOR BACKUP, LOCK BINLOG FOR BACKUP, UNLOCK BINLOG 3개의 신규 SQL 명령어 도입. FLUSH TABLES WITH READ LOCK의 백업 락 방식은 전체 데이터베이스에 서비스 제공이 불가능하지만, 해당 3개 명령어는 데이터베이스에 대한 경량급 락 백업을 위해 백업 과정에서의 데이터 액세스 지원. 물리 백업이나 로직 백업 상관없이 해당 명령어를 사용해 백업의 일관성 구현 가능.
- 대용량 테이블의 drop table 최적화.

#### Bug 수정
- performance_schema 쿼리 시 hang되는 문제 수정.
- digest_add_token 함수 내의 overflow 문제 수정.
- MySQL 공식 업데이트 버전 truncate table 시 ibuf 액세스로 인한 crash 문제 수정.
- left join 명령어에서 const 사전 계산으로 인한 쿼리 정확성 문제 수정.

### 20200930
#### 성능 최적화
- 백업 락(Lock) 최적화 
FLUSH TABLES WITH READ LOCK의 백업 락(Lock) 방식으로 인해 전체 데이터베이스에 서비스 제공이 불가능하며, 해당 버전에서는 데이터베이스에 대한 경량급 락 백업 방식 제공.
- 대용량 테이블의 drop table 최적화 
신속한 어댑티브 해시 정리의 최적화(innodb_fast_ahi_cleanup_for_drop_table 제어)로 대용량 테이블 drop 시 어댑티브 해시 인덱스 정리 소모 시간 대폭 단축 가능.

#### Bug 수정
- MySQL 공식 업데이트 버전 truncate table 시 ibuf 액세스로 인한 crash 문제 수정.
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
#### Bug 수정
- INNOBASE_SHARE index mapping 오류 문제 수정.

### 20200630
#### 새로운 기능
- SELECT FOR UPDATE/SHARE 명령어의 NOWAIT 및 SKIP LOCKED 옵션 사용 지원.
- 대용량 트랜잭션 최적화 기능 지원을 통해 대용량 트랜잭션으로 인한 마스터/슬레이브 딜레이, 백업 실패 등 문제 개선.
- 감사 성능 최적화: 비동기 감사 기능 지원.

#### Bug 수정
- digest_add_token 함수 내의 오버플로우 문제 수정.
- insert blob으로 인한 인스턴스 crash 문제 수정.
- event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 마스터/슬레이브가 중단되는 문제 수정.
- performance_schema 쿼리 시 hang되는 문제 수정.

### 20200331
#### 새로운 기능
- 새롭게 추가된 공식 MySQL 5.7.22 버전의 JSON 시리즈 함수.
- 전자상거래의 타임세일 시나리오를 기반으로 한 [핫스팟 업데이트](https://intl.cloud.tencent.com/document/product/1035/36037) 기능 지원.
- [SQL 제한](https://intl.cloud.tencent.com/document/product/1035/36037) 지원.
- 데이터 암호화 기능으로 KMS 사용자 지정 키 암호화 지원.

#### Bug 수정
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 있었던 crash 문제 수정.
- 동시 실행이 많을 때 CATS(Contention-Aware Transaction Scheduling) 락(Lock) 스케쥴링 모듈에 있었던 crash 문제 수정.

### 20190830
#### 새로운 기능
- binlog 파일이 손상됐을 때 건너뛰고 이어서 리졸브하는 기능 지원. 마스터 인스턴스와 binlog가 모두 손상된 경우 백업 데이터베이스의 데이터를 최대한 복구하여 사용할 수 있도록 합니다.
- GTID 모드부터 GTID 외 모드까지의 데이터 동기화 지원.
- 사용자가 show full processlist를 통해 '사용자의 스레드 메모리 사용 정보'를 조회하도록 지원.
- 테이블에 [빠른 칼럼 추가 기능](https://intl.cloud.tencent.com/document/product/236/35990) 지원. 데이터를 복사하지 않고 디스크 용량 및 디스크 I/O를 차지하지 않으며 비즈니스 피크 기간에도 실시간으로 변경할 수 있습니다.
- 자동 자동 증가값(Auto_increment) 지속화 지원.

#### Bug 수정
- Grant에서 칼럼 이름에 예약어가 발견되어 복제가 중단되는 문제 수정.
- 파티션 테이블에서 역스캔을 실행하여 SQL 실행 효율이 낮아지는 문제 수정.
- 기본 키 테이블의 가상화 색인 데이터가 불일치함에 따른 쿼리 결과 오류 문제 수정.
- InnoDB 기본 키 범위 쿼리로 인한 데이터 결함 문제 수정.
- 용량 색인을 포함한 테이블에 DDL을 실행함에 따른 시스템 crash 문제 수정.
- binlog가 지나치게 클 때, 하트비트 메시지의 파일 길이 초과로 인해 마스터/슬레이브가 중단되는 문제 수정.
- event 삭제로 인해 다른 event가 제때 실행되지 않는 문제 수정.
- 집계 질의 결과 오류 문제 수정.

### 20190615
#### 새로운 기능
- 투명한 데이터 암호화 기능 지원.

### 20190430
#### Bug 수정
- 서브 쿼리에서 긴 텍스트 기능을 사용할 때의 null 포인터 레퍼런스 문제 수정.
- Hash Scan으로 인한 마스터/슬레이브 중단 문제 수정.
- 마스터 데이터베이스 binlog 교체로 인한 slave 노드 I/O 스레드 중단 문제 수정.
- NAME_CONST로 인한 crash 문제 수정.
- 문자 세트로 인한 illegal mix of collation 문제 수정.

### 20190203
#### 새로운 기능
- 비동기화 시 대용량 테이블 삭제 지원: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 통해 신청해야 합니다.
- CATS 락(Lock) 스케쥴링 모드 지원.
- GTID를 실행할 때 트랜잭션에서 임시 테이블과 CTS 구문을 생성, 삭제할 수 있도록 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 내장 기본 키 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill 할 수 있는 기능 지원. cdb_kill_user_extra 매개변수를 통해 설정하며, 기본값은 root@%입니다.
- 기업급의 암호화 함수 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### Bug 수정
- binlog 캐시 파일 용량 부족에 따른 복제 중단 문제 수정.
- fsync에서 EIO 리턴 시 반복적으로 무한 루프에 빠지려 하는 문제 수정.
- GTID 홀(Hole)로 인한 복제 중단 및 복구 불가 문제 수정.
  
### 20180918
#### 새로운 기능
- 유휴 트랜잭션을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- Memory 엔진을 InnoDB 엔진으로 자동 교체: 전역 변수cdb_convert_memory_to_innodb가 ON이라면, 테이블 생성/수정 시 테이블 엔진을 Memory에서 InnoDB로 교체합니다.
- 색인 숨기기 기능 지원.
- Jemalloc 메모리 관리 지원. jlibc 메모리 관리 모듈을 교체하여 메모리 사용량이 감소하고, 메모리 할당 효율은 증가합니다.
  
#### 성능 최적화
- binlog 교체 최적화로, rotate HOLDLOCK 시간을 감소하여 시스템 성능 향상.
- crash 복구 속도 향상.
  
#### Bug 수정
- 마스터/슬레이브 스위치로 인한 event 무효화 문제 수정.
- REPLAY LOG RECORD로 인한 Crash 문제 수정.
- Loose index scans로 인한 쿼리 결과 오류 문제 수정.

### 20180530
#### 새로운 기능
- SQL 감사 기능 지원.
- 테이블 레벨별 동시 복제 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
  
#### 성능 최적화
- 슬레이브 인스턴스의 락을 최적화하여, 해당 인스턴스의 동기화 성능 향상.   
- select ... limit의 푸시다운 최적화.
  
#### Bug 수정
- relay_log_pos & master_log_pos 시점 불일치로 인한 교체 실패 문제 수정.
- Crash on UPDATE ON DUPLICATE KEY로 인한 crash 문제 수정.
- JSON 칼럼 가져오기에 따른 'Invalid escape character in string.' 오류 수정.
  
### 20171130
#### 새로운 기능
- information_schema.metadata_locks 뷰 지원. 현재 인스턴스의 MDL 권한 및 대기 상태를 조회할 수 있습니다.
- ALTER TABLE NO_WAIT | TIMEOUT 구문을 지원하며 DDL 작업에 대기 타임아웃 제공. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 스레드 풀(Thread Pool) 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### Bug 수정
- bytes_data를 기준으로 innodb_buffer_pool_pages_data를 연산하여 해당 매개변수의 오버플로우(Overflow) 방지.
- 비동기화 모드에서 속도 제한 플러그 인을 사용할 수 없는 문제 수정.

## MySQL 5.6
### 20201231
#### Bug 수정
- hash scan으로 인한 1032 문제 수정. 
- row 포맷의 replace into로 인한 마스터/슬레이브 auto increment 값 불일치 문제 수정.
- SQL 분석 신청 메모리가 릴리스되지 않아 메모리 유출이 발생하는 문제 수정.
- create table as select로 테이블 생성 시 sql mode 검사를 건너뛰는 문제 수정.
- Insert 명령어로 기본값 삽입 시 sql mode 검사를 건너뛰는 문제 수정.
- 매개변수를 바인딩하여 update 명령어를 실행할 때 sql mode 검사를 건너뛰는 문제 수정.

### 20200915
#### 새로운 기능
- [SQL 제한](https://intl.cloud.tencent.com/document/product/1035/36037) 기능 지원.

#### 성능 최적화   
- buffer pool 초기화 가속 최적화.

#### Bug 수정
- 마스터/슬레이브 rename table이 모두 hang되는 문제 수정. 
- event_scheduler를 disable로 설정하고 cdb_skip_event_scheduler를 on에서 off로 변경할 때 발생하는 crash 문제 수정. 
- tencentroot 최대 링크 수에 srv_max_n_threads가 포함되지 않아 sync_wait_array 관련 어서션 실패 문제 수정. 
- 기타 클라우드 서비스의 MySQL 5.6과 Tencent MySQL 5.6의 시스템 라이브러리에서 일부 테이블의 구조가 달라 마스터/슬레이브 동시 복사 활성화 시 crash가 발생하는 문제 수정. 
- INSERT ON DUPLICATE KEY UPDATE THE WRONG ROW 문제 수정. 
- index_mapping에 발생하는 오류 문제 수정. 
- mtr 실패 bug 문제 수정. 
- event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 마스터/슬레이브가 중단되는 문제 수정. 

### 20190930
#### 새로운 기능
- 사용자의 show full processlist를 통한 '사용자 스레드 메모리 사용 정보' 조회 지원.  

#### Bug 수정
- 백업 데이터베이스 replication filter로 인한 gtid hole 문제 수정.
- Binlog가 지나치게 클 때, 하트비트 메시지의 파일 길이 초과로 인해 마스터/슬레이브가 중단되는 문제 수정.
- 문자 세트로 인한 illegal mix of collation 문제 수정.
- Hash Scan으로 인한 마스터/슬레이브 중단 문제 수정.
- 한 NAME_CONST 용법으로 인한 crash 문제 수정.
- 마스터 데이터베이스 binlog 교체로 인한 slave 노드 I/O 스레드 중단 문제 수정.
- innodb_log_checusum으로 인해 백업이 호환되지 않는 문제 수정.

### 20190530
#### Bug 수정
- RC 모드에서 오손 데이터를 읽는 문제 수정.
- 임시 테이블 삭제로 인한 슬레이브에서 다시보기 실패 문제 수정.
- 동시 실행이 많을 때의 데드 락 문제 수정.
  
### 20190203
#### 새로운 기능
- 비동기화 시 대용량 테이블 삭제: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 막을 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill 할 수 있는 기능 지원. cdb_kill_user_extra 매개변수를 통해 설정하며, 기본값: root@%.
- GTID를 실행할 때 트랜잭션에서 임시 테이블과 CTS 구문을 생성, 삭제할 수 있도록 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
  
#### 성능 최적화   
- 파티션 테이블의 복제 다시보기를 최적화하여 다시보기 속도 향상.
  
#### Bug 수정
- 임시 용량 부족으로 인한 마스터/슬레이브 불일치 문제 수정.
- 핫스팟 기록 업데이트 오류 문제 수정.
- 병행 복제 시 Seconds_Behind_Master 값 오류 문제 수정.

### 20180915
#### 새로운 기능
- MEMORY 엔진을 InnoDB 엔진으로 자동 교체: 전역 변수cdb_convert_memory_to_innodb가 ON이라면, 테이블 생성/수정 시 테이블 엔진을 MEMORY에서 InnoDB로 교체합니다.
- 유휴 트랜잭션을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
  
#### Bug 수정
- REPLAY LOG RECORD로 인한 crash 문제 수정.
- decima 정확성 문제로 인한 마스터/슬레이브 시간 데이터 불일치 문제 수정.

### 20180130
#### 새로운 기능
- 스레드 풀(Thread Pool) 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 슬레이브 노드에서 복제한 필터링 조건을 동적으로 수정할 수 있도록 지원.

#### 성능 최적화
- drop table로 인한 성능 지터.
  
#### Bug 수정
- 비밀번호 문자열 인증으로 인한 데이터베이스 crash 문제 수정.
  
### 20180122
#### 새로운 기능
- SQL 감사 기능 지원.

#### Bug 수정
- 정수 오버플로우 문제 수정.
- 전체 텍스트 인덱스 쿼리 오류 문제 수정.
- 복제 시 슬레이브 기기의 crash 문제 수정.
	
### 20170830
#### Bug 수정
- 비동기화 모드에서 binlog 속도 제한 무효화 문제 수정.
- buffer_pool 상태 오류 문제 수정.
- SEQUENCE와 내장 기본 키가 충돌하는 문제 수정.
  
### 20170228
#### Bug 수정
- drop table 중의 문자 인코딩 bug 수정.
- replicate-wild-do-table에서 db 혹은 table에 포함된 소수점 등의 특수문자를 정확히 필터링할 수 없는 문제 수정.
- 백업 데이터베이스에 rotate 이벤트가 발생한 이후 SQL 스레드가 미리 종료되는 문제 수정.
  
### 20161130
#### 성능 최적화
- lock_log 락을 해제하여 lock log의 사용 시간을 단축하고, 동시 실행 성능 향상.
- 마스터 데이터베이스의 ACK 스레드가 독립되어 응답 시간 향상.
- 사용자 스레드가 ACK를 기다리는 과정에서 kill 기능을 사용하지 못하도록 하여 가상 판독(Phantom Read) 방지.
- sync_binlog != 1에 따른 불필요한 lock_sync 락 문제 수정.

