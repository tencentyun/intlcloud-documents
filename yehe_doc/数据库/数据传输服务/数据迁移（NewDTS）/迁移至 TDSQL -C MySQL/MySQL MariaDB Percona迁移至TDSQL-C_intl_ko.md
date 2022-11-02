본문은 DTS의 데이터 마이그레이션 기능을 사용하여, MySQL, MariaDB, Percona에서 Tencent Cloud 네이티브 데이터베이스 TDSQL-C for MySQL로 데이터를 마이그레이션하는 방법을 설명합니다.

원본 데이터베이스의 다음 배포 모드가 지원됩니다.

- 자체 구축 MySQL, 타사 클라우드 벤더 MySQL, TencentDB for MySQL.
- 자체 구축 MariaDB, TencentDB for MariaDB.
- 자체 구축 Percona.

MySQL, MariaDB 및 Percona에서 데이터를 TDSQL-C for MySQL로 마이그레이션하기 때문에, 세 시나리오의 마이그레이션 요구 사항 및 작업 단계는 기본적으로 동일합니다. 이 장에서는 MySQL에서 TDSQL-C for MySQL로의 데이터 마이그레이션을 예로 들어 설명합니다. 다른 시나리오의 경우 관련 내용을 참고하십시오.

## 주의 사항

- 전체 데이터 마이그레이션을 진행할 때 DTS는 특정 원본 인스턴스 리소스를 사용하므로 원본 데이터베이스의 로드와 압력이 증가할 수 있습니다. 데이터베이스 구성이 낮으면 사용량이 적은 시간에 데이터를 동기화하는 것이 좋습니다.
- 마이그레이션은 기본적으로 잠금 없이 구현되며 이 동안에는 전역 잠금(FTWRL 잠금)이 원본 데이터베이스에 추가되지 않고 기본 키가 없는 테이블만 잠깁니다.
- [데이터 일관성 검증 생성](https://intl.cloud.tencent.com/document/product/571/42724) 시 DTS는 마이그레이션 작업을 실행하는 계정을 사용하여 원본 데이터베이스의 시스템 데이터베이스 `__tencentdb__`를 작성하여 마이그레이션 작업 중 데이터 대조 정보를 기록합니다.
  - 후속 데이터 문제를 찾을 수 있도록 원본 데이터베이스의 `__tencentdb__` 시스템 데이터베이스는 마이그레이션 작업이 끝난 후 삭제되지 않습니다.
  - `__tencentdb__`시스템 데이터베이스는 단일 스레드 연결 대기 메커니즘을 사용하며 원본 데이터베이스의 저장 공간의 약 0.01%–0.1%인 매우 작은 공간을 차지합니다. 예를 들어, 원본 데이터베이스가 50G인 경우 `__tencentdb__`는 약 5K-50K가 됩니다. 따라서 원본 데이터베이스의 성능에 거의 영향을 미치지 않으며 리소스를 선점하지 않습니다. 

## 전제 조건
- [TDSQL-C for MySQL 생성](https://intl.cloud.tencent.com/document/product/1102/41312)을 완료해야 합니다.
- 원본 및 대상 데이터베이스는 [데이터 마이그레이션 지원 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42647)에 설명된 대로 마이그레이션 기능 및 버전에 대한 요구 사항을 충족해야 합니다.
- 모든 [준비 작업](https://intl.cloud.tencent.com/document/product/571/42652)을 마쳐야 합니다.
- 원본 자체구축 MySQL에 마이그레이션 계정을 생성해야 하며, 다음과 같은 계정 권한이 필요합니다.
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW
DATABASES,SHOW VIEW,PROCESS ON *.* TO '마이그레이션 계정'@'%'; 
//원본이 Tencent Cloud MariaDB 데이터베이스인 경우 RELOAD 권한 부여를 위해 티켓을 제출해야 하며, 다른 시나리오의 경우 코드 인증을 참고하십시오
//원본 데이터베이스가 Alibaba CDB인 경우 SHOW DATABASES에 대한 권한 부여가 필요하지 않으며, 다른 시나리오는 권한 부여가 필요합니다. Alibaba 클라우드 데이터베이스 권한 부여는 https://help.aliyun.com/document_detail/96101.htmll을 참고하십시오
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO '마이그레이션 계정'@'%'; 
GRANT SELECT ON `mysql`.* TO '마이그레이션 계정'@'%';
```
- 부분 DB 테이블 마이그레이션: `GRANT SELECT ON 마이그레이션 예정 데이터베이스.* TO '마이그레이션 계정';`
- 전체 인스턴스 마이그레이션: `GRANT SELECT ON *.* TO '마이그레이션 계정';`
- 대상 데이터베이스 필요 권한: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, UPDATE.

## 애플리케이션 제한
- 기본 테이블 및 뷰만 마이그레이션할 수 있으며 함수, 트리거, 저장 프로시저와 같은 객체는 지원되지 않습니다.
- `information_schema`, `sys`, `performance_schema`, `__cdb_recycle_bin__`, `__recycle_bin__`, `__tencentdb__`, `mysql`을 포함한 시스템 DB 테이블은 마이그레이션할 수 없습니다.
- 뷰를 내보낼 때 DTS는 원본 데이터베이스의 `DEFINER`([DEFINER = user1])에 해당하는 user1이 마이그레이션 대상의 user2와 동일한지 확인하고, 동일하지 않은 경우 DTS는 대상 데이터베이스에 있는 user1의 `SQL SECURITY` 속성을 `DEFINER`에서 `INVOKER`([INVOKER = user1])로 변경하고 대상 데이터베이스의 `DEFINER`를 마이그레이션 대상의 user2로 설정합니다([DEFINER = 마이그레이션 대상 user2]). 원본 데이터베이스의 뷰 정의가 너무 복잡하면 작업이 실패할 수 있습니다.
- 원본 MySQL 데이터베이스가 비 GTID 데이터베이스인 경우 DTS는 이에 대한 HA 스위치를 지원하지 않습니다. 전환되면 DTS 증분 동기화가 중단될 수 있습니다.
- InnoDB, MyISAM 및 TokuDB 데이터베이스 엔진이 있는 데이터만 마이그레이션할 수 있습니다. 다른 데이터 테이블 엔진은 마이그레이션 중에 기본적으로 건너뜁니다.
- 연결된 데이터 객체는 함께 마이그레이션해야 합니다. 그렇지 않으면 마이그레이션이 실패합니다. 일반적인 연결 관계에는 뷰-참조 테이블, 뷰-뷰 참조, 기본/외래 키 연결 테이블 등이 포함됩니다.
- 증분 마이그레이션 중에 원본 데이터베이스에 분산 트랜잭션이 있거나 `STATEMENT` 형식의 Binlog문을 생성하면 마이그레이션이 실패됩니다.
- 잠금 없는 마이그레이션 시나리오에서 마이그레이션 작업 단계가 ‘원본 데이터베이스에서 내보내기’인 경우 DDL 작업은 지원되지 않습니다.
- 원본 데이터베이스 Binlog의 GTID에 hole이 있는 경우 마이그레이션 작업의 성능에 영향을 미치고 작업이 실패할 수 있습니다.
- 동일한 트랜잭션에 DML 및 DDL 문을 모두 포함하는 시나리오는 지원되지 않으므로 작업 실행 중에 오류가 트리거됩니다.
- Geometry 데이터 유형은 지원되지 않으며 작업 실행 중에 오류를 트리거합니다.
- `ALTER VIEW` 문은 지원되지 않으며 마이그레이션 중에 건너뜁니다.

## 작업 제한
- 마이그레이션하는 동안 다음 작업을 수행하지 마십시오. 그렇지 않으면 마이그레이션 작업이 실패합니다.
  - 원본 및 대상 데이터베이스와 포트 번호의 사용자 정보(사용자 이름, 암호 및 권한 포함)를 수정하거나 삭제하지 마십시오.
  - 원본 데이터베이스에서 분산 트랜잭션을 실행하지 마십시오.
  - `STATEMENT` 형식의 Binlog 데이터를 원본 데이터베이스에 쓰지 마십시오.
  - 원본 데이터베이스에서 Binlog를 지우지 마십시오.
  - 데이터베이스/테이블 구조 마이그레이션 또는 전체 마이그레이션 중에 데이터베이스/테이블 구조를 변경하는 DDL 작업을 실행하지 마십시오.
  - 증분 마이그레이션 중에 시스템 테이블 `__tencentdb__`를 삭제하지 마십시오. 
- 전체 데이터 마이그레이션만 수행하는 경우 마이그레이션 중에 원본 데이터베이스에 새 데이터를 쓰지 마십시오. 그렇지 않으면 원본 및 대상 데이터베이스의 데이터가 일치하지 않습니다. 데이터 쓰기가 있는 시나리오에서 실시간으로 데이터 일관성을 보장하려면 전체+증분 데이터 마이그레이션을 선택하는 것이 좋습니다.

## 지원되는 SQL 작업
| 작업 유형 | 지원되는 SQL 작업                                         |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAEM TABLE <br>VIEW: CREATE VIEW, DROP VIEW<br>INDEX: CREATE INDEX, DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, DROP DATABASE |

## 환경 요건
> ?시스템은 마이그레이션 작업을 시작하기 전에 다음 환경 요구 사항을 자동으로 확인하고 요구 사항이 충족되지 않으면 오류를 보고합니다. 실패 항목을 식별할 수 있는 경우 [확인 항목 요구 사항](https://intl.cloud.tencent.com/document/product/571/42551)에 따라 수정하십시오. 그렇지 않으면 시스템 확인이 완료될 때까지 기다렸다가 오류 메시지에 따라 문제를 수정하십시오.

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
<li>Binlog 매개변수 요구사항:
<ul>
<li>원본 데이터베이스의 log_bin 변수는 ON으로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_format 변수는 ROW로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_row_image 변수는 FULL로 설정해야 합니다.</li>
<li>MySQL 5.6 이상에서 gtid_mode 변수가 ON이 아니면 알람이 트리거됩니다. gtid_mode를 활성화하는 것이 좋습니다.</li>
<li>do_db 및 ignore_db로 필터 조건을 설정할 수 없습니다.</li>
<li>원본 데이터베이스가 세컨더리 데이터베이스인 경우 log_slave_updates 변수를 ON으로 설정해야 합니다.</li>
<li>최소 3일 동안 원본 데이터베이스의 Binlog를 보관하는 것이 좋습니다. 그렇지 않으면 체크포인트에서 작업을 재개할 수 없으며 실패합니다.</li>
</ul></li>
<li>외래 키 종속성:
<ul>
<li>외래 키 종속성은 NO ACTION 또는 RESTRICT 두 가지 유형 중 하나로만 설정할 수 있습니다.</li>
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
<td>환경 변수 innodb_stats_on_metadata를 OFF로 설정해야 합니다.</td></tr>
</table>

## 작업 단계
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 왼쪽 사이드바에서 **데이터 마이그레이션**을 선택한 다음 **마이그레이션 작업 생성**을 클릭하여 마이그레이션 작업 생성 페이지로 이동합니다.
2. 마이그레이션 작업 생성 페이지에서 원본 및 대상 인스턴스의 유형, 리전 및 사양을 선택하고 **구매하기**를 클릭합니다.
<table>
<thead><tr><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>원본 인스턴스 유형</td>
<td>원본 데이터베이스 유형을 선택합니다. 구매 후 변경할 수 없습니다. 이 시나리오에서는 ‘MySQL’을 선택합니다.</td></tr>
<tr>
<td>원본 인스턴스 리전</td>
<td>원본 데이터베이스 리전을 선택합니다. 원본 데이터베이스가 자체 구축된 데이터베이스인 경우 가장 가까운 리전을 선택하십시오.</td></tr>
<tr>
<td>대상 인스턴스 유형</td>
<td>대상 데이터베이스 유형을 선택합니다. 구매 후 변경할 수 없습니다. 이 시나리오에서는 ‘TDSQL-C for MySQL’을 선택합니다.</td></tr>
<tr>
<td>대상 인스턴스 리전</td>
<td>대상 데이터베이스 리전을 선택합니다.</td></tr>
<tr>
<td>사양</td>
<td>비즈니스 상황에 따라 마이그레이션 링크의 사양을 선택합니다.</td></tr>
</tbody></table>
3. 원본과 대상 데이터베이스 설정 페이지에서 작업 설정, 원본 데이터베이스 설정 및 대상 데이터베이스 설정을 완료하고, 원본 데이터베이스와 대상 데이터베이스의 연결성 테스트 통과 시 **생성**을 클릭합니다.
>?연결 테스트에 실패하면 [수정 방법](https://intl.cloud.tencent.com/document/product/571/42552)의 지침에 따라 문제를 해결하고 수정한 후 다시 시도하십시오.
<table>
<thead><tr><th width="15%">설정 유형</th><th width="15%">설정 항목</th><th width="70%">설명</th></tr></thead>
<tbody><tr>
<td rowspan=3>작업 설정</td>
<td>작업 이름</td>
<td>쉬운 작업 식별을 위해 의미 있는 이름을 설정합니다.</td></tr>
<tr>
<td>실행 모드</td>
<td>즉시 실행 및 예약 실행 지원: 즉시 실행은 작업 검증 통과 후 즉시 작업을 시작하고, 예약 실행은 작업 실행 시간을 설정하고 설정 시간이 되면 작업을 시작합니다.</td></tr>
<tr>
<td>태그</td>
<td>태그는 다양한 차원의 범주별로 리소스를 관리하는 데 사용됩니다. 기존 태그가 요구 사항을 충족하지 않는 경우 콘솔로 이동하여 추가로 생성하십시오.</td></tr>
<tr>
<td rowspan=8>원본 데이터베이스 설정</td>
<td>원본 데이터베이스 유형</td><td>구매 시 선택한 원본 데이터베이스 유형으로, 변경할 수 없습니다.</td></tr>
<tr>
<td>서비스 공급자</td><td>자체 구축 데이터베이스(예: CVM 기반 데이터베이스) 또는 TencentDB 데이터베이스의 경우 ‘일반’을 선택합니다. 타사 클라우드 데이터베이스의 경우 해당 서비스 공급자를 선택합니다. 이 시나리오에서는 ‘일반’(자체 구축 데이터베이스를 예로 들 수 있음)를 선택합니다.</td></tr>
<tr>
<td>리전</td><td>구매 시 선택한 원본 데이터베이스 리전으로, 변경할 수 없습니다.</td></tr>
 <tr>
<td>액세스 유형</td><td>시나리오에 따라 유형을 선택하십시오. 이 시나리오에서는 ‘공중망’을 선택합니다.
<ul><li>공중망: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.</li>
<li>CVM 기반 자체 구축: 원본 데이터베이스가 <a href="https://cloud.tencent.com/document/product/213">CVM 인스턴스</a>에 배포됩니다.</li>
<li>DC: 원본 데이터베이스는 <a href="https://cloud.tencent.com/document/product/216">Direct Connect</a> 방식을 통해 Tencent Cloud VPC와 상호 연결할 수 있습니다. 이 유형을 선택하는 경우 <a href="https://intl.cloud.tencent.com/document/product/571/42651">VPN과 IDC간 통신</a>을 구성해야 합니다.</li>
<li>VPN 액세스: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a> 방식을 통해 Tencent Cloud VPC와 상호 연결할 수 있습니다. 이 유형을 선택하는 경우 <a href="https://intl.cloud.tencent.com/document/product/571/42651">VPN과 IDC간 통신</a>을 구성해야 합니다.</li>
<li>데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.</li>
<li>CCN: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>을 통해 Tencent Cloud VPC와 상호 연결할 수 있습니다. 이 유형을 선택하는 경우 <a href="https://intl.cloud.tencent.com/document/product/571/42650">CCN을 통한 VPC와 IDC 간의 통신 연결</a>을 구성해야 합니다. </li></ul>타사 클라우드 벤더 데이터베이스의 경우 일반적으로 공중망 방식을 선택하거나 실제 네트워크 조건에 따라 VPN 액세스, 직접 연결 또는 CCN을 선택할 수 있습니다.</td></tr>
<tr>
<td>호스트 주소</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 IP 주소 또는 도메인 이름입니다. </td></tr>
<tr>
<td>포트</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 포트입니다.</td></tr>
<tr>
<td>계정</td><td>특정 권한이 있어야 하는 원본 MySQL 데이터베이스의 계정입니다.</td></tr>
<tr>
<td>비밀번호</td><td>원본 MySQL 데이터베이스의 비밀번호입니다.</td></tr>
<tr>
<td rowspan=6>대상 라이브러리 설정</td>
<td>대상 데이터베이스 유형</td><td>구매 시 선택한 대상 데이터베이스 유형으로, 변경할 수 없습니다.</td></tr>
<tr>
<td>리전</td><td>구매 시 선택한 대상 데이터베이스 리전으로, 변경할 수 없습니다.</td></tr>
<tr>
<td>액세스 유형</td><td>‘데이터베이스’를 선택합니다. </td></tr>
<tr>
<td>데이터베이스 인스턴스</td><td>대상 TDSQL-C for MySQL의 인스턴스 ID를 선택합니다.</td></tr>
<tr>
<td>계정</td><td>대상 TDSQL-C for MySQL 데이터베이스 계정으로, 적절한 권한이 있어야 합니다.</td></tr>
<tr>
<td>비밀번호</td><td>대상 TDSQL-C for MySQL의 데이터베이스 계정 비밀번호입니다.</td></tr>
</tbody></table>
4. 마이그레이션 옵션 설정 및 마이그레이션 객체 선택 페이지에서 마이그레이션 유형과 마이그레이션 객체를 설정하고 **저장**을 클릭합니다.
>?
>
>마이그레이션하는 동안 테이블 이름을 rename하려면(예: table A를 table B로 rename) **마이그레이션 객체**로 table A만 선택하는 것이 아니라 table A가 있는 전체 데이터베이스(또는 전체 인스턴스)를 선택해야 합니다. 그렇지 않으면 시스템에서 오류를 보고합니다.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/2d9b4d6316c079e7cee34c9d9102641b.png" style="zoom:67%;" />
<table>
<thead><tr><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>마이그레이션 유형</td>
<td><ul><li>구조적 마이그레이션: 데이터베이스 및 데이터베이스의 테이블과 같은 구조적 데이터가 마이그레이션됩니다. </li><li>전체 마이그레이션: 전체 데이터베이스가 마이그레이션됩니다. 마이그레이션된 데이터에는 작업 시작 시 원본 데이터베이스의 기존 데이터만 포함되며 작업 시작 후 원본 데이터베이스에 기록된 증분 데이터는 포함되지 않습니다. </li><li>전체 + 증분 마이그레이션: 마이그레이션된 데이터에는 작업 시작 시 원본 데이터베이스의 기존 데이터와 작업 시작 후 원본 데이터베이스에 기록된 증분 데이터가 포함됩니다. 마이그레이션 중 원본 데이터베이스에 데이터 쓰기가 있고 논스톱 방식으로 원활하게 데이터를 마이그레이션하려면 이 유형을 선택하십시오.</li></ul></td></tr>
<tr>
<td>객체 마이그레이션</td>
<td>모든 인스턴스를 마이그레이션해야 하는 경우, information_schema, mysql, performance_schema, sys와 같은 시스템 라이브러리를 제외한 모든 인스턴스를 선택하십시오. <br>지정 DB 테이블 마이그레이션 진행 시 지정 객체를 선택하십시오. </td></tr>
<tr>
<td>계정 마이그레이션</td>
<td>원본 데이터베이스의 계정 정보를 마이그레이션하려면 이 기능을 선택하십시오.</td></tr><tr>
<td>선택한 객체</td>
<td><ul><li>DB 테이블 매핑 지원(DB 테이블 이름 변경), 데이베이스 이름과 테이블 이름 위에 마우스를 올리면 편집 버튼이 나타납니다. 클릭 후 팝업 창에서 새 이름을 입력할 수 있습니다. </li><li>마이그레이션할 고급 객체를 선택할 때 DB 테이블의 이름 변경을 하지 않는 것이 좋습니다. 그렇지 않으면 고급 객체의 마이그레이션이 실패할 수 있습니다. </li><li>Online DDL 임시 테이블 마이그레이션을 지원(gh-ost, pt-online-schema-change 툴 사용)합니다. 테이블의 편집 버튼을 클릭하면 팝업 창에서 임시 테이블 이름을 선택할 수 있습니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/571/75889">Online DDL 임시 테이블 마이그레이션</a>을 참고하십시오.</li></ul></td></tr>
</tbody></table>
5. 확인 작업 페이지에서 확인을 진행하고 확인 통과 후 **작업 실행**을 클릭합니다.
 - 확인이 실패한 경우 [검증 불통과 처리 방법](https://intl.cloud.tencent.com/document/product/571/42551)의 설명 대로 문제를 수정하고 확인 작업을 다시 시작합니다.
    - 실패: 확인 항목 실패로 작업이 차단되었음을 나타냅니다. 문제를 수정하고 확인 작업을 다시 실행해야 합니다.
    - 알람: 확인 항목이 요구 사항을 완전히 충족하지 못함을 나타내며, 작업을 계속할 수 있지만 비즈니스에 영향을 미칩니다. 알람을 무시할지 아니면 문제를 해결하고 계속할지 선택합니다.
 - 계정 마이그레이션을 선택하면 원본 데이터베이스의 계정 정보를 확인합니다. 자세한 내용은 [계정 마이그레이션](https://cloud.tencent.com/document/product/571/65702)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/c18a641009300d8e765a4664ef7f3063.png)
6. 데이터 마이그레이션 작업 리스트로 돌아가면 작업이 생성 중 상태가 되며, 1 - 2분 실행 후 데이터 마이그레이션 작업이 정상적으로 실행됩니다.
 -  **구조 마이그레이션** 또는 **전체 마이그레이션** 선택: 완료되면 작업이 자동 중지됩니다.
 -  **전체 + 증분 마이그레이션** 선택: 전체 마이그레이션이 완료된 후 마이그레이션 작업은 자동으로 중지되지 않는 증분 데이터 동기화 단계에 자동으로 들어갑니다. 증분 데이터 동기화를 수동으로 중지하려면 **완료**를 클릭해야 합니다.
    - 적절한 시기에 증분 데이터 동기화 및 비즈니스 전환을 수동으로 완료합니다.
    - 마이그레이션 작업이 증분 동기화 단계에 있고 지연 상태가 아닌지 확인합니다. 그렇다면 몇 분 동안 원본 데이터베이스에 데이터 쓰기를 중지하십시오.
    - 대상-원본 데이터베이스 데이터 간격이 0MB이고 대상-원본 데이터베이스 시간 지연이 0초인 경우 증분 동기화를 수동으로 완료합니다.
7. (옵션) 작업 조회, 삭제 등 작업을 수행하려면 해당 작업을 클릭하고 **작업** 열에서 해당 작업을 선택합니다. 자세한 내용은 [작업 관리](https://intl.cloud.tencent.com/document/product/571/42637)를 참고하십시오.
8. 마이그레이션 작업 상태가 **작업 성공**이 되면 정식으로 컷오버할 수 있습니다. 자세한 내용은 [컷오버 설명](https://intl.cloud.tencent.com/document/product/571/42612)을 참고하십시오.


