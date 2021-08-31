본 문서는 MySQL 커널 버전 업데이트 현황에 대해 소개합니다. 업그레이드가 필요한 경우 [커널 마이너 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/36816)를 참조하십시오.

## MySQL 8.0
### 20201230
#### 업데이트 현황
- 공식 홈페이지 [8.0.19](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-19.html), [8.0.20](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-20.html), [8.0.21](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-21.html), [8.0.22](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-22.html) 변경 병합
- thread_handling 스레드 모드 또는 연결 풀 모드 동적 설정 지원

#### 성능 최적화
- BINLOG LOCK_done 락 충돌 최적화로 쓰기 성능 향상
- Lock Free Hash를 사용해 trx_sys mutex 충돌을 최적화하여 성능 향상
- redo log 플러시 최적화
- buffer pool 초기화 시간 최적화
- 대용량 테이블 drop table의 AHI 정리 최적화
- 감사 성능 최적화

#### 공식 홈페이지 Bug 수정
- innodb 임시 테이블 정리 시 성능 지터 발생 문제 수정
- 코어 수가 많은 인스턴스의 read only 성능 저하 문제 수정
- hash scan으로 인한 1032 발생 문제 수정
- 핫스팟 업데이트 기능의 동시 접속 보안 문제 수정

### 20200630
#### 업데이트 현황
- 대용량 테이블 비동기 삭제 지원: 파일을 비동기 방식 및 느린 속도로 정리하면 대용량 테이블 삭제로 인한 작업 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 유휴 작업을 자동으로 kill하여 리소스 충돌을 줄입니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- TDE 기능 지원

#### 공식 홈페이지 Bug 수정
- relay_log_pos & master_log_pos 위치 불일치로 인한 전환 실패 문제 수정
- 비동기 저장으로 인한 데이터 파일 오류 문제 수정
- fsync에서 EIO 반환 시 반복적으로 무한 루프에 빠지려 하는 문제 수정
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 존재하는 크래쉬 문제 수정

## MySQL 5.7
### 20201231
#### 업데이트 현황
- SELECT FOR UPDATE/SHARE에서 NOWAIT 및 SKIP LOCKED 옵션 사용 지원
- thread_handling 스레드 모드 또는 연결 풀 모드 동적 설정 지원
- 마스터/슬레이브 buffer pool 동기화 기능 지원
- 사용자 연결 상태 모니터링 기능의 모니터링 항목에 동기/비동기 IO, 메모리, 로그 양, CPU 시간, 점유 시간 락(Lock) 등 포함

#### 성능 최적화
- 트랜잭션 서브 시스템 최적화로 동시 접속 성능 향상
- 대규모 트랜잭션 crash recover 실행 시간 최적화
- redo log 플러시 최적화
- buffer pool 초기화 시간 최적화
- utf8/utf8mb4 문자열 효율 최적화
- 감사 성능 최적화
- gtid_purged를 반드시 null로 설정해야 하는 제한 삭제
- 백업 락(Lock) 최적화: LOCK TABLES FOR BACKUP, LOCK BINLOG FOR BACKUP, UNLOCK BINLOG 3개의 신규 SQL 명령어 도입. FLUSH TABLES WITH READ LOCK의 백업 락 방식은 전체 데이터베이스에 서비스 제공이 불가능하지만, 해당 3개 명령어는 데이터베이스에 대한 경량급 락 백업을 위해 백업 과정에서의 데이터 액세스 지원. 물리 백업이나 로직 백업 상관없이 해당 명령어를 사용해 백업의 일관성 구현 가능.
- 대용량 테이블의 drop table 최적화

#### 공식 홈페이지 Bug 수정
- performance_schema 쿼리 시 hang되는 문제 수정
- digest_add_token 함수 내의 overflow 문제 수정
- MySQL 공식 홈페이지 truncate table 시 ibuf 액세스로 인한 crash 문제 수정
- left join 명령어에서 const 사전 계산으로 인한 쿼리 정확성 문제 수정

### 20200930
#### 성능 최적화
- 백업 락(Lock) 최적화 
FLUSH TABLES WITH READ LOCK의 백업 락(Lock) 방식으로 인해 전체 데이터베이스에 서비스 제공이 불가능하며, 해당 버전에서는 데이터베이스에 대한 경량급 락 백업 방식 제공
- 대용량 테이블의 drop table 최적화 
신속한 어댑티브 해시 정리의 최적화(innodb_fast_ahi_cleanup_for_drop_table 제어)로 대용량 테이블 drop 시 어댑티브 해시 인덱스 정리 소모 시간 대폭 단축 가능

#### 공식 홈페이지 Bug 수정
- MySQL 공식 홈페이지 truncate table 시 ibuf 액세스로 인한 crash 문제 수정
- 빠른 컬럼 추가 후 콜드 스탠바이로 풀링할 수 없는 문제 수정
- innodb 메모리 테이블 객체의 빈번한 릴리스로 성능이 저하되는 문제 수정
- left join 명령어에서 const 사전 계산으로 인한 쿼리 정확성 문제 수정
- sql 제한 및 query rewrite 플러그 인에 Rule 클래스 이름 충돌로 core가 발생하는 문제 수정
- 여러 session에서 insert on duplicate key update 명령어의 동시 업데이트 문제 수정
- auto_increment_increment 동시 삽입 시 duplicate key error 실패가 발생하는 문제 수정
- innodb 메모리 객체가 제거되어 시스템이 다운되는 문제 수정
- 핫스팟 업데이트 기능의 동시 접속 보안 문제 수정
- jemalloc 5.2.1 버전으로 업데이트 시 스레드 풀 활성화로 coredump가 트리거되는 문제 수정
- fwrite 처리 오류가 없을 때 감사 로그가 불완전한 문제 수정
- mysqld_safe를 root 사용자로 실행할 때 로그가 출력되지 않는 문제 수정
- alter table exchange partition으로 인한 ddl log 파일 증가 문제 수정

### 20200701
#### 공식 홈페이지 Bug 수정
- INNOBASE_SHARE index mapping 오류 문제 수정

### 20200630
#### 업데이트 현황
- SELECT FOR UPDATE/SHARE 명령어의 NOWAIT 및 SKIP LOCKED 옵션 사용 지원
- 대용량 트랜잭션 최적화 기능 지원을 통해 대용량 트랜잭션으로 인한 마스터/슬레이브 딜레이, 백업 실패 등 문제 개선
- 감사 성능 최적화: 비동기 감사 기능 지원

#### 공식 홈페이지 Bug 수정
- digest_add_token 함수 내의 오버플로우 문제 수정
- insert blob으로 인한 인스턴스 crash 문제 수정
- event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 마스터/슬레이브가 중단되는 문제 수정
- performance_schema 쿼리 시 hang되는 문제 수정

### 20200331
#### 업데이트 현황
- 공식 홈페이지 MySQL 5.7.22 버전의 JSON 시리즈 함수 신규 추가
- 전자상거래의 타임세일 시나리오를 기반으로 한 [이슈 업데이트](https://intl.cloud.tencent.com/document/product/1035/36037) 기능 지원
- [SQL 제한](https://intl.cloud.tencent.com/document/product/1035/36037) 지원
- 데이터 암호화 기능으로 KMS 사용자 지정 키 암호화 지원

#### 공식 홈페이지 Bug 수정
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 존재하는 크래쉬 문제 수정
- 동시 접속이 많을 때 CATS 락 스케쥴링 모듈에 있었던 크래쉬 문제 수정

### 20190830
#### 업데이트 현황
- binlog 파일 손상 시 건너뛰고 이어서 분석하는 기능 지원. 마스터 인스턴스와 binlog가 모두 손상된 경우 백업 데이터베이스의 데이터를 최대한 복구하여 사용
- 비 GTID 모드에서 GTID 모드로의 데이터 동기화 지원
- 사용자의 show full processlist를 통한 '사용자 스레드 메모리 사용 정보' 조회 지원
- 테이블에 [빠른 칼럼 추가 기능](https://intl.cloud.tencent.com/document/product/236/35990)을 지원하여 데이터를 복사하지 않고 디스크 용량 및 디스크 I/O를 차지하지 않으며 비즈니스 피크 시간에도 실시간으로 변경 가능
- 자동 증가값(Auto_increment) 지속화 지원

#### 공식 홈페이지 Bug 수정
- Grant에서 칼럼 이름에 예약어가 발견되어 복사가 중단되는 문제 수정
- 파티션 테이블에서 역스캔을 실행하여 SQL 실행 효율이 낮아지는 문제 수정
- 기본 키 테이블의 버츄얼 색인 데이터 불일치에 따른 쿼리 결과 이상 경고 문제 수정
- InnoDB 기본 키 범위 쿼리로 인한 데이터 결함 문제 수정
- 용량 색인을 포함한 테이블에 DDL을 실행하여 일어나는 시스템 crash 문제 수정
- binlog가 너무 클 때, 하트비트 정보의 파일 길이가 제한을 초과하면 마스터/슬레이브가 중단되는 문제 수정
- event 삭제로 인해 다른 event가 제때 실행되지 않는 문제 수정
- 취합 쿼리 결과 오류 문제 수정

### 20190615
#### 업데이트 현황
- TDE 기능 지원

### 20190430
#### 공식 홈페이지 Bug 수정
- 서브 쿼리에서 긴 텍스트 기능 사용 시 널 포인터 역참조 문제 수정
- Hash Scan으로 인한 마스터/슬레이브 중단 문제 수정
- 마스터 데이터베이스 binlog 전환으로 인한 slave 노드 I/O 스레드 중단 문제 수정
- NAME_CONST로 인한 crash 문제 수정
- 문자 세트로 인한 illegal mix of collation 문제 수정

### 20190203
#### 업데이트 현황
- 대용량 테이블 비동기 삭제 지원: 파일을 비동기 방식 및 느린 속도로 정리하면 대용량 테이블 삭제로 인한 작업 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- CATS 락 스케쥴링 모드를 지원합니다.
- GTID 활성화 시 트랜잭션에서 임시 테이블과 CTS 구문의 생성, 삭제를 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 암묵적 기본 키를 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill할 수 있는 기능을 지원합니다. cdb_kill_user_extra 매개변수를 통해 설정하며 기본값은 root@%입니다.
- 엔터프라이즈급 암호화 함수를 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### 공식 홈페이지 Bug 수정
- binlog 캐시 파일 용량 부족에 따른 복사 중단 문제 수정
- fsync에서 EIO 반환 시 반복적으로 무한 루프에 빠지려 하는 문제 수정
- GTID 홀로 인한 복사 중단 및 복구 불가 문제 수정
   
### 20180918
#### 업데이트 현황
- 유휴 트랜잭션을 자동으로 kill하여 리소스 충돌을 줄입니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- Memory 엔진에서 InnoDB 엔진으로의 자동 전환: 전역 변수 cdb_convert_memory_to_innodb가 ON인 경우, 테이블 생성/수정 시 테이블 엔진을 Memory에서 InnoDB로 전환합니다.
- 색인 숨기기 기능 지원
- Jemalloc 메모리 관리 지원, jlibc 메모리 관리 모듈 교체로 메모리 점유율은 감소하고 메모리 할당 효율은 증가
   
#### 성능 최적화
- binlog 전환 최적화로 rotate HOLDLOCK 시간을 단축하여 시스템 성능 향상
- Crash Recovery 시 복구 속도 향상
    
#### 공식 홈페이지 Bug 수정
- 마스터/슬레이브 전환으로 인해 event가 유효하지 않은 문제 수정
- REPLAY LOG RECORD로 인한 Crash 문제 수정
- Loose index scans로 인한 쿼리 결과 오류 문제 수정

### 20180530
#### 업데이트 현황
- SQL 감사 기능 지원
- 테이블 레벨의 동시 복사를 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
   
#### 성능 최적화
- 슬레이브 인스턴스의 락 최적화로 해당 인스턴스의 동기화 성능 향상   
- select ... limit의 푸시다운 최적화
   
#### 공식 홈페이지 Bug 수정
- relay_log_pos & master_log_pos 위치 불일치로 인한 전환 실패 문제 수정
- Crash on UPDATE ON DUPLICATE KEY로 인한 crash 문제 수정
- JSON 칼럼 가져오기에 따른 'Invalid escape character in string.' 오류 수정
   
### 20171130
#### 업데이트 현황
- information_schema.metadata_locks 뷰 지원으로 현재 인스턴스의 MDL 권한 및 대기 상태를 조회할 수 있습니다.
- ALTER TABLE NO_WAIT | TIMEOUT 구문 지원으로 DDL 작업에 대기 타임아웃을 제공합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 스레드 풀 기능을 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### 공식 홈페이지 Bug 수정
- bytes_data를 기준으로 innodb_buffer_pool_pages_data를 계산하여 해당 매개변수의 오버플로우 방지
- 비동기 모드에서 속도 제한 플러그 인을 사용할 수 없는 문제 수정

## MySQL 5.6
### 20201231
#### 공식 홈페이지 Bug 수정
- hash scan으로 인한 1032 문제 수정 
- row 포맷의 replace into로 인한 마스터/슬레이브 auto increment 값 불일치 문제 수정
- SQL 분석 신청 메모리가 릴리스되지 않아 메모리 유출이 발생하는 문제 수정
- create table as select로 테이블 생성 시 sql mode 검사를 건너뛰는 문제 수정
- Insert 명령어로 기본값 삽입 시 sql mode 검사를 건너뛰는 문제 수정
- 매개변수를 바인딩하여 update 명령어를 실행할 때 sql mode 검사를 건너뛰는 문제 수정

### 20200915
#### 업데이트 현황
- [SQL 제한](https://intl.cloud.tencent.com/document/product/1035/36037) 기능 지원

#### 성능 최적화   
- buffer pool 초기화 가속 최적화

#### 공식 홈페이지 Bug 수정
- 마스터/슬레이브 rename table이 모두 hang되는 문제 수정 
- event_scheduler를 disable로 설정하고 cdb_skip_event_scheduler를 on에서 off로 변경할 때 발생하는 crash 문제 수정 
- tencentroot 최대 링크 수에 srv_max_n_threads가 포함되지 않아 sync_wait_array 관련 어서션이 실패하는 문제 수정 
- 기타 클라우드 서비스의 MySQL 5.6과 Tencent MySQL 5.6의 시스템 라이브러리에서 일부 테이블의 구조가 달라 마스터/슬레이브 동시 복사 활성화 시 crash가 발생하는 문제 수정 
- INSERT ON DUPLICATE KEY UPDATE THE WRONG ROW 문제 수정 
- index_mapping에 발생하는 오류 문제 수정 
- mtr 실패 bug 문제 수정 
- event에서 동일한 행을 업데이트하는 동안 hash scan이 기록을 찾지 못한 경우 마스터/슬레이브가 중단되는 문제 수정 

### 20190930
#### 업데이트 현황
- 사용자의 show full processlist를 통한 '사용자 스레드 메모리 사용 정보' 조회 지원  

#### 공식 홈페이지 Bug 수정
- 백업 데이터베이스 replication filter로 인한 gtid hole 문제 수정
- Binlog가 너무 클 때, 하트비트 정보의 파일 길이가 제한을 초과하면 마스터/슬레이브가 중단되는 문제 수정
- 문자 세트로 인한 illegal mix of collation 문제 수정
- Hash Scan으로 인한 마스터/슬레이브 중단 문제 수정
- 한 NAME_CONST 용법으로 인한 crash 문제 수정
- 마스터 데이터베이스 binlog 전환으로 인한 slave 노드 I/O 스레드 중단 문제 수정
- innodb_log_checusum으로 인해 백업이 호환되지 않는 문제 수정

### 20190530
#### 공식 홈페이지 Bug 수정
- RC 모드에서 오손 데이터를 읽는 문제 수정
- 임시 테이블 삭제로 인해 슬레이브에서 다시보기 실패 문제 수정
- 동시 접속이 많을 때의 데드락 문제 수정
   
### 20190203
#### 업데이트 현황
- 대용량 테이블 비동기 삭제: 파일을 비동기 방식 및 느린 속도로 정리하면 대용량 테이블 삭제로 인한 작업 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill할 수 있는 기능을 지원합니다. cdb_kill_user_extra 매개변수를 통해 설정하며 기본값은 root@%입니다.
- GTID 활성화 시 트랜잭션에서 임시 테이블과 CTS 구문의 생성, 삭제를 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
   
#### 성능 최적화   
- 파티션 테이블의 복사 다시보기를 최적화하여 다시보기 속도 향상
   
#### 공식 홈페이지 Bug 수정
- 임시 용량 부족으로 인한 마스터/슬레이브 불일치 문제 수정
- 핫스팟 기록 업데이트 보류 문제 수정
- 동시 복사 시 Seconds_Behind_Master 값 이상 경고 문제 수정

### 20180915
#### 업데이트 현황
- Memory 엔진에서 InnoDB 엔진으로의 자동 전환: 전역 변수 cdb_convert_memory_to_innodb가 ON인 경우, 테이블 생성/수정 시 테이블 엔진을 Memory에서 InnoDB로 전환합니다.
- 유휴 트랜잭션을 자동으로 kill하여 리소스 충돌을 줄입니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
   
#### 공식 홈페이지 Bug 수정
- REPLAY LOG RECORD로 인한 crash 문제 수정
- decima 정확성 문제로 인한 마스터/슬레이브 시간 데이터 불일치 문제 수정

### 20180130
#### 업데이트 현황
- 스레드 풀 기능을 지원합니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 슬레이브 노드는 복사한 필터링 조건을 동적으로 수정할 수 있도록 지원합니다.

#### 성능 최적화
- drop table로 인한 성능 지터
   
#### 공식 홈페이지 Bug 수정
- 비밀번호 문자열 인증으로 인한 데이터베이스 crash 문제 수정
   
### 20180122
#### 업데이트 현황
- SQL 감사 기능 지원

#### 공식 홈페이지 Bug 수정
- 정수 오버플로우 문제 수정
- 전체 텍스트 인덱스 쿼리 오류 문제 수정
- 복사 시 슬레이브의 crash 문제 수정
	
### 20170830
#### 공식 홈페이지 Bug 수정
- 비동기 모드에서 binlog 속도 제한이 유효하지 않은 문제 수정
- buffer_pool 상태 이상 경고 문제 수정
- SEQUENCE와 암묵적 기본 키가 충돌하는 문제 수정
   
### 20170228
#### 공식 홈페이지 Bug 수정
- drop table의 문자 인코딩 bug 수정
- replicate-wild-do-table에서 db 또는 table에 포함된 소수점 등 특수 문자를 정확히 필터링할 수 없는 문제 수정
- 백업 데이터베이스에 rotate 이벤트 발생 후 SQL 스레드가 미리 종료되는 문제 수정
  
### 20161130
#### 성능 최적화
- lock_log 락 분해로 lock log의 점유 시간 단축 및 동시 접속 성능 향상
- 마스터 데이터베이스의 ACK 스레드 독립으로 응답 시간 향상
- 사용자 스레드가 ACK를 기다리는 동안 가상 판독(Phantom Read)을 방지하기 위해 kill 기능은 허용하지 않음
- sync_binlog != 1에 따른 불필요한 lock_sync 락 문제 수정

