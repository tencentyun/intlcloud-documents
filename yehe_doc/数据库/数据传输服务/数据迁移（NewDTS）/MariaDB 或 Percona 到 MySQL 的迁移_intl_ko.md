본문은 DTS의 데이터 마이그레이션 기능을 사용하여 MariaDB 또는 Percona에서 TencentDB for MySQL로 데이터를 마이그레이션하는 방법을 설명합니다.

## 주의 사항 
- 전체 데이터 마이그레이션 중에 DTS는 원본 데이터베이스 리소스를 사용하므로 원본 데이터베이스의 로드와 부담이 증가할 수 있습니다. 데이터베이스 설정이 낮으면 사용량이 적은 시간에 데이터를 마이그레이션하는 것이 좋습니다.
- 전체 마이그레이션은 잠긴(백업 잠금) 테이블로 구현되어 몇 초 동안 쓰기 작업이 차단됩니다.

## 전제 조건
- [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/37785) 인스턴스를 생성해야 합니다.
- 원본 및 대상 데이터베이스는 [데이터 마이그레이션에서 지원하는 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42647)에 설명된 대로 마이그레이션 기능 및 버전에 대한 요구 사항을 충족해야 합니다.
- 모든 [준비 작업](https://intl.cloud.tencent.com/document/product/571/42652)을 마쳐야 합니다.
- 원본 데이터베이스에는 다음 권한이 있어야 합니다.
  - ‘전체 인스턴스’ 마이그레이션:
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO '마이그레이션 계정'@'%'; //원본 데이터베이스가 TencentDB 데이터베이스인 경우 `__tencentdb__` 권한 부여
GRANT SELECT ON *.* TO '마이그레이션 계정';
```
  - ‘지정 객체’ 마이그레이션:
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW, RELOAD, PROCESS ON *.* TO '마이그레이션 계정'@'%';  //원본 데이터베이스가 MariaDB/Percona 데이터베이스인 경우 'RELOAD'를 승인하려면 티켓을 제출해야 합니다. 그렇지 않으면 코드 예시를 참고하여 권한을 부여하십시오.
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO '마이그레이션 계정'@'%'; //원본 데이터베이스가 TencentDB 데이터베이스인 경우 `__tencentdb__` 권한 부여
GRANT SELECT ON `mysql`.* TO '마이그레이션 계정'@'%';
GRANT SELECT ON 마이그레이션 예정 데이터베이스.* TO '마이그레이션 계정';
```
 - 원본 데이터베이스가 MariaDB 10.5 또는 10.6인 경우 show slave status를 실행하려면 SLAVE MONITOR 권한도 필요합니다.
- 대상 데이터베이스 필요 권한: ALTER, ALTER ROUTINE, CREATE,  CREATE ROUTINE, CREATE TEMPORARY TABLES,  CREATE USER,  CREATE VIEW,  DELETE,  DROP,  EVENT,  EXECUTE,  INDEX,  INSERT,  LOCK TABLES,  PROCESS,  REFERENCES,  RELOAD,  SELECT,  SHOW DATABASES,  SHOW VIEW,  TRIGGER,  UPDATE.

## 이종 마이그레이션에 대한 호환성 설명
MariaDB에서 MySQL로 마이그레이션하는 동안 약간의 기능 차이로 인해 다음과 같은 호환성 문제가 발생할 수 있습니다.
1. MariaDB의 기능적 특성으로 인해 일부 SQL문은 SHOW CREATE TABLE의 반환 결과와 다르므로 대상 데이터베이스에서 동기화된 DDL 문에 차이가 발생할 수 있습니다.
   - MariaDB에서 blob 유형에 대해 기본값이 지정되지 않은 경우에도 SHOW CREATE TABLE은 테이블이 생성된 후 기본값 DEFAULT NULL을 계속 표시합니다.   
   - 원본 데이터베이스의 datetime 유형의 DDL 문이 'datetime NOT NULL ON UPDATE CURRENT_TIMESTAMP'인 경우 SHOW CREATE TABLE은 'datetime NOT NULL DEFAULT ‘0000-00-00 00:00:00’ ON UPDATE current_timestamp()'를 표시합니다. 테이블이 생성된 후 대상 MySQL이 구문 분석한 DDL은 'datetime NOT NULL ON UPDATE CURRENT_TIMESTAMP'가 됩니다.

2. MariaDB에서만 지원되는 일부 명령문(예: CREATE OR REPLACE TABLE/PERIOD FOR/WITHOUT OVERLAPS)은 마이그레이션 작업이 전체 마이그레이션 중에 오류를 보고하도록 할 수 있으며 증분 마이그레이션 중에는 무시됩니다. 
   - 마이그레이션 작업이 시작되기 전이나 전체 마이그레이션 중에(원본 데이터베이스 내보내기 및 데이터 가져오기 단계에서) PERIOD FOR/WITHOUT OVERLAPS 문이 실행되면 마이그레이션 작업이 실패합니다. 증분 동기화 중에 실행하면 대상 데이터베이스에서 이를 무시하고 데이터를 대상 데이터베이스에 동기화할 수 없습니다.
   - 전체 마이그레이션 중에는 데이터베이스나 테이블 구조를 변경하는 DDL 작업을 수행할 수 없으므로 전체 마이그레이션 중에 CREATE OR REPLACE TABLE 문을 실행하면 마이그레이션 작업이 실패합니다. 증분 동기화 중에 실행하면 대상 데이터베이스에서 이를 무시하고 데이터를 대상 데이터베이스에 동기화할 수 없습니다. 

3. MariaDB는 blob/text 데이터에 대한 기본값을 허용하지만 MySQL은 허용하지 않습니다. 이러한 유형의 SQL 문이 있는 경우 마이그레이션 작업에서 오류를 보고합니다.  

## 제한
- 기본 테이블 및 뷰만 마이그레이션할 수 있으며 함수, 트리거, 저장 프로시저와 같은 객체는 지원되지 않습니다.
- `information_schema`, `sys`, `sysdb`, `performance_schema`, `__cdb_recycle_bin__`, `__recycle_bin__`, `__tencentdb__`, `mysql`을 포함한 시스템 데이터베이스/테이블 및 사용자 정보는 마이그레이션할 수 없습니다. 마이그레이션이 완료된 후 대상 데이터베이스의 보기, 저장 프로시저 또는 함수를 호출하려면 호출자에게 읽기/쓰기 권한을 부여해야 합니다. 
- 뷰를 내보낼 때 DTS는 원본 데이터베이스의 `DEFINER`([DEFINER = user1])에 해당하는 user1이 마이그레이션 대상의 user2와 동일한지 확인하고, 동일하지 않은 경우 DTS는 대상 데이터베이스에 있는 user1의 `SQL SECURITY` 속성을 `DEFINER`에서 `INVOKER`([INVOKER = user1])로 변경하고 대상 데이터베이스의 `DEFINER`를 마이그레이션 대상의 user2로 설정합니다([DEFINER = 마이그레이션 대상 user2]).
- 원본 MySQL 데이터베이스가 비 GTID 데이터베이스인 경우 DTS는 이에 대한 HA 스위치를 지원하지 않습니다. 전환되면 DTS 증분 동기화가 중단될 수 있습니다.
- InnoDB, MySIAM 및 TokuDB 데이터베이스 엔진이 있는 데이터만 마이그레이션할 수 있습니다. 다른 데이터 테이블 엔진은 마이그레이션 중에 기본적으로 건너뜁니다.
- 연결된 데이터 객체는 함께 마이그레이션해야 합니다. 그렇지 않으면 마이그레이션이 실패합니다. 일반적인 연결 관계에는 뷰-테이블 참조, 뷰-뷰 참조, 저장 프로시저/함수/트리거 뷰/테이블 참조, 기본/외래 키 연결 테이블이 포함됩니다.
- 증분 마이그레이션 중에 원본 데이터베이스에 분산 트랜잭션이 있거나 `STATEMENT` 형식의 Binlog문을 생성하면 마이그레이션이 실패됩니다.
- DTS 마이그레이션 작업을 수행하려면 원본 및 대상 데이터베이스의 `lower_case_tame_name` 매개변수(테이블 이름 대소문자 구분) 값이 동일해야 합니다. 원본 데이터베이스가 TencentDB for MariaDB 또는 Percona인 경우 인스턴스 생성 중에만 이 매개변수를 수정할 수 있으므로 원본 데이터베이스를 생성할 때 대소문자 구분 규칙을 결정하고 검증 중 값이 다른 경우 대상 데이터베이스의 이 매개변수를 수정해야 합니다. .
-  원본 데이터베이스가 TencentDB for MariaDB 10.4인 경우 **액세스 유형**은 **데이터베이스** 옵션을 지원하지 않으며 **공용 네트워크** 또는 기타 유형을 선택해야 합니다.

## 작업 제한
- 마이그레이션하는 동안 다음 작업을 수행하지 마십시오. 그렇지 않으면 마이그레이션 작업이 실패합니다.
  - 원본 및 대상 데이터베이스와 포트 번호의 사용자 정보(사용자 이름, 암호 및 권한 포함)를 수정하거나 삭제하지 마십시오.
  - 원본 데이터베이스에서 분산 트랜잭션을 실행하지 마십시오.
  - `STATEMENT` 형식의 Binlog 데이터를 원본 데이터베이스에 쓰지 마십시오.
  - 원본 데이터베이스에서 Binlog를 지우지 마십시오.
  - 데이터베이스/테이블 구조 마이그레이션 또는 전체 마이그레이션 중에 데이터베이스/테이블 구조를 변경하는 DDL 작업을 실행하지 마십시오.
  - 증분 마이그레이션 중에 시스템 테이블 `__tencentdb__`를 삭제하지 마십시오. 
  - CREATE OR REPLACE TABLE/PERIOD FOR/WITHOUT OVERLAPS와 같은 MariaDB의 고유한 명령문이 포함된 경우 마이그레이션 작업은 전체 마이그레이션 중에 오류를 보고할 수 있으며 증분 마이그레이션 중에는 무시합니다.
- 전체 데이터 마이그레이션만 수행하는 경우 마이그레이션 중에 원본 데이터베이스에 새 데이터를 쓰지 마십시오. 그렇지 않으면 원본 및 대상 데이터베이스의 데이터가 일치하지 않습니다. 데이터 쓰기가 있는 시나리오에서 실시간으로 데이터 일관성을 보장하려면 전체+증분 데이터 마이그레이션을 선택하는 것이 좋습니다.

## 지원되는 SQL 작업
| 작업 유형 | 지원되는 SQL 작업                                              |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAEM TABLE <br>VIEW: CREATE VIEW, DROP VIEW<br>INDEX: CREATE INDEX, DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, DROP DATABASE |

## 환경 요건
>?시스템은 마이그레이션 작업을 시작하기 전에 다음 환경 요구 사항을 자동으로 확인하고 요구 사항이 충족되지 않으면 오류를 보고합니다. 실패 항목을 식별할 수 있는 경우 [확인 항목 요구 사항](https://intl.cloud.tencent.com/document/product/571/42552)에 따라 수정하십시오. 그렇지 않으면 시스템 확인이 완료될 때까지 기다렸다가 오류 메시지에 따라 문제를 수정하십시오.

<table>
<tr><th width="20%">유형</th><th width="80%">환경 요건</th></tr>
<tr>
<td>원본 데이터베이스 요구 사항</td>
<td>
<ul>
<li>원본 및 대상 데이터베이스를 연결할 수 있어야 합니다.</li>
<li>원본 데이터베이스가 있는 서버에 충분한 아웃바운드 대역폭이 있어야 합니다. 그렇지 않으면 마이그레이션 속도가 영향을 받습니다.</li>
<li>데이터베이스 매개변수 요구 사항:
<ul>
<li>원본 데이터베이스의 server_id 매개변수는 수동으로 설정해야 하며 0이 될 수 없습니다.</li>
<li>원본 데이터베이스/테이블의 row_format은 FIXED로 설정할 수 없습니다.</li>
<li>원본 및 대상 데이터베이스의 lower_case_table_names 변수 값은 동일해야 합니다.</li>
<li>원본 데이터베이스의 connect_timeout 변수는 10 이상이어야 합니다.</li>
<li>연결 시간 초과 가능성을 줄이려면 skip-name-resolve를 활성화하는 것이 좋습니다.</li></ul></li>
<li>Binlog 매개변수 요구 사항:
<ul>
<li>원본 데이터베이스의 log_bin 변수는 ON으로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_format 변수는 ROW로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_row_image 변수는 FULL로 설정해야 합니다.</li>
<li>MariaDB 10.2 이상 및 Percona 5.6 이상에서 gtid_mode 변수가 ON이 아니면 알람이 트리거됩니다. gtid_mode를 활성화하는 것이 좋습니다.</li>
<li>do_db 및 ignore_db로 필터 조건을 설정할 수 없습니다.</li>
<li>원본 데이터베이스가 세컨더리 데이터베이스인 경우 log_slave_updates 변수를 ON으로 설정해야 합니다.</li>
</ul></li>
<li>외래 키 종속성:
<ul>
<li>외래 키 종속성은 NO ACTION, RESTRICT 및 CASCADE의 세 가지 유형 중 하나로만 설정할 수 있습니다.</li>
<li>부분 테이블 마이그레이션 중에는 외래 키 종속성이 있는 테이블을 마이그레이션해야 합니다.</li>
</ul></li>
<li>FLOAT 유형의 데이터에 대한 DTS의 마이그레이션 정밀도는 38자리이며, DOUBLE 유형의 데이터는 308자리입니다. 요구 사항을 충족하는지 확인해야 합니다.</li></ul></td></tr>
<tr> 
<td>대상 데이터베이스에 대한 요구 사항</td>
<td>
<li>대상 데이터베이스 버전은 원본 데이터베이스 버전보다 높거나 같아야 합니다.</li>
<li>대상 데이터베이스 공간의 크기는 원본 데이터베이스에서 마이그레이션할 데이터베이스/테이블 크기의 1.2배 이상이어야 합니다. (전체 데이터 마이그레이션은 INSERT 작업을 동시에 실행하여 대상 데이터베이스의 일부 테이블에서 데이터 조각을 생성합니다. 따라서 전체 마이그레이션이 완료된 후 대상 데이터베이스의 테이블 크기가 원본 데이터베이스의 테이블 크기보다 클 수 있습니다.)</li>
<li>대상 데이터베이스는 원본 데이터베이스에 있는 것과 동일한 이름을 가진 테이블 및 뷰와 같은 마이그레이션 객체를 가질 수 없습니다.</li>
<li>대상 데이터베이스의 max_allowed_packet 매개변수는 4M 이상으로 설정해야 합니다.</li></td></tr>
<tr> 
<td>기타 요구 사항</td>
<td>환경 변수 innodb_stats_on_metadataw는 OFF로 설정해야 합니다.</td></tr>
</table>

## 작업 단계
MariaDB 및 Percona에서 MySQL로의 마이그레이션은 MySQL에서 MySQL로의 마이그레이션과 작업 단계가 같습니다. 자세한 설정은 [MySQL에서 MySQL로 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42645)을 참고하십시오.
