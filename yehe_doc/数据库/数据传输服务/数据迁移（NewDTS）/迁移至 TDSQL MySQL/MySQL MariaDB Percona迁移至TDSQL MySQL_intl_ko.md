본문은 DTS의 데이터 마이그레이션 기능을 사용하여 MySQL, MariaDB, Percona에서 TDSQL for MySQL로 데이터를 마이그레이션하는 방법을 설명합니다.

지원되는 원본 데이터베이스 배포 유형은 다음과 같습니다.

- 자체 구축 MySQL, TencentDB for MySQL.
- 자체 구축 MariaDB, TencentDB for MariaDB.
- 자체 구축 Percona.

> ? TencentDB for MariaDB는 MariaDB, MySQL 및 Percona의 세 가지 커널을 지원합니다. 사용자는 사용할 때 커널을 구분할 필요가 없으며, 원본 데이터베이스가 Tencent Cloud MariaDB인 경우 원본 데이터베이스의 커널이 MariaDB, Percona 또는 MySQL인지 여부에 관계없이 원본 데이터베이스의 유형을 설정할 때 모두 MariaDB를 선택합니다.

본문은 MySQL에서 TDSQL for MySQL로 데이터를 마이그레이션하는 방법을 설명합니다. MariaDB 및 Percona에서 TDSQL for MySQL로의 데이터 마이그레이션 요구 사항 및 단계는 기본적으로 동일합니다.


## 주의 사항
- 전체 데이터 마이그레이션 중에 DTS는 특정 원본 인스턴스 리소스를 사용하므로 원본 데이터베이스의 로드와 압력이 증가할 수 있습니다. 데이터베이스 구성이 낮으면 사용량이 적은 시간에 데이터를 동기화하는 것이 좋습니다.
- 전체 마이그레이션은 테이블을 잠근 상태로 구현되며, 이 동안 쓰기 작업은 잠시 차단됩니다.
- [데이터 일관성 검증 생성](https://intl.cloud.tencent.com/document/product/571/42724) 시 DTS는 마이그레이션 작업을 실행하는 계정을 사용하여 원본 데이터베이스에 시스템 데이터베이스 `__tencentdb__`를 입력하여 마이그레이션 작업 중 데이터 대조 정보를 기록합니다.
  - 후속 데이터 문제를 찾을 수 있도록 원본 데이터베이스의 `__tencentdb__` 시스템 데이터베이스는 마이그레이션 작업이 끝난 후 삭제되지 않습니다.
  - `__tencentdb__`시스템 데이터베이스는 단일 스레드 연결 대기 메커니즘을 사용하며 원본 데이터베이스의 저장 공간의 약 0.01%–0.1%인 매우 작은 공간을 차지합니다. 예를 들어, 원본 데이터베이스가 50G인 경우 `__tencentdb__`는 약 5K-50K가 됩니다. 따라서 원본 데이터베이스의 성능에 거의 영향을 미치지 않으며 리소스를 선점하지 않습니다. 

## 전제 조건
- [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/1042/33336) 인스턴스를 생성해야 합니다.
- 원본 및 타깃 데이터베이스는 [데이터 마이그레이션 지원 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42647)에 설명된 대로 마이그레이션 기능 및 버전에 대한 요구 사항을 충족해야 합니다.
- 모든 [준비 작업](https://intl.cloud.tencent.com/document/product/571/42652)을 마쳐야 합니다.
- 원본 MySQL 데이터베이스에 미리 `__tencentdb__` 데이터베이스를 생성해야 합니다.
- 원본 데이터베이스 권한이 있어야 합니다.
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT SELECT,RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
//원본 데이터베이스가 TencentDB for MariaDB 데이터베이스인 경우 RELOAD를 승인하기 위해 티켓을 제출해야 합니다. 그렇지 않으면 예시 코드를 참고하여 권한을 부여할 수 있습니다.
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, INDEX, ALTER, CREATE ON `__tencentdb__`.* TO '마이그레이션 계정'@'%';
```
- 대상 데이터베이스에 필요한 권한: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, UPDATE(대상 데이터베이스가 TencentDB for MariaDB인 경우 RELOAD를 승인하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)해야 함).

## 제한
- 기본 테이블만 마이그레이션할 수 있으며 뷰, 함수, 트리거 및 저장 프로시저와 같은 객체는 마이그레이션할 수 없습니다.
- `information_schema`, `sys`, `performance_schema`, `__tencentdb__`, `mysql`을 포함한 시스템 데이터베이스/테이블 및 사용자 정보는 마이그레이션할 수 없습니다.
- InnoDB 데이터베이스 엔진이 있는 데이터만 마이그레이션할 수 있습니다. 다른 엔진이 있는 테이블은 기본적으로 마이그레이션 중에 건너뜁니다.
- 관련 데이터 객체는 동시에 마이그레이션되어야 합니다. 그렇지 않으면 마이그레이션이 실패합니다.
- 증분 마이그레이션 중에 원본 데이터베이스에 분산 트랜잭션이 있거나 `STATEMENT` 형식의 Binlog문을 생성하면 마이그레이션이 실패됩니다.
- 동일한 트랜잭션에 DML 및 DDL 문을 모두 포함하는 시나리오는 지원되지 않으므로 작업 실행 중에 오류가 트리거됩니다.
- Geometry 데이터 유형은 지원되지 않으며 작업 실행 중에 오류를 트리거합니다.

## 작업 제한
- 마이그레이션하는 동안 다음 작업을 수행하지 마십시오. 그렇지 않으면 마이그레이션 작업이 실패합니다.
  - 원본 및 타깃 데이터베이스와 포트 번호의 사용자 정보(사용자 이름, 암호 및 권한 포함)를 수정하거나 삭제하지 마십시오.
  - 원본 데이터베이스에서 분산 트랜잭션을 실행하지 마십시오.
  - `STATEMENT` 형식의 Binlog 데이터를 원본 데이터베이스에 쓰지 마십시오.
  - 원본 데이터베이스에서 Binlog를 지우지 마십시오.
  - 증분 마이그레이션 중에 시스템 테이블 `__tencentdb__`를 삭제하지 마십시오. 
- 전체 데이터 마이그레이션만 수행하는 경우 마이그레이션 중에 원본 데이터베이스에 새 데이터를 쓰지 마십시오. 그렇지 않으면 원본 및 대상 데이터베이스의 데이터가 일치하지 않습니다. 데이터 쓰기가 있는 시나리오에서 실시간으로 데이터 일관성을 보장하려면 전체+증분 데이터 마이그레이션을 선택하는 것이 좋습니다.

## 지원되는 SQL 작업
| 작업 유형 | 지원되는 SQL 작업                                         |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE<br>VIEW: CREATE VIEW, DROP VIEW<br>INDEX: CREATE INDEX, DROP INDEX<br>DATABASE: CREATE DATABASE, ALTER DATABASE, DROP DATABASE |

## 환경 요건
> ?시스템은 마이그레이션 작업을 시작하기 전에 다음 환경 요구 사항을 자동으로 확인하고 요구 사항이 충족되지 않으면 오류를 보고합니다. 실패 항목을 식별할 수 있는 경우 [확인 항목 요구 사항](https://intl.cloud.tencent.com/document/product/571/42551)에 따라 수정하십시오. 그렇지 않으면 시스템 확인이 완료될 때까지 기다렸다가 오류 메시지에 따라 문제를 수정하십시오.

<table>
<tr><th width="20%">유형</th><th width="80%">환경 요건</th></tr>
<tr>
<td>원본 데이터베이스 요구 사항</td>
<td>
<li>원본 및 타깃 데이터베이스를 연결할 수 있어야 합니다.</li>
<ul>
<li>데이터베이스 매개변수 요구 사항:
<ul>
<li>table_row_format은 FIXED로 설정할 수 없습니다.</li>
<li>원본 및 대상 데이터베이스의 lower_case_table_names 변수 값은 동일해야 합니다.</li>
<li>대상 데이터베이스의 max_allowed_packet 매개변수는 4M 이상이어야 합니다.</li>
<li>원본 데이터베이스의 connect_timeout 변수는 10 이상이어야 합니다.</li></ul></li>
<li>Binlog 매개변수 요구사항:
<ul>
<li>원본 데이터베이스의 binlog_format 변수는 ROW로 설정해야 합니다.</li>
<li>원본 데이터베이스의 log_bin 변수는 ON으로 설정해야 합니다.</li>
<li>원본 데이터베이스의 binlog_row_image 변수는 FULL로 설정해야 합니다.</li>
<li>v5.6 이상에서는 원본 데이터베이스의 gtid_mode 변수가 ON이 아닌 경우 WARNING이 발생합니다. gtid_mode를 활성화하는 것이 좋습니다.</li>
<li>do_db 및 ignore_db를 설정할 수 없습니다.</li>
<li>원본 데이터베이스가 세컨더리 데이터베이스인 경우 log_slave_updates 변수를 ON으로 설정해야 합니다.</li>
<li>최소 3일 동안 원본 데이터베이스의 Binlog를 보관하는 것이 좋습니다. 그렇지 않으면 체크포인트에서 작업을 재개할 수 없으며 실패합니다.</li>
</ul></li>
<li>외래 키 종속성:
<ul>
<li>외래 키 종속성은 no action 또는 restrict 유형일 수 있습니다.</li>
<li>부분 테이블 마이그레이션 중에는 외래 키 종속성이 있는 테이블을 마이그레이션해야 합니다.</li></ul></li></td></tr>
<tr> 
<td>타깃 데이터베이스에 대한 요구 사항</td>
<td>
<li>타깃 데이터베이스가 분산 데이터베이스인 경우 수동으로 분할된 테이블을 생성하고 shardkey를 미리 계획하는 것이 좋습니다. 그렇지 않으면 DTS는 원본 데이터베이스의 테이블 스타일을 기반으로 타깃 데이터베이스에 테이블을 만듭니다. 원본 데이터베이스가 독립 실행형 인스턴스인 경우 타깃 데이터베이스는 단일 테이블로 생성됩니다. </li><li>대상 데이터베이스 버전은 원본 데이터베이스 버전보다 높아야 합니다.</li>
<li>대상 데이터베이스의 공간은 원본 데이터베이스에서 마이그레이션할 테이블 크기의 1.2배 이상이어야 합니다.</li>
<li>대상 데이터베이스는 원본 데이터베이스와 충돌하는 테이블을 가질 수 없습니다.</li>
</td></tr>
<tr> 
<td>기타 요구 사항</td>
<td>환경 변수 innodb_stats_on_metadata는 off로 설정해야 합니다.</td></tr>
</table>

## 작업 단계
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 왼쪽 사이드바에서 **데이터 마이그레이션**을 선택한 다음 **마이그레이션 작업 생성**을 클릭하여 마이그레이션 작업 생성 페이지로 이동합니다.
2. 마이그레이션 작업 생성 페이지에서 원본 및 타깃 인스턴스의 유형, 리전 및 사양을 선택하고 **구매하기**를 클릭합니다.
<table>
<thead><tr><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>원본 인스턴스 유형</td>
<td>원본 데이터베이스 유형을 선택합니다. 구매 후 변경할 수 없습니다. 본 시나리오에서는 ‘MySQL’을 선택합니다.</td></tr>
<tr>
<td>원본 인스턴스 리전</td>
<td>원본 데이터베이스 리전을 선택합니다. 원본 데이터베이스가 자체 구축된 데이터베이스인 경우 가장 가까운 리전을 선택하십시오.</td></tr>
<tr>
<td>타깃 인스턴스 유형</td>
<td>타깃 데이터베이스 유형을 선택합니다. 구매 후 변경할 수 없습니다. 여기에서는 ‘TDSQL for MySQL’을 선택합니다.</td></tr>
<tr>
<td>타깃 인스턴스 리전</td>
<td>타깃 데이터베이스 리전을 선택합니다.</td></tr>
<tr>
<td>사양</td>
<td>비즈니스 상황에 따라 마이그레이션 링크의 사양을 선택합니다.</td></tr>
</tbody></table>
3. 원본과 타깃 데이터베이스 설정 페이지에서 작업 설정, 원본 데이터베이스 설정 및 타깃 데이터베이스 설정을 완료하고, 원본 데이터베이스와 타깃 데이터베이스의 연결성 테스트 통과 시 **생성**을 클릭합니다.
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
<td>서비스 공급자</td><td>자체 구축 데이터베이스(예: CVM 기반 데이터베이스) 또는 TencentDB 데이터베이스의 경우 ‘일반’을 선택하고 타사 클라우드 데이터베이스의 경우 해당 서비스 공급자를 선택하십시오. <br>이 시나리오에서는 ‘일반’을 선택합니다(로컬 자체 구축 데이터베이스를 예로 사용).</td></tr>
<tr>
<td>리전</td><td>구매 시 선택한 원본 데이터베이스 리전으로, 변경할 수 없습니다.</td></tr>
<tr>
<td>액세스 유형</td><td>시나리오에 따라 유형을 선택하십시오. 이 시나리오에서는 ‘공중망’을 선택합니다. 다양한 액세스 유형에 대한 준비 작업은 <a href="https://intl.cloud.tencent.com/document/product/571/42652">준비 작업 개요</a>를 참고하십시오.
<ul><li>공중망: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.</li>
<li>CVM에서 자체 구축: 원본 데이터베이스가 <a href="https://intl.cloud.tencent.com/document/product/213">CVM 인스턴스</a>에 배포됩니다.</li>
<li>DC: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/216">DC</a>를 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>VPN 액세스: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1037">VPN 연결</a>을 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.</li>
<li>CCN: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>을 통해 VPC와 상호 연결할 수 있습니다.</li></ul>타사 클라우드 데이터베이스의 경우 일반적으로 공중망을 선택하거나 실제 네트워크 조건에 따라 VPN, DC 또는 CCN을 선택할 수 있습니다.</td></tr>
<tr>
<td>호스트 주소</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 IP 주소 또는 도메인 이름입니다. </td></tr>
<tr>
<td>포트</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 포트입니다.</td></tr>
<tr>
<td>계정</td><td>특정 권한이 있어야 하는 원본 MySQL 데이터베이스의 계정입니다.</td></tr>
<tr>
<td>비밀번호</td><td>원본 MySQL 데이터베이스의 비밀번호입니다.</td></tr>
<tr>
<td rowspan=6>타깃 라이브러리 설정</td>
<td>타깃 데이터베이스 유형</td><td>구매 시 선택한 타깃 데이터베이스 유형으로, 변경할 수 없습니다.</td></tr>
<tr>
<td>리전</td><td>구매 시 선택한 타깃 데이터베이스 리전으로, 변경할 수 없습니다.</td></tr>
<tr>
<td>액세스 유형</td><td>‘데이터베이스’를 선택합니다. </td></tr>
<tr>
<td>데이터베이스 인스턴스</td><td>대상 TDSQL for MySQL 인스턴스 ID를 선택합니다.</td></tr>
<tr>
<td>계정</td><td>대상 TDSQL for MySQL 데이터베이스 계정으로, 적절한 권한이 있어야 합니다.</td></tr>
<tr>
<td>비밀번호</td><td>대상 TDSQL for MySQL 계정 비밀번호입니다.</td></tr>
</tbody></table>
4. 마이그레이션 옵션 설정 및 마이그레이션 객체 선택 페이지에서 마이그레이션 유형과 마이그레이션 객체를 설정하고 **저장**을 클릭합니다.
> ?
>- 마이그레이션 중에 테이블에 Online DDL 작업을 수행하기 위해 gh-ost 및 pt-osc와 같은 도구를 사용하려면, **마이그레이션 객체**로 테이블만 선택하는 것이 아니라 테이블이 있는 전체 데이터베이스(또는 전체 인스턴스)를 선택해야 합니다. 그렇지 않으면 Online DDL 변경으로 생성된 임시 테이블 데이터를 대상 데이터베이스로 마이그레이션할 수 없습니다.
>- 마이그레이션하는 동안 테이블 이름을 rename하려면(예: table A를 table B로 rename) **마이그레이션 객체**로 table A만 선택하는 것이 아니라 table A가 있는 전체 데이터베이스(또는 전체 인스턴스)를 선택해야 합니다. 그렇지 않으면 시스템에서 오류를 보고합니다.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/f37c15d20ebc26aaf535c3c0a3c404bb.png"  style="margin:0;">
<table>
<thead><tr><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>마이그레이션 유형</td>
<td>시나리오에 따라 유형을 선택하십시오. <ul><li>전체 마이그레이션: 전체 데이터베이스가 마이그레이션됩니다. 마이그레이션된 데이터는 작업이 시작될 때만 원본 데이터베이스의 기존 콘텐츠가 되지만 작업이 시작된 후 원본 데이터베이스에 기록된 증분 데이터는 포함되지 않습니다. </li><li>전체 + 증분 마이그레이션: 마이그레이션된 데이터에는 작업이 시작될 때 원본 데이터베이스의 기존 콘텐츠와 작업이 시작된 후 원본 데이터베이스에 기록된 증분 데이터가 포함됩니다. 마이그레이션 중에 원본 데이터베이스에 데이터 쓰기가 있고 논스톱 방식으로 원활하게 데이터를 마이그레이션하려면 이 옵션을 선택하십시오.</li></ul></td></tr>
<tr>
<td>객체 마이그레이션</td>
<td><ul><li>전체 인스턴스: information_schema, mysql, performance_schema 및 sys와 같은 시스템 데이터베이스를 제외한 전체 데이터베이스 인스턴스를 마이그레이션합니다.</li>
<li>지정된 객체: 지정된 객체를 마이그레이션합니다.</li></ul> </td></tr>
<tr>
<td>객체 지정</td>
<td>원본 데이터베이스 객체에서 마이그레이션할 객체를 선택하고 선택한 객체 상자로 이동합니다.</td></tr>
</tbody></table>
5. 확인 작업 페이지에서 확인을 진행하고 확인 통과 후 **작업 실행**을 클릭합니다.
확인이 실패한 경우 [확인 실패 해결 방법](https://intl.cloud.tencent.com/document/product/571/42551)의 설명 대로 문제를 수정하고 확인 작업을 다시 시작합니다.
 - 실패: 확인 항목 실패로 작업이 차단되었음을 나타냅니다. 문제를 수정하고 확인 작업을 다시 실행해야 합니다.
 - 알람: 확인 항목이 요구 사항을 완전히 충족하지 못함을 나타내며, 작업을 계속할 수 있지만 비즈니스에 영향을 미칩니다. 알람을 무시할지 아니면 문제를 해결하고 계속할지 선택합니다.
6. 데이터 마이그레이션 작업 리스트로 돌아가면 작업이 생성 중 상태가 되며, 1 - 2분 실행 후 데이터 마이그레이션 작업이 정상적으로 실행됩니다.
   -  **구조 마이그레이션** 또는 **전체 마이그레이션**을 선택: 완료되면 작업이 자동 중지됩니다.
   -  **전체 + 증분 마이그레이션** 선택: 전체 마이그레이션이 완료된 후 마이그레이션 작업은 자동으로 중지되지 않는 증분 데이터 동기화 단계에 자동으로 들어갑니다. 증분 데이터 동기화를 수동으로 중지하려면 **완료**를 클릭해야 합니다.
      - 적절한 시기에 증분 데이터 동기화 및 비즈니스 전환을 수동으로 완료합니다.
      - 마이그레이션 작업이 증분 동기화 단계에 있고 지연 상태가 아닌지 확인합니다. 그렇다면 몇 분 동안 원본 데이터베이스에 데이터 쓰기를 중지하십시오.
      - 타깃-원본 데이터베이스 데이터 간격이 0MB이고 타깃-원본 데이터베이스 시간 지연이 0초인 경우 증분 동기화를 수동으로 완료합니다.      
7. (옵션) 작업 조회, 삭제 등 작업을 수행하려면 해당 작업을 클릭하고 **작업** 열에서 해당 작업을 선택합니다. 자세한 내용은 [작업 관리](https://intl.cloud.tencent.com/document/product/571/42637)를 참고하십시오.
8. 마이그레이션 작업 상태가 **작업 성공**이 되면 정식으로 컷오버할 수 있습니다. 자세한 내용은 [컷오버 설명](https://intl.cloud.tencent.com/document/product/571/42612)을 참고하십시오.

