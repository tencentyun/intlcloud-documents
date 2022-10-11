본문은 DTS의 데이터 동기화 기능을 사용하여 MySQL, MariaDB, Percona에서 TencentDB for MySQL로 데이터를 동기화하는 방법을 설명합니다.

원본 데이터베이스에서 지원하는 배포 유형은 다음과 같습니다.

- 자체 구축 MySQL, 타사 클라우드 벤더 MySQL, TencentDB for MySQL.
- 자체 구축 MariaDB, TencentDB for MariaDB.
- 자체 구축 Percona.

MySQL, MariaDB 및 Percona는 TencentDB for MySQL과 동기화되기 때문에 세 시나리오의 동기화 요구 사항 및 작업 단계는 기본적으로 동일합니다. 이 장에서는 MySQL에서 MySQL로의 데이터 동기화를 예로 들어 설명합니다. 다른 시나리오의 경우 관련 내용을 참고하십시오.

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
- 원본 및 대상 데이터베이스와 포트 번호의 사용자 정보(사용자 이름, 암호 및 권한 포함)를 수정하거나 삭제하지 마십시오.
- 원본 데이터베이스에서 분산 트랜잭션을 실행하지 마십시오.
- `STATEMENT` 형식의 Binlog 데이터를 원본 데이터베이스에 쓰지 마십시오.
- 원본 데이터베이스에서 Binlog를 지우지 마십시오.
- 증분 동기화 중에 시스템 테이블 `__tencentdb__`를 삭제하지 마십시오. 

## 동기화 지원 SQL 작업

| 작업 유형 | SQL 문                                                |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE                                       |
| DDL      | CREATE DATABASE, DROP DATABASE, ALTER DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAEM TABLE, CREATE VIEW, DROP VIEW, CREATE INDEX, DROP INDEX<br/><dx-alert infotype="explain" title="설명">파티션(Partition)과 관련된 DDL 문은 동기화할 수 없습니다.</dx-alert> |

## 환경 요건
<table>
<tr><th width="20%">유형</th><th width="80%">환경 요건</th></tr>
<tr>
<td>원본 데이터베이스 요구 사항</td>
<td>
<li>원본 및 대상 데이터베이스를 연결할 수 있어야 합니다.</li>
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
<td>대상 데이터베이스에 대한 요구 사항</td>
<td>
<li>대상 데이터베이스 버전은 원본 데이터베이스 버전보다 높거나 같아야 합니다.</li>
<li>대상 데이터베이스에는 충분한 저장 공간이 있어야 합니다. 초기화 유형으로 ‘전체 데이터 초기화’를 선택한 경우 대상 데이터베이스 공간은 원본 데이터베이스에서 동기화할 데이터베이스/테이블 공간의 1.2배 이상이어야 합니다.</li>
<li>대상 데이터베이스는 원본 데이터베이스에 있는 것과 동일한 이름을 가진 테이블 및 뷰와 같은 동기화 객체를 가질 수 없습니다.</li>
<li>대상 데이터베이스의 max_allowed_packet 매개변수는 4M 이상으로 설정해야 합니다.</li></td></tr>
<tr> 
<td>기타 요구 사항</td>
<td>환경 변수 innodb_stats_on_metadata를 OFF로 설정해야 합니다.</td></tr>
</table>

## 작업 단계
1. [데이터 동기화 구매 페이지](https://buy.intl.cloud.tencent.com/replication)에 로그인하여 알맞은 설정을 선택하고 **구매하기**를 클릭합니다.
<table>
<thead><tr><th>매개변수</th><th>설명</th></tr></thead>
<tbody><tr>
<td>과금 방식</td><td>정액 과금제 및 사용량 과금이 지원됩니다.</td></tr>
<tr>
<td>원본 인스턴스 유형</td><td>MySQL을 선택합니다. 한 번 구성하면 변경할 수 없습니다.</td></tr>
<tr>
<td>원본 인스턴스 리전</td><td>원본 인스턴스 리전을 선택합니다. 구성한 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>대상 인스턴스 유형</td><td>MySQL을 선택합니다. 한 번 구성하면 변경할 수 없습니다.</td></tr>
<tr>
<td>대상 인스턴스 리전</td><td>대상 인스턴스 리전을 선택합니다. 한 번 구성되면 변경할 수 없습니다.</td></tr>
<tr>
<td>사양</td><td>비즈니스 요구 사항에 따라 사양을 선택하십시오. 사양이 높을수록 성능이 좋습니다.</td></tr>
</tbody></table>
2. 구매 성공 후 [데이터 동기화 목록](https://console.cloud.tencent.com/dts/replication)으로 돌아가면 새로 생성된 데이터 동기화 작업을 볼 수 있습니다. 사용하기 전에 설정해야 합니다.
3. 데이터 동기화 목록의 **작업** 열에서 **설정**을 클릭하여 동기화 작업 설정 페이지로 들어갑니다.
4. 동기화 작업 설정 페이지에서 원본 인스턴스와 대상 인스턴스를 설정하고 해당 계정 및 비밀번호를 설정한 뒤 연결성 테스트를 하고 **다음 단계**를 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ba534c6eff18421c8ea9fa1e640508d5.png"  style="zoom:80%;">
<br><b>원본 데이터베이스 배포 모드 및 액세스 유형의 교차 시나리오가 많기 때문에 다양한 시나리오에 대한 동기화 작업 단계는 유사합니다. 다음은 일반적인 시나리오에 대한 구성 예만 제공합니다. 다른 시나리오의 경우 예시를 참고하여 구성하십시오.</b>
<br><b>예시1</b>: 로컬 자체 구축 데이터베이스는 전용선/VPN을 통해 Tencent Cloud 데이터베이스와 동기화됩니다.
<table>
<thead><tr><th width="10%">설정 항목</th><th width="15%">매개변수</th><th width="75%">설명</th></tr></thead>
<tbody><tr>
<td rowspan=2>작업 설정</td>
<td>작업 이름</td>
<td>DTS는 사용자 정의할 수 있는 작업 이름을 자동으로 생성합니다.</td></tr>
<tr>
<td>실행 모드</td><td>즉시 실행 및 예약 실행이 지원됩니다.</td></tr>
<tr>
<td rowspan=10 >원본 Instance Settings</td>
<td>원본 인스턴스 유형</td>
<td>구매 시 선택한 원본 인스턴스 유형을 선택하며, 설정 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>원본 인스턴스 리전</td>
<td>구매 시 선택한 원본 인스턴스 리전을 선택합니다. 이 리전은 한 번 설정하면 변경할 수 없습니다.</td></tr>
<tr>
<td>서비스 제공자</td>
<td>자체 구축 데이터베이스(클라우드 서버에 자체 구축 포함) 또는 Tencent Cloud 데이터베이스는 ‘일반’을 선택하고 타사 클라우드 벤더 데이터베이스는 해당 서비스 제공 업체를 선택하십시오. <br>이 시나리오에서는 ‘일반’을 선택합니다.</td></tr>
<tr>
<td>액세스 유형</td>
<td>시나리오에 따라 선택하십시오. 이 시나리오에서는 ‘DC(Direct Connect)’ 또는 ‘VPN 액세스’를 선택합니다. 이 시나리오에서는 <a href="https://intl.cloud.tencent.com/document/product/571/42651">VPN과 IDC 간의 통신을 구성</a>해야 합니다. 다른 액세스 유형에 대한 준비 작업은 <a href="https://intl.cloud.tencent.com/document/product/571/42652">준비 작업 개요</a>를 참고하십시오.<ul>
<li>공용 네트워크: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.</li>
<li>CVM에서 자체 구축: 원본 데이터베이스가 <a href="https://intl.cloud.tencent.com/document/product/213">CVM 인스턴스</a>에 배포됩니다.</li>
<li>DC: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/216">DC</a>를 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>VPN 액세스: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1037">VPN 연결</a>을 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.</li>
<li>CCN: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>을 통해 VPC와 상호 연결될 수 있습니다. </li><li>VPC: 원본 및 대상 데이터베이스가 모두 Tencent Cloud <a href="https://intl.cloud.tencent.com/document/product/215">VPC</a>에 배포됩니다. VPC 액세스 유형을 사용해야 하는 경우 <a href="https://console.cloud.tencent.com/workorder/category">티켓을 제출</a>하여 신청하십시오.</li></ul></td></tr>
<tr>
<td>VPC 전용 게이트웨이/ VPN 게이트웨이</td><td>전용 게이트웨이 액세스 시 VPC 전용 게이트웨이만 지원됩니다. 게이트웨이 연결 네트워크 유형을 확인해 주십시오. <br>VPN 게이트웨이, VPN 게이트웨이를 통해 액세스한 VPN 게이트웨이 인스턴스를 선택하십시오. </td></tr>
<tr>
<td>VPC</td><td>VPC 전용 게이트웨이와 VPN 게이트웨이에 연결된 VPC 및 서브넷을 선택합니다. </td></tr>
<tr>
<td>호스트 주소</td><td>원본 MySQL 인스턴스에 액세스하기 위한 IP 주소 또는 도메인 이름입니다. </td></tr>
<tr>
<td>포트</td><td>원본 MySQL 인스턴스 액세스 포트.</td></tr>
<tr>
<td>계정</td><td>적절한 권한이 있는 원본 인스턴스 계정.</td></tr>
<tr>
<td>비밀번호</td><td>원본 인스턴스 계정의 비밀번호.</td></tr>
<tr>
<td rowspan=6>대상 인스턴스 설정</td>
<td>대상 인스턴스 유형</td><td>구매 시 선택한 대상 인스턴스 유형. 변경할 수 없습니다.</td></tr>
<tr>
<td>대상 인스턴스 리전</td><td>구매 시 대상 인스턴스 리전을 선택합니다. 설정 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>액세스 유형</td><td>시나리오에 따라 유형을 선택하십시오. 이 시나리오에서는 ‘데이터베이스’를 선택합니다.</td></tr>
<tr>
<td>인스턴스 ID</td><td>대상 인스턴스 ID.</td></tr>
<tr>
<td>계정</td><td>특정 권한이 있어야 하는 대상 인스턴스 계정입니다.</td></tr>
<tr>
<td>비밀번호</td><td>대상 인스턴스 계정의 비밀번호.</td></tr>
</tbody></table>
<b>예시2</b>: 두 TencentDB 인스턴스 간에 동기화
<table>
<thead><tr><th width="10%">설정 항목</th><th width="15%">매개변수</th><th width="75%">설명</th></tr></thead>
<tbody><tr>
<td rowspan=2>작업 설정</td>
<td>작업 이름</td>
<td>DTS는 사용자 정의할 수 있는 작업 이름을 자동으로 생성합니다.</td></tr>
<tr>
<td>실행 모드</td><td>즉시 실행 및 예약 실행이 지원됩니다.</td></tr>
<tr>
<td rowspan=7 >원본 인스턴스 설정</td>
<td>원본 인스턴스 유형</td>
<td>구매 시 선택한 원본 인스턴스 유형을 선택하며, 설정 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>원본 인스턴스 리전</td>
<td>구매 시 선택한 원본 인스턴스 리전을 선택합니다. 이 리전은 한 번 설정하면 변경할 수 없습니다.</td></tr>
<tr>
<td>서비스 제공자</td>
<td>자체 구축 데이터베이스(클라우드 서버에 자체 구축 포함) 또는 Tencent Cloud 데이터베이스는 ‘일반’을 선택하고 타사 클라우드 벤더 데이터베이스는 해당 서비스 제공 업체를 선택하십시오. <br>이 시나리오에서는 ‘일반’을 선택하십시오.</td></tr>
<tr>
<td>액세스 유형</td>
<td>시나리오에 따라 유형을 선택하십시오. 이 시나리오에서는 ‘데이터베이스’를 선택합니다. 다양한 액세스 유형에 대한 준비 작업은 <a href="https://intl.cloud.tencent.com/document/product/571/42652">준비 작업 개요</a>를 참고하십시오.<ul>
<li>공용 네트워크: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.</li>
<li>CVM에서 자체 구축: 원본 데이터베이스가 <a href="https://intl.cloud.tencent.com/document/product/213">CVM 인스턴스</a>에 배포됩니다.</li>
<li>DC: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/216">DC</a>를 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>VPN 액세스: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1037">VPN 연결</a>을 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.</li>
<li>CCN: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>을 통해 VPC와 상호 연결될 수 있습니다. </li><li>VPC: 원본 및 대상 데이터베이스가 모두 Tencent Cloud <a href="https://intl.cloud.tencent.com/document/product/215">VPC</a>에 배포됩니다. VPC 액세스 유형을 사용해야 하는 경우 <a href="https://console.cloud.tencent.com/workorder/category">티켓을 제출</a>하여 신청하십시오.</li></ul></td></tr>
<tr>
<td>인스턴스 ID</td><td>원본 인스턴스 ID입니다. <a href="https://console.cloud.tencent.com/cdb">인스턴스 리스트</a>에서 원본 인스턴스 정보를 볼 수 있습니다. </td></tr>
<tr>
<td>계정</td><td>적절한 권한이 있는 원본 인스턴스 계정.</td></tr>
<tr>
<td>비밀번호</td><td>원본 인스턴스 계정의 비밀번호.</td></tr>
<tr>
<td rowspan=6>대상 인스턴스 설정</td>
<td>대상 인스턴스 유형</td><td>구매 시 선택한 대상 데이터베이스 유형. 변경할 수 없습니다.</td></tr>
<tr>
<td>대상 인스턴스 리전</td><td>구매 시 대상 인스턴스 리전을 선택합니다. 설정 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>액세스 유형</td><td>시나리오에 따라 유형을 선택하십시오. 이 시나리오에서는 ‘데이터베이스’를 선택합니다.</td></tr>
<tr>
<td>인스턴스 ID</td><td>대상 인스턴스 ID.</td></tr>
<tr>
<td>계정</td><td>적절한 권한이 있는 대상 인스턴스 계정.</td></tr>
<tr>
<td>비밀번호</td><td>대상 인스턴스 계정의 비밀번호.</td></tr>
</tbody></table>
<b>예시3</b>: Alibaba Cloud RDS는 공용 네트워크를 통해 Tencent CDB와 동기화됩니다.
<table>
<thead><tr><th width="10%">설정 항목</th><th width="15%">매개변수</th><th width="75%">설명</th></tr></thead>
<tbody><tr>
<td rowspan=2>작업 설정</td>
<td>작업 이름</td>
<td>DTS는 사용자 정의할 수 있는 작업 이름을 자동으로 생성합니다.</td></tr>
<tr>
<td>실행 모드</td><td>즉시 실행 및 예약 실행이 지원됩니다.</td></tr>
<tr>
<td rowspan=8 >원본 데이터베이스 설정</td>
<td>원본 인스턴스 유형</td>
<td>구매 시 선택한 원본 인스턴스 유형을 선택하며, 설정 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>원본 인스턴스 리전</td>
<td>구매 시 선택한 원본 인스턴스 리전을 선택합니다. 이 리전은 한 번 설정하면 변경할 수 없습니다.</td></tr>
<tr>
<td>서비스 제공자</td>
<td>자체 구축 데이터베이스(클라우드 서버에 자체 구축 포함) 또는 Tencent Cloud 데이터베이스는 ‘일반’을 선택하고 타사 클라우드 벤더 데이터베이스는 해당 서비스 제공 업체를 선택하십시오. <br>이 시나리오에서는 ‘Alibaba Cloud’를 선택하십시오.</td></tr>
<tr>
<td>액세스 유형</td>
<td>타사 클라우드 데이터베이스의 경우 일반적으로 공용 네트워크를 선택하거나 실제 네트워크 조건에 따라 VPC 액세스, 직접 연결 또는 CCN을 선택할 수 있습니다. <br>이 시나리오에서는 ‘공용 네트워크’를 선택합니다. 다양한 액세스 유형에 대한 준비 작업은 <a href="https://intl.cloud.tencent.com/document/product/571/42652">준비 작업 개요</a>를 참고하십시오.<ul>
<li>공용 네트워크: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.</li>
<li>CVM에서 자체 구축: 원본 데이터베이스가 <a href="https://intl.cloud.tencent.com/document/product/213">CVM 인스턴스</a>에 배포됩니다.</li>
<li>DC: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/216">DC</a>를 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>VPN 액세스: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1037">VPN 연결</a>을 통해 VPC와 상호 연결될 수 있습니다.</li>
<li>데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.</li>
<li>CCN: 원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>을 통해 VPC와 상호 연결될 수 있습니다. </li><li>VPC: 원본 및 대상 데이터베이스가 모두 Tencent Cloud <a href="https://intl.cloud.tencent.com/document/product/215">VPC</a>에 배포됩니다. VPC 액세스 유형을 사용해야 하는 경우 <a href="https://console.cloud.tencent.com/workorder/category">티켓을 제출</a>하여 신청하십시오.</li></ul></td></tr>
<tr>
<td>호스트 주소</td><td>원본 인스턴스에 액세스하기 위한 IP 주소 또는 도메인 이름입니다. </td></tr>
<tr>
<td>포트</td><td>원본 인스턴스 포트.</td></tr>
<tr>
<td>계정</td><td>적절한 권한이 있는 원본 인스턴스 계정.</td></tr>
<tr>
<td>비밀번호</td><td>원본 인스턴스 계정의 비밀번호.</td></tr>
<tr>
<td rowspan=6>대상 인스턴스 설정</td>
<td>대상 인스턴스 유형</td><td>구매 시 선택한 대상 인스턴스 유형. 설정 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>대상 인스턴스 리전</td><td>구매 시 대상 인스턴스 리전을 선택합니다. 설정 후에는 변경할 수 없습니다.</td></tr>
<tr>
<td>액세스 유형</td><td>시나리오에 따라 유형을 선택하십시오. 이 시나리오에서는 ‘데이터베이스’를 선택합니다.</td></tr>
<tr>
<td>인스턴스 ID</td><td>대상 인스턴스 ID.</td></tr>
<tr>
<td>계정</td><td>적절한 권한이 있는 대상 인스턴스 계정.</td></tr>
<tr>
<td>비밀번호</td><td>대상 인스턴스 계정의 비밀번호.</td></tr>
</tbody></table>
5. 동기화 옵션 및 객체 설정 페이지에서 데이터 초기화, 데이터 동기화 및 객체 동기화 옵션을 설정하고 **저장 후 다음으로 이동**을 클릭합니다.
>?
>- **초기화 유형**에 대해 **전체 데이터 초기화**만 선택하는 경우 시스템은 기본적으로 대상 데이터베이스에 테이블 구조를 생성했다고 가정하고 테이블 구조를 동기화하거나 원본 및 대상 데이터베이스에 동일한 이름의 테이블이 있는지 여부를 확인하지 않습니다. 따라서 **대상이 이미 있는 경우**에 **사전 확인 및 오류 보고**를 선택하면 사전 확인 및 오류 보고 기능이 적용되지 않습니다.
>- **전체 데이터 초기화**만을 선택한 경우 대상 데이터베이스에 미리 테이블 구조를 생성해야 합니다.
>- 동기화하는 동안 테이블 이름을 rename하려면(예: table A를 table B로 rename) **동기화 객체**로 table A만 선택하는 것이 아니라 table A가 있는 전체 데이터베이스(또는 전체 인스턴스)를 선택해야 합니다. 그렇지 않으면 시스템에서 오류를 보고합니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/9d1e475f9684e2a37844d5a35ef6144f.png)
<table>
<thead><tr><th>설정 항목</th><th>매개변수</th><th>설명</th></tr></thead>
<tbody>
<tr>
<td rowspan=2>데이터 초기화 옵션</td>
<td>초기화 유형</td>
<td><ul><li>구조 초기화: 원본 인스턴스의 테이블 구조는 동기화 작업이 실행되기 전에 대상 인스턴스로 초기화됩니다.<li>전체 데이터 초기화: 원본 인스턴스의 데이터는 동기화 작업이 실행되기 전에 대상 인스턴스로 초기화됩니다. 두 옵션 모두 기본적으로 선택되어 있으며 필요에 따라 선택을 취소할 수 있습니다.</td></tr>
<tr>
<td>대상이 이미 있는 경우</td>
<td><ul><li>사전 확인 및 오류 보고: 동일한 이름의 테이블이 원본 및 대상 인스턴스에 모두 있는 경우 오류가 보고되고 작업이 중지됩니다.<li>무시 및 실행: 전체 및 증분 데이터가 대상 인스턴스의 테이블에 직접 추가됩니다.</td></tr>
<tr>
<td rowspan=2>데이터 동기화 옵션</td>
<td>충돌 해결 방법</td>
<td><ul><li>보고: 데이터 동기화 중 기본 키 충돌이 발견되면 오류가 보고되고 데이터 동기화 작업이 일시 중지됩니다.<li>무시: 데이터 동기화 중에 기본 키 충돌이 발견되면 대상 데이터베이스의 기본 키 레코드가 유지됩니다.<li>덮어쓰기: 데이터 동기화 중에 기본 키 충돌이 발견되면 원본 데이터베이스의 기본 키 레코드가 대상 데이터베이스의 기본 키 레코드를 덮어씁니다.</td></tr>
<tr>
<td>동기화 작업 유형</td><td>지원되는 작업: Insert, Update, Delete, DDL. 필요에 따라 다른 DDL 동기화 정책을 선택하려면 ‘DDL 사용자 지정’을 선택하십시오. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/571/47342">SQL 필터 정책 설정</a>을 참고하십시오.</td></tr>
<tr>
<td rowspan=2>동기화 객체 옵션</td>
<td>원본 인스턴스 DB 테이블 객체</td><td>동기화할 객체를 선택하고 기본 DB 테이블, 뷰, 저장 프로시저 및 함수를 지원합니다. <br>고급 객체 동기화는 일회성 작업입니다. 작업이 시작되기 전에 원본 데이터베이스의 고급 객체 동기화만 지원합니다. 작업이 시작된 후 새로 추가된 고급 객체는 대상 데이터베이스에 동기화되지 않습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/571/48487">고급 객체 동기화</a>를 참고하십시오.</td></tr>
<tr>
<td>선택된 객체</td><td><ul><li>DB 테이블 매핑 지원(DB 테이블 이름 변경), 데이베이스 이름과 테이블 이름 위에 마우스를 올리면 편집 버튼이 나타납니다. 클릭 후 팝업 창에서 새 이름을 입력할 수 있습니다. </li><li>동기화할 고급 객체를 선택할 때 DB 테이블의 이름 변경을 하지 않는 것이 좋습니다. 그렇지 않으면 고급 객체의 동기화가 실패할 수 있습니다. </li><li>Online DDL 임시 테이블 동기화를 지원(gh-ost, pt-online-schema-change 툴 사용)합니다. 테이블의 편집 버튼을 클릭하면 팝업 창에서 임시 테이블 이름을 선택할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/571/48486">Online DDL 임시 테이블 동기화</a>를 참고하십시오.</li></ul></td></tr>
</tbody></table>
6. 확인 작업 페이지에서 확인을 완료하고 모든 점검 항목이 통과되면 **작업 실행**을 클릭합니다.
    확인이 실패한 경우 [검증 불통과 처리 방법](https://intl.cloud.tencent.com/document/product/571/42551)의 설명 대로 문제를 수정하고 확인 작업을 다시 시작합니다.
 - 실패: 확인 항목 실패로 작업이 차단되었음을 나타냅니다. 문제를 수정하고 확인 작업을 다시 실행해야 합니다.
 - 알람: 확인 항목이 요구 사항을 완전히 충족하지 못함을 나타내며, 작업을 계속할 수 있지만 비즈니스에 영향을 미칩니다. 알람을 무시할지 아니면 문제를 해결하고 계속할지 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a4b270b55a1b389a0858c8ad921aeb3e.png)
7. 데이터 동기화 작업 리스트로 돌아가면 작업이 **실행 중** 상태가 됩니다.
>?**작업** 열에서 **더 보기** > **중지**를 클릭하여 동기화 작업을 중지할 수 있습니다. 작업을 중지하기 전에 데이터 동기화가 완료되었는지 확인해야 합니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c1f21ebe711d5df70789b6904fa27d8c.png)
8. (옵션) 작업 이름을 클릭하여 작업 상세 보기 페이지로 들어가면 작업 초기화 상태 및 모니터링 데이터를 확인할 수 있습니다.

