본 문서에서는 MySQL 커널 버전 업데이트 동향에 대해 소개합니다. 업그레이드가 필요하다면 [커널 마이너 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/36816)를 참조 바랍니다.

## MySQL 8.0
### 20200630
#### 새로운 특성:
- 비동기화 시 대용량 테이블 삭제 지원: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 통해 신청해야 합니다.
- 유휴 작업을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- Transparent Data Encryption(TDE)를 지원합니다.


#### Bug 수정:
- relay_log_pos & master_log_pos 위치 불일치로 인한 교체 실패 문제 수정.
- 비동기화 디스크 저장으로 인한 데이터 파일 오류 문제 수정.
- fsync에서 EIO 리턴 시 반복적으로 무한 루프에 빠지려 하는 문제 수정.
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 있었던 crash 문제 수정.

## MySQL 5.7
### 20200331
#### 새로운 특성:
- 새롭게 추가된 공식 MySQL 5.7.22 버전의 JSON 시리즈 함수.
- 전자상거래의 타임세일 시나리오를 기반으로 한 [잇슈 업데이트](https://intl.cloud.tencent.com/document/product/1035/36037) 기능 지원.
- [SQL 제한](https://intl.cloud.tencent.com/document/product/1035/36037) 지원.
- 데이터 암호화 기능으로 KMS 사용자 지정 키 암호화 지원.

#### Bug 수정:
- 전체 텍스트 인덱스에서 구문 검색(phrase search) 시 다중 바이트 문자 세트에 있었던 crash 문제 수정.
- 동시 실행이 많을 때 CATS(Contention-Aware Transaction Scheduling) 락(Lock) 스케쥴링 모듈에 있었던 crash 문제 수정.

### 20190830
#### 새로운 특성:
- binlog 파일이 손상됐을 때 건너뛰고 이어서 리졸브하는 기능 지원. 마스터 인스턴스와 binlog가 모두 손상된 경우 백업 데이터베이스의 데이터를 최대한 복구하여 사용할 수 있도록 합니다.
- GTID 모드부터 GTID 외 모드까지의 데이터 동기화 지원.
- 사용자가 show full processlist를 통해 '사용자의 스레드 메모리 사용 정보'를 조회하도록 지원.
- 테이블에 [빠른 칼럼 추가 기능](https://intl.cloud.tencent.com/document/product/236/35990) 지원. 데이터를 복사하지 않고 디스크 용량 및 디스크 I/O를 차지하지 않으며 비즈니스 피크 기간에도 실시간으로 변경할 수 있습니다.
- 자동 자동 증가값(Auto_increment) 지속화 지원.

#### Bug 수정:
- Grant에서 칼럼 이름에 예약어가 발견되어 복제가 중단되는 문제 수정.
- 파티션 테이블에서 역스캔을 실행하여 SQL 실행 효율이 낮아지는 문제 수정.
- 기본 키 테이블의 가상화 색인 데이터가 불일치함에 따른 쿼리 결과 오류 문제 수정.
- InnoDB 기본 키 범위 쿼리로 인한 데이터 결함 문제 수정.
- 용량 색인을 포함한 테이블에 DDL을 실행함에 따른 시스템 crash 문제 수정.
- binlog가 지나치게 클 때, 하트비트 메시지의 파일 길이 초과로 인해 마스터/슬레이브가 중단되는 문제 수정.
- event 삭제로 인해 다른 event가 제때 실행되지 않는 문제 수정.
- 집계 질의 결과 오류 문제 수정.

### 20190615
#### 새로운 특성:
- 투명한 데이터 암호화 기능 지원.

### 20190430
#### Bug 수정:
- 서브 쿼리에서 긴 텍스트 기능을 사용할 때의 널 포인터 디레퍼런스 문제 수정.
- Hash Scan으로 인한 마스터/슬레이브 중단 문제 수정.
- 마스터 데이터베이스 binlog 교체로 인한 slave 노드 I/O 스레드 중단 문제 수정.
- NAME_CONST로 인한 crash 문제 수정.
- 문자 세트로 인한 illegal mix of collation 문제 수정.


### 20190203
#### 새로운 특성:
- 비동기화 시 대용량 테이블 삭제 지원: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 방지할 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 통해 신청해야 합니다.
- CATS 락(Lock) 스케쥴링 모드 지원.
- GTID를 실행할 때 트랜잭션에서 임시 테이블과 CTS 구문을 생성, 삭제할 수 있도록 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 내장 기본 키 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill 할 수 있는 기능 지원. cdb_kill_user_extra 매개변수를 통해 설정하며, 기본값은 root@%입니다.
- 기업급의 암호화 함수 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### Bug 수정:
- binlog 캐시 파일 용량 부족에 따른 복제 중단 문제 수정
- fsync에서 EIO 리턴 시 반복적으로 무한 루프에 빠지려 하는 문제 수정.
- GTID 홀(Hole)로 인한 복제 중단 및 복구 불가 문제 수정.
   

### 20180918
#### 새로운 특성:
- 유휴 트랜잭션을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- Memory 엔진을 InnoDB 엔진으로 자동 교체: 전역 변수cdb_convert_memory_to_innodb가 ON이라면, 테이블 생성/수정 시 테이블 엔진을 Memory에서 InnoDB로 교체합니다.
- 색인 숨기기 기능 지원.
- Jemalloc 메모리 관리 지원. jlibc 메모리 관리 모듈을 교체하여 메모리 사용량이 감소하고, 메모리 할당 효율은 증가합니다.
   
#### 성능 최적화:
- binlog 교체 최적화로, rotate HOLDLOCK 시간을 감소하여 시스템 성능 향상.
- crash 복구 속도 향상.
    
#### Bug 수정:
- 마스터/슬레이브 스위치로 인한 event 무효화 문제 수정.
- REPLAY LOG RECORD로 인한 Crash 문제 수정.
- Loose index scans로 인한 쿼리 결과 오류 문제 수정.


### 20180530
#### 새로운 특성:
- SQL 감사 기능 지원.
- 테이블 레벨별 동시 복제 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
   
#### 성능 최적화:
- 슬레이브 인스턴스의 락을 최적화하여, 해당 인스턴스의 동기화 성능 향상.   
- select ... limit의 푸시다운 최적화.
   
#### Bug 수정:
- relay_log_pos & master_log_pos 시점 불일치로 인한 교체 실패 문제 수정.
- Crash on UPDATE ON DUPLICATE KEY로 인한 crash 문제 수정.
- JSON 칼럼 가져오기에 따른 'Invalid escape character in string.' 오류 수정.
   
### 20171130
#### 새로운 특성:
- information_schema.metadata_locks 뷰 지원. 현재 인스턴스의 MDL 권한 및 대기 상태를 조회할 수 있습니다.
- ALTER TABLE NO_WAIT | TIMEOUT 구문을 지원하며 DDL 작업에 대기 타임아웃 제공. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 스레드 풀(Thread Pool) 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.

#### Bug 수정:
- bytes_data를 기준으로 innodb_buffer_pool_pages_data를 연산하여 해당 매개변수의 오버플로우(Overflow) 방지.
- 비동기화 모드에서 속도 제한 플러그 인을 사용할 수 없는 문제 수정.

   
## MySQL 5.6
### 20190930
#### 새로운 특성:
- 사용자가 show full processlist를 통해 '사용자의 스레드 메모리 사용 정보'를 조회하도록 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.  

#### Bug 수정:
- 백업 데이터베이스 replication filter로 인한 gtid hole 문제 수정.
- Binlog가 지나치게 클 때, 하트비트 메시지의 파일 길이 초과로 인해 마스터/슬레이브가 중단되는 문제 수정.
- 문자 세트로 인한 illegal mix of collation 문제 수정.
- Hash Scan으로 인한 마스터/슬레이브 중단 문제 수정.
- 한 NAME_CONST 용법으로 인한 crash 문제 수정.
- 마스터 데이터베이스 binlog 교체로 인한 slave 노드 I/O 스레드 중단 문제 수정.
- innodb_log_checusum으로 인해 백업이 호환되지 않는 문제 수정.

### 20190530
#### Bug 수정:
- RC 모드에서 오손 데이터를 읽는 문제 수정.
- 임시 테이블 삭제로 인한 슬레이브에서 다시보기 실패 문제 수정.
- 동시 실행이 많을 때의 데드 락 문제 수정.
   

### 20190203
#### 새로운 특성:
- 비동기화 시 대용량 테이블 삭제: 비동기화로 느리게 파일을 정리하면 대용량 테이블 삭제로 인한 비즈니스 성능 지터 현상을 막을 수 있습니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 통해 신청해야 합니다.
- super 권한이 없는 사용자가 다른 사용자의 세션을 kill 할 수 있는 기능 지원. cdb_kill_user_extra 매개변수를 통해 설정하며, 기본값은 root@%입니다.
- GTID를 실행할 때 트랜잭션에서 임시 테이블과 CTS 구문을 생성, 삭제할 수 있도록 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
   
#### 성능 최적화:   
- 파티션 테이블의 복제 다시보기를 최적화하여 다시보기 속도 향상.
   
#### Bug 수정:
- 임시 용량 부족으로 인한 마스터/슬레이브 불일치 문제 수정.
- 핫스팟 기록 업데이트 오류 문제 수정.
- 병행 복제 시 Seconds_Behind_Master 값 오류 문제 수정.

### 20180915
#### 새로운 특성:
- MEMORY 엔진을 InnoDB 엔진으로 자동 교체: 전역 변수cdb_convert_memory_to_innodb가 ON이라면, 테이블 생성/수정 시 테이블 엔진을 MEMORY에서 InnoDB로 교체합니다.
- 유휴 트랜잭션을 자동으로 kill하도록 지원하여 리소스 충돌을 감소시킵니다. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
   
#### Bug 수정:
- REPLAY LOG RECORD로 인한 crash 문제 수정.
- decima 정확성 문제로 인한 마스터/슬레이브 시간 데이터 불일치 문제 수정.


### 20180130
#### 새로운 특성:
- 스레드 풀(Thread Pool) 지원. 해당 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청해야 합니다.
- 슬레이브 노드에서 복제한 필터링 조건을 동적으로 수정할 수 있도록 지원.

#### 성능 최적화:
- drop table로 인한 성능 지터.
   
#### Bug 수정:
- 비밀번호 문자열 인증으로 인한 데이터베이스 crash 문제 수정.
   
### 20180122
#### 새로운 특성:
- SQL 감사 기능 지원.

#### Bug 수정:
- 정수 오버플로우 문제 수정.
- 전체 텍스트 인덱스 쿼리 오류 문제 수정.
- 복제 시 슬레이브 기기의 crash 문제 수정.
	
### 20170830
#### Bug 수정:
- 비동기화 모드에서 binlog 속도 제한 무효화 문제 수정.
- buffer_pool 상태 오류 문제 수정.
- SEQUENCE와 내장 기본 키가 충돌하는 문제 수정.
   
### 20170228
#### Bug 수정:
- drop table 중의 문자 인코딩 bug 수정.
- replicate-wild-do-table에서 db 혹은 table에 포함된 소수점 등의 특수문자를 정확히 필터링할 수 없는 문제 수정.
- 백업 데이터베이스에 rotate 이벤트가 발생한 이후 SQL 스레드가 미리 종료되는 문제 수정.
  
### 20161130
#### 성능 최적화:
- lock_log 락을 해제하여 lock log의 사용 시간을 단축하고, 동시 실행 성능 향상.
- 마스터 데이터베이스의 ACK 스레드가 독립되어 응답 시간 향상.
- 사용자 스레드가 ACK를 기다리는 과정에서 kill 기능을 사용하지 못하도록 하여 가상 판독(Phantom Read) 방지.
- sync_binlog != 1에 따른 불필요한 lock_sync 락 문제 수정.

