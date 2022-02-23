본문은 DTS의 데이터 마이그레이션 기능을 사용하여 MySQL에서 TDSQL for MySQL로 데이터를 마이그레이션하는 방법을 설명합니다.

## 주의 사항
- 전체 데이터 마이그레이션 중에 DTS는 특정 원본 데이터베이스 리소스를 사용하므로 원본 데이터베이스의 로드와 부담이 증가할 수 있습니다. 데이터베이스 사양이 낮으면 사용량이 적은 시간에 데이터를 마이그레이션하는 것이 좋습니다.
- 전체 마이그레이션은 잠긴 테이블로 구현되어 몇 초 동안 쓰기 작업이 차단됩니다.

## 전제 조건
- [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/1042/33336) 인스턴스를 생성해야 합니다.
- 원본 및 대상 데이터베이스는 [데이터 마이그레이션에서 지원하는 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42647)에 설명된 대로 마이그레이션 기능 및 버전에 대한 요구 사항을 충족해야 합니다.
- 모든 [준비 작업](https://intl.cloud.tencent.com/document/product/571/42652)을 마쳐야 합니다.
- 원본 MySQL 데이터베이스에 미리 `__tencentdb__` 데이터베이스를 생성해야 합니다.
- 원본 데이터베이스 권한이 있어야 합니다.
  - ‘전체 인스턴스’를 마이그레이션하려면 다음 계정 권한이 필요합니다.
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, CREATE ON `__tencentdb__`.* TO '마이그레이션 계정'@'%'; //원본 데이터베이스가 TencentDB 데이터베이스인 경우 `__tencentdb__` 권한 부여
GRANT SELECT ON *.* TO '마이그레이션 계정';
```
  - ‘지정된 객체’를 마이그레이션하려면 다음 계정 권한이 필요합니다.
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
GRANT INSERT, UPDATE, DELETE, DROP, SELECT, CREATE ON `__tencentdb__`.* TO '마이그레이션 계정'@'%'; //원본 데이터베이스가 TencentDB 데이터베이스인 경우 `__tencentdb__` 권한 부여
GRANT SELECT ON `mysql`.* TO '마이그레이션 계정'@'%';
GRANT SELECT ON 마이그레이션 예정 데이터베이스.* TO '마이그레이션 계정';
```
- 대상 데이터베이스에 필요한 권한: ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, DELETE, DROP, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, UPDATE.

## 제한
- 기본 테이블만 마이그레이션할 수 있으며 뷰, 함수, 트리거, 저장 프로시저와 같은 객체는 지원되지 않습니다.
- `information_schema`, `sys`, `performance_schema`, `__tencentdb__`, `mysql`을 포함한 시스템 데이터베이스/테이블 및 사용자 정보는 마이그레이션할 수 없습니다. 마이그레이션이 완료된 후 대상 데이터베이스의 보기, 저장 프로시저 또는 함수를 호출하려면 호출자에게 읽기/쓰기 권한을 부여해야 합니다. 
- 뷰 구조를 내보낼 때 대상 마이그레이션 계정의 user@host와 동일한 `definer`만 마이그레이션할 수 있습니다.
- 뷰 제한:
  - 원본 데이터베이스의 뷰는 전체 마이그레이션 중에 무시되고 마이그레이션되지 않습니다.
  - 원본 데이터베이스에서 생성된 뷰 DDL 작업은 증분 마이그레이션 중에 대상 데이터베이스의 첫 번째 샤드에서만 재생됩니다.
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
| 작업 유형 | 동기화 가능한 SQL 작업                                            |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE<br>VIEW: CREATE VIEW, DROP VIEW<br>INDEX: CREATE INDEX, DROP INDEX |

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
<td>환경 변수 innodb_stats_on_metadata는 off로 설정해야 합니다.</td></tr>
</table>

## 작업 단계
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 왼쪽 사이드바에서 **데이터 마이그레이션**을 선택한 다음 **마이그레이션 작업 생성**을 클릭하여 마이그레이션 작업 만들기 페이지로 들어갑니다.
2. 마이그레이션 작업 생성 페이지에서 대상 데이터베이스의 영역을 선택하고 **무료 평가판**을 클릭합니다. 현재 DTS 데이터 마이그레이션 기능은 무료입니다.
3. 원본과 대상 데이터베이스 설정 페이지에서 작업 설정, 원본 데이터베이스 설정 및 대상 데이터베이스 설정을 완료하고, 원본 데이터베이스와 대상 데이터베이스의 연결성 테스트 통과 시 **생성**을 클릭합니다.
>?연결 테스트가 실패하면 메시지가 표시됩니다. [문제 해결 가이드](https://intl.cloud.tencent.com/document/product/571/42552)의 지침에 따라 문제를 해결, 수정한 다음 다시 시도하십시오.
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
<td>태그는 다양한 각도에서 리소스를 분류하여 관리하는 데 사용됩니다. 기존의 태그가 사용자의 요구에 부합하지 않을 경우 콘솔에서 태그를 관리할 수 있습니다. </td></tr>
<tr>
<td rowspan=8>원본 데이터베이스 설정</td>
<td>원본 데이터베이스 유형</td><td>‘MySQL’을 선택합니다. </td></tr>
<tr>
<td>서비스 제공업체</td><td>‘일반’을 선택합니다. </td></tr>
<tr>
<td>액세스 유형</td><td>시나리오에 따라 유형을 선택하십시오. 본문은 ‘공용 네트워크’를 선택합니다.
<ul><li>공용 네트워크: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.</li>
<li>CVM에서 자체 구축: 원본 데이터베이스가 <a href="https://intl.cloud.tencent.com/document/product/213">CVM 인스턴스</a>에 배포됩니다.</li>
<li>DC: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/216">DC</a>를 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>VPN 액세스: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1037">VPN 연결</a>을 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.</li>
<li>CCN: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>을 통해 VPC와 상호 연결될 수 있습니다.</li></ul>다양한 액세스 유형에 대한 준비는 <a href="https://intl.cloud.tencent.com/document/product/571/42652">개요</a>를 참고하십시오.</td></tr>
<tr>
<td>소속 리전</td><td>원본 데이터베이스 소속 리전은 DTS 서비스 아웃바운드 리전입니다. 자체구축 인스턴스에서 가장 가까운 리전을 선택하십시오.</td></tr>
<tr>
<td>호스트 주소</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 IP 주소 또는 도메인 이름입니다. </td></tr>
<tr>
<td>포트</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 포트입니다.</td></tr>
<tr>
<td>계정</td><td>특정 권한이 있어야 하는 원본 MySQL 데이터베이스의 계정입니다.</td></tr>
<tr>
<td>비밀번호</td><td>원본 MySQL 데이터베이스의 비밀번호입니다.</td></tr>
<tr>
<td rowspan=6>대상 데이터베이스 설정</td>
<td>대상 데이터베이스 유형</td><td>‘TDSQL for MySQL’을 선택합니다. </td></tr>
<tr>
<td>액세스 유형</td><td>‘CDB’를 선택합니다. </td></tr>
<tr>
<td>소속 리전</td><td>이전 단계에서 선택한 리전입니다. </td></tr>
<tr>
<td>데이터베이스 인스턴스</td><td>대상 TDSQL for MySQL 인스턴스 ID를 선택합니다.</td></tr>
<tr>
<td>계정</td><td>대상 TDSQL for MySQL 데이터베이스 계정으로, 특정 권한이 있어야 합니다.</td></tr>
<tr>
<td>비밀번호</td><td>대상 TDSQL for MySQL 계정 비밀번호입니다.</td></tr>
</tbody></table>
4. 마이그레이션 옵션 설정 및 마이그레이션 객체 선택 페이지에서 마이그레이션 유형과 마이그레이션 객체를 설정하고 **저장**을 클릭합니다.
> ?
>- 마이그레이션 중에 테이블에 Online DDL 작업을 수행하기 위해 gh-ost 및 pt-osc와 같은 도구를 사용하려면, **마이그레이션 객체**로 테이블만 선택하는 것이 아니라 테이블이 있는 전체 데이터베이스(또는 전체 인스턴스)를 선택해야 합니다. 그렇지 않으면 Online DDL 변경으로 생성된 임시 테이블 데이터를 대상 데이터베이스로 마이그레이션할 수 없습니다.
>- 마이그레이션하는 동안 테이블 이름을 rename하려면(예: table A를 table B로 rename) **마이그레이션 객체**로 table A만 선택하는 것이 아니라 table A가 있는 전체 데이터베이스(또는 전체 인스턴스)를 선택해야 합니다. 그렇지 않으면 시스템에서 오류를 보고합니다.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/deb994f49499b1ce50a17098e4d6dcd0.png"  style="margin:0;">
<table>
<thead><tr><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>마이그레이션 유형</td>
<td>상황에 따라 선택하십시오.<ul><li>구조적 마이그레이션: 데이터베이스 및 데이터베이스의 테이블과 같은 구조화된 데이터가 마이그레이션됩니다.</li><li>전체 마이그레이션: 전체 데이터베이스가 마이그레이션됩니다.</li><li>전체 + 증분 마이그레이션: 전체 데이터베이스 및 후속 증분 데이터가 마이그레이션됩니다. 마이그레이션 중 데이터 쓰기가 있고 논스톱 방식으로 데이터를 원활하게 마이그레이션하려면 이 옵션을 선택합니다.</li></ul></td></tr>
<tr>
<td>객체 마이그레이션</td>
<td><ul><li>전체 인스턴스: information_schema, mysql, performance_schema 및 sys와 같은 시스템 데이터베이스를 제외한 전체 데이터베이스 인스턴스를 마이그레이션합니다.</li>
<li>지정된 객체: 지정된 객체를 마이그레이션합니다.</li></ul> </td></tr>
<tr>
<td>객체 지정</td>
<td>원본 데이터베이스 객체에서 마이그레이션할 객체를 선택하고 선택한 객체 상자로 이동합니다.</td></tr>
</tbody></table>
5. 확인 작업 페이지에서 확인을 진행하고 확인 통과 후 **작업 실행**을 클릭합니다.
확인이 실패한 경우 [확인 실패 수정](https://intl.cloud.tencent.com/document/product/571/42552) 설명 대로 문제를 수정하고 확인 작업을 다시 시작합니다.
 - 실패: 확인 항목 실패로 작업이 차단되었음을 나타냅니다. 문제를 수정하고 확인 작업을 다시 실행해야 합니다.
 - 알람: 확인 항목이 요구 사항을 완전히 충족하지 못함을 나타내며, 작업을 계속할 수 있지만 비즈니스에 영향을 미칩니다. 알람을 무시할지 아니면 문제를 해결하고 계속할지 선택합니다.
6. 데이터 마이그레이션 작업 리스트로 돌아가면 작업이 생성 중 상태가 되며, 1 - 2분 실행 후 데이터 마이그레이션 작업이 정상적으로 실행됩니다.
   - **구조적 마이그레이션** 또는 **전체 마이그레이션**을 선택합니다. 완료되면 작업이 자동 중지됩니다.
   - **전체 + 증분 마이그레이션** 선택: 전체 마이그레이션 완료 후 자동으로 증분 데이터 동기화를 진행하며, 증분 데이터 동기화는 자동 종료되지 않으므로 수동으로 **완료**를 클릭해 종료해야 합니다.
      - 증분 데이터 동기화를 수동으로 완료하고 비즈니스 전환을 수행할 적절한 시간을 선택합니다.
      - 마이그레이션 작업이 증분 동기화 단계에 있고 대기 시간이 없음을 알 수 있습니다. 몇 분 동안 원본 데이터베이스 쓰기를 중지하십시오.
      - 원본-대상 데이터베이스 데이터 간격이 0MB이고 원본-대상 데이터베이스 시간 지연이 0초인 경우 증분 동기화를 수동으로 완료합니다.      
7. (옵션) 작업 조회, 삭제 등 작업을 수행하려면 해당 작업을 클릭하고 **작업** 열에서 해당 작업을 선택합니다. 자세한 내용은 [작업 관리](https://intl.cloud.tencent.com/document/product/571/42637)를 참고하십시오.
8. 마이그레이션 작업 상태가 **작업 성공**이 되면 정식으로 컷오버할 수 있습니다. 자세한 내용은 [컷오버 개요](https://intl.cloud.tencent.com/document/product/571/42612)를 참고하십시오.

