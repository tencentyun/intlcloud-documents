본문은 DTS의 데이터 마이그레이션 기능을 사용하여 MySQL에서 TencentDB for MariaDB(Percona)로 데이터를 마이그레이션하는 방법을 설명합니다.

MariaDB(Percona)에서 MariaDB(Percona)로의 데이터 마이그레이션 및 MariaDB에서 MariaDB로의 데이터 마이그레이션은 MySQL에서 MariaDB(Percona)로 마이그레이션하는 것과 요구 사항이 동일합니다. 이 문서에서 관련 내용을 참고할 수 있습니다.

## 주의 사항

- DTS가 전체 데이터 마이그레이션을 진행할 때 일정 원본 인스턴스 리소스를 점유함으로써 원본 인스턴스 부하가 높아져 데이터베이스 자체의 부담이 가중될 수 있습니다. 데이터베이스의 사양이 낮을 경우 서비스 사용량이 적은 시간대에 진행하는 것을 권장합니다.
- 전체 마이그레이션은 잠긴 테이블로 구현되어 몇 초 동안 쓰기 작업이 차단됩니다.

## 전제 조건

- [TencentDB for MariaDB](https://intl.cloud.tencent.com/document/product/237/7051) 인스턴스를 생성해야 합니다.
- 원본 및 대상 데이터베이스는 [데이터 마이그레이션에서 지원하는 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42647)에 설명된 대로 마이그레이션 기능 및 버전에 대한 요구 사항을 충족해야 합니다.
- 모든 [준비 작업](https://intl.cloud.tencent.com/document/product/571/42652)을 마쳐야 합니다.
- 원본 MySQL 데이터베이스에 미리 `__tencentdb__` 데이터베이스를 생성해야 합니다.
- 원본 데이터베이스 권한이 있어야 합니다.
  - ‘전체 인스턴스’를 마이그레이션하려면 다음 계정 권한이 필요합니다.
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, CREATE ON `__tencentdb__`.* TO '마이그레이션 계정'@'%'; //원본 데이터베이스가 TencentDB 데이터베이스인 경우 `__tencentdb__` 권한을 부여해야 합니다.
GRANT SELECT ON *.* TO '마이그레이션 계정';
```
  - ‘지정된 객체’를 마이그레이션하려면 다음 계정 권한이 필요합니다.
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, CREATE ON `__tencentdb__`.* TO '마이그레이션 계정'@'%'; //원본 데이터베이스가 TencentDB 데이터베이스인 경우 `__tencentdb__` 권한을 부여해야 합니다.
GRANT SELECT ON `mysql`.* TO '마이그레이션 계정'@'%';
GRANT SELECT ON 마이그레이션 예정 데이터베이스.* TO '마이그레이션 계정';
```
- 대상 데이터베이스 필요 권한: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, UPDATE.

## 제한

- 기본 테이블만 마이그레이션할 수 있으며 뷰, 함수, 트리거 및 저장 프로시저와 같은 객체는 마이그레이션할 수 없습니다.
- `information_schema`, `sys`, `performance_schema`, `__tencentdb__`, `mysql`을 포함한 시스템 데이터베이스/테이블 및 사용자 정보는 마이그레이션할 수 없습니다. 마이그레이션이 완료된 후 대상 데이터베이스의 보기, 저장 프로시저 또는 함수를 호출하려면 호출자에게 읽기/쓰기 권한을 부여해야 합니다. 
- 뷰 구조를 내보낼 때 대상 마이그레이션 계정의 user@host와 동일한 `definer`만 마이그레이션할 수 있습니다.
- InnoDB 데이터베이스 엔진이 있는 데이터만 마이그레이션할 수 있습니다. 다른 엔진이 있는 테이블은 기본적으로 마이그레이션 중에 건너뜁니다.
- 관련 데이터 객체는 동시에 마이그레이션되어야 합니다. 그렇지 않으면 마이그레이션이 실패합니다.
- 증분 마이그레이션 중에 원본 데이터베이스에 분산 트랜잭션이 있거나 `STATEMENT` 형식의 Binlog문을 생성하면 마이그레이션이 실패됩니다.

## 작업 제한

- 마이그레이션하는 동안 다음 작업을 수행하지 마십시오. 그렇지 않으면 마이그레이션 작업이 실패합니다.
  - 원본 및 대상 데이터베이스와 포트 번호의 사용자 정보(사용자 이름, 암호 및 권한 포함)를 수정하거나 삭제하지 마십시오.
  - 원본 데이터베이스에서 분산 트랜잭션을 실행하지 마십시오.
  - `STATEMENT` 형식의 Binlog 데이터를 원본 데이터베이스에 쓰지 마십시오.
  - 원본 데이터베이스에서 Binlog를 지우지 마십시오.
  - 증분 마이그레이션 중에 시스템 테이블 `__tencentdb__`를 삭제하지 마십시오. 
- 전체 데이터 마이그레이션만 수행하는 경우 마이그레이션 중에 원본 데이터베이스에 새 데이터를 쓰지 마십시오. 그렇지 않으면 원본 및 대상 데이터베이스의 데이터가 일치하지 않습니다. 데이터 쓰기가 있는 시나리오에서 실시간으로 데이터 일관성을 보장하려면 전체+증분 데이터 마이그레이션을 선택하는 것이 좋습니다.

## 지원되는 SQL 작업

| 작업 유형 | 지원되는 SQL 작업                                         |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE<br>VIEW: CREATE VIEW, DROP VIEW<br>INDEX: CREATE INDEX, DROP INDEX <br> |

## 환경 요건

> ?시스템은 마이그레이션 작업을 시작하기 전에 다음 환경 요구 사항을 자동으로 확인하고 요구 사항이 충족되지 않으면 오류를 보고합니다. 실패 항목을 식별할 수 있는 경우 [확인 항목 요구 사항](https://intl.cloud.tencent.com/document/product/571/42552)에 따라 수정하십시오. 그렇지 않으면 시스템 확인이 완료될 때까지 기다렸다가 오류 메시지에 따라 문제를 수정하십시오.

<table>
<tr><th width="20%">유형</th><th width="80%">환경 요건</th></tr>
<tr>
<td>원본 데이터베이스 요구 사항</td>
<td>
<li>원본 및 대상 데이터베이스를 연결할 수 있어야 합니다.</li>
<ul>
<li>데이터베이스 매개변수 요구 사항:
<ul>
<li>table_row_format은 FIXED로 설정할 수 없습니다.</li>
<li>원본 및 대상 데이터베이스의 'lower_case_table_names' 변수 값은 동일해야 합니다.</li>
<li>대상 데이터베이스의 max_allowed_packet 매개변수는 4MB 이상이어야 합니다.</li>
<li>원본 데이터베이스의 connect_timeout 변수는 10 이상이어야 합니다.</li></ul></li>
<li>Binlog 매개변수 요구 사항:
<ul>
<li>원본 데이터베이스의 binlog_format 변수는 ROW로 설정해야 합니다.</li>
<li>원본 데이터베이스의 log_bin 변수는 ON으로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_row_image 변수는 FULL로 설정해야 합니다.</li>
<li>v5.6 이상에서는 원본 데이터베이스의 gtid_mode 변수가 ON이 아닌 경우 WARNING이 발생합니다. gtid_mode를 활성화하는 것이 좋습니다.</li>
<li>do_db 및 ignore_db를 설정할 수 없습니다.</li>
<li>원본 데이터베이스가 세컨더리 데이터베이스인 경우 log_slave_updates 변수를 ON으로 설정해야 합니다.</li></ul></li>
<li>외래 키 종속성:
<ul>
<li>외래 키 종속성은 no action 또는 restrict 유형일 수 있습니다.</li>
<li>부분 테이블 마이그레이션 중에는 외래 키 종속성이 있는 테이블을 마이그레이션해야 합니다.</li></ul></li></td></tr>
<tr> 
<td>대상 데이터베이스에 대한 요구 사항</td>
<td>
<li>대상 데이터베이스 버전은 원본 데이터베이스 버전보다 높거나 같아야 합니다.</li>
<li>대상 데이터베이스의 공간은 원본 데이터베이스에서 마이그레이션할 테이블 크기의 1.2배 이상이어야 합니다.</li>
<li>대상 데이터베이스는 원본 데이터베이스와 충돌하는 테이블을 가질 수 없습니다.</li>
<li>원본 데이터베이스 인스턴스가 분산 데이터베이스인 경우 대상 데이터베이스에 미리 샤딩된 테이블을 생성해야 합니다. 그렇지 않으면 테이블이 마이그레이션된 후 분할되지 않은 테이블이 됩니다.</li></td></tr>
<tr> 
<td>기타 요구 사항</td>
<td>환경 변수 innodb_stats_on_metadata를 OFF로 설정해야 합니다.</td></tr>
</table>

## 작업 단계
다양한 시나리오의 데이터 마이그레이션 단계는 기본적으로 동일합니다. 자세한 지침은 [MySQL에서 TDSQL for MySQL로 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42645)을 참고하십시오.

