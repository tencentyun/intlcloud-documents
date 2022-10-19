본문은 DTS의 데이터 동기화 기능을 사용하여 MySQL, MariaDB, Percona에서 TencentDB for MariaDB로 데이터를 동기화하는 방법을 설명합니다.

원본 데이터베이스에서 지원하는 배포 유형은 다음과 같습니다.

- 자체 구축 MySQL, TencentDB for MySQL.
- 자체 구축 MariaDB, TencentDB for MariaDB.
- 자체 구축 Percona.

MySQL, MariaDB 및 Percona는 TencentDB for MariaDB과 동기화되기 때문에 세 시나리오의 동기화 요구 사항 및 작업 단계는 기본적으로 동일합니다. 이 장에서는 TencentDB for MariaDB로의 데이터 동기화를 예로 들어 설명합니다. 다른 시나리오의 경우 관련 내용을 참고하십시오.

## 주의 사항
- 전체 데이터 동기화 중에 DTS는 특정 원본 데이터베이스 리소스를 사용하므로 원본 데이터베이스의 로드와 압력이 증가할 수 있습니다. 데이터베이스 설정이 낮으면 사용량이 적은 시간에 데이터를 동기화하는 것이 좋습니다.
- 데이터 중복을 방지하려면 동기화할 테이블에 기본 키 또는 null이 아닌 고유 키가 있어야 합니다.
- 기본적으로 잠금 없는 방식이 사용되며 동기화 과정에서 원본 데이터베이스에 전역 잠금(FTWRL)이 적용되지 않고 기본 키가 없는 테이블만 테이블 잠금이 추가되고 나머지는 NOLOCK입니다.
- 데이터 동기화 중에 DTS는 동기화 작업을 실행하는 계정을 사용하여 원본 데이터베이스에 시스템 데이터베이스`__tencentdb__`를 작성하여 동기화 작업 중에 데이터 비교 정보를 기록합니다.
  - 후속 데이터 문제를 찾을 수 있도록 원본 데이터베이스의 `__tencentdb__` 시스템 데이터베이스는 동기화 작업이 끝난 후 삭제되지 않습니다.
  - `__tencentdb__`시스템 데이터베이스는 단일 스레드 연결 대기 메커니즘을 사용하며 원본 데이터베이스의 저장 공간의 약 0.01%–0.1%인 매우 작은 공간을 차지합니다. 예를 들어, 원본 데이터베이스가 50G인 경우 `__tencentdb__`는 약 5K-50K가 됩니다. 따라서 원본 데이터베이스의 성능에 거의 영향을 미치지 않으며 리소스를 선점하지 않습니다. 

## [전제 조건](id:qttj)
- 원본 및 대상 데이터베이스는 [데이터 동기화가 지원하는 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42579)에 설명된 대로 동기화 기능 및 버전에 대한 요구 사항을 충족해야 합니다.
- 원본 데이터베이스에 필요한 권한:
```sql
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW VIEW,PROCESS,SELECT ON *.* TO '계정'@'%' IDENTIFIED BY '비밀번호';
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO '계정'@'%'; 
FLUSH PRIVILEGES;
```
- 대상 데이터베이스 필요 권한: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, UPDATE.

## 제한
- 기본 테이블, 뷰, 저장 프로시저 및 함수의 동기화만 지원합니다. 
- 뷰, 저장 프로시저 및 함수를 동기화할 때 DTS는 원본 데이터베이스의 `DEFINER`([DEFINER = user1])에 해당하는 user1이 동기화 계정의 user2와 동일한지 확인하고, 동일하지 않은 경우 동기화 후 DTS는 대상 데이터베이스에 있는 user1의 `SQL SECURITY` 속성을 `DEFINER`에서 `INVOKER`([INVOKER = user1])로 변경하고 대상 데이터베이스의 `DEFINER`를 동기화 계정의 user2로 설정합니다([DEFINER = 동기화 계정 user2]). 소스 라이브러리의 뷰 정의가 너무 복잡하면 작업이 실패할 수 있습니다.
- 원본 MySQL 데이터베이스가 비 GTID 데이터베이스인 경우 DTS는 이에 대한 HA 스위치를 지원하지 않습니다. 전환되면 DTS 증분 동기화가 중단될 수 있습니다.
- InnoDB, MyISAM 및 TokuDB의 세 가지 데이터베이스 엔진이 있는 데이터만 동기화할 수 있습니다. 다른 엔진이 있는 테이블은 기본적으로 동기화 중에 건너뜁니다.
- 연결된 데이터 객체는 함께 동기화해야 합니다. 그렇지 않으면 동기화에 실패합니다. 일반적인 연결 관계에는 뷰-테이블 참조, 뷰-뷰 참조, 기본/외래 키 연결 테이블 등이 포함됩니다.
- 증분 동기화 중에 원본 데이터베이스에 분산 트랜잭션이 있거나 `STATEMENT` 형식의 Binlog 문을 생성하면 동기화가 실패합니다.
- 원본 데이터베이스가 MySQL용 Alibaba Cloud ApsaraDB RDS인 경우 v5.6에서 동기화할 테이블에는 기본 키가 있어야 하지만 v5.7 이상에서는 테이블에 제한이 없습니다. 원본 데이터베이스가 MySQL용 Amazon RDS인 경우 동기화할 테이블에 기본 키가 있어야 합니다.
- 원본 데이터베이스 Binlog의 GTID에 hole이 있는 경우 동기화 작업의 성능에 영향을 미치고 작업이 실패할 수 있습니다.
- 동일한 트랜잭션에 DML 및 DDL 문을 모두 포함하는 시나리오는 지원되지 않으므로 작업 실행 중에 오류가 트리거됩니다.
- Geometry 데이터 유형은 지원되지 않으며 작업 실행 중에 오류를 트리거합니다.
- 'ALTER VIEW' 명령은 지원하지 않으며 이 명령을 만났을 때 작업 건너뛰기가 동기화되지 않습니다.

## 작업 제한
동기화 중에는 다음 작업을 수행하지 마십시오. 그렇지 않으면 동기화 작업이 실패합니다.
- 원본 및 타깃 데이터베이스와 포트 번호의 사용자 정보(사용자 이름, 암호 및 권한 포함)를 수정하거나 삭제하지 마십시오.
- 원본 데이터베이스에서 분산 트랜잭션을 실행하지 마십시오.
- `STATEMENT` 형식의 Binlog 데이터를 원본 데이터베이스에 쓰지 마십시오.
- 원본 데이터베이스에서 Binlog를 지우지 마십시오.
- 증분 동기화 중에 시스템 테이블 `__tencentdb__`를 삭제하지 마십시오. 

## 동기화 지원 SQL 작업

| 작업 유형 | SQL 문                                                |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE                                       |
| DDL      | CREATE DATABASE, DROP DATABASE, ALTER DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAEM TABLE, CREATE VIEW, DROP VIEW, CREATE INDEX, DROP INDEX<br><dx-alert infotype="explain" title="설명">파티션(Partition)과 관련된 DDL 문은 동기화할 수 없습니다.</dx-alert> |

## 환경 요건
<table>
<tr><th width="20%">유형</th><th width="80%">환경 요건</th></tr>
<tr>
<td>원본 데이터베이스 요구 사항</td>
<td>
<li>원본 및 타깃 데이터베이스를 연결할 수 있어야 합니다.</li>
<ul>
<li>데이터베이스 매개변수 요구 사항:
<ul>
<li>원본 데이터베이스의 server_id 매개변수는 수동으로 설정해야 하며 0이 될 수 없습니다.</li>
<li>원본 데이터베이스/테이블의 row_format은 FIXDE로 설정할 수 없습니다.</li>
<li>원본 및 대상 데이터베이스의 lower_case_table_names 변수 값은 동일해야 합니다.</li>
<li>원본 데이터베이스의 connect_timeout 변수는 10 이상이어야 합니다.</li></ul></li>
<li>Binlog 매개변수 요구사항:
<ul>
<li>원본 데이터베이스의 log_bin 변수는 ON으로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_format 변수는 ROW로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_row_image 변수는 FULL로 설정해야 합니다.</li>
<li>MySQL 5.6 이상에서 gtid_mode 변수가 ON이 아니면 알람이 트리거됩니다. gtid_mode를 활성화하는 것이 좋습니다.</li>
<li>do_db 및 ignore_db를 설정할 수 없습니다.</li>
<li>원본 데이터베이스가 세컨더리 데이터베이스인 경우 log_slave_updates 변수를 ON으로 설정해야 합니다.</li>
   <li>최소 3일 동안 원본 데이터베이스의 Binlog를 보관하는 것이 좋습니다. 그렇지 않으면 체크포인트에서 작업을 재개할 수 없으며 실패합니다.</li>
  </ul></li>
<li>외래 키 종속성:
<ul>
<li>외래 키 종속성은 NO ACTION 또는 RESTRICT 두 가지 유형 중 하나로만 설정할 수 있습니다.</li>
<li>부분 테이블 동기화 중에 외래 키 종속성이 있는 테이블을 마이그레이션해야 합니다.</li></ul></li></td></tr>
<tr> 
<td>타깃 데이터베이스에 대한 요구 사항</td>
<td>
<li>타깃 데이터베이스 버전은 원본 데이터베이스 버전보다 높거나 같아야 합니다.</li>
<li>대상 데이터베이스에는 충분한 저장 공간이 있어야 합니다. 초기화 유형으로 ‘전체 데이터 초기화’를 선택한 경우 대상 데이터베이스 공간은 원본 데이터베이스에서 동기화할 데이터베이스/테이블 공간의 1.2배 이상이어야 합니다.</li>
<li>대상 데이터베이스는 원본 데이터베이스에 있는 것과 동일한 이름을 가진 테이블 및 뷰와 같은 동기화 객체를 가질 수 없습니다.</li>
<li>타깃 데이터베이스의 max_allowed_packet 매개변수는 4M 이상으로 설정해야 합니다.</li></td></tr>
<tr> 
<td>기타 요구 사항</td>
<td>환경 변수 innodb_stats_on_metadata를 OFF로 설정해야 합니다.</td></tr>
</table>

## 작업 단계
이 시나리오의 작업 단계는 [MySQL 데이터를 MySQL로 동기화](https://intl.cloud.tencent.com/document/product/571/47344)의 단계와 동일하므로 MySQL 동기화 시나리오의 작업 단계를 참고하십시오.
