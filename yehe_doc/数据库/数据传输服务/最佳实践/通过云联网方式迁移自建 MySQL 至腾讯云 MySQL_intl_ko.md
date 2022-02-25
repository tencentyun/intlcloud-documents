## 작업 시나리오

본문은 DTS의 데이터 마이그레이션 기능을 사용하여 CCN을 통해 자체 구축 데이터베이스에서 TencentDB 데이터베이스로 데이터를 마이그레이션하는 방법을 설명합니다.

CCN은 VPC를 다른 VPC 또는 로컬 IDC와 상호 연결할 수 있습니다. CCN 액세스를 사용하려면 미리 CCN을 통해 VPC 간 및 VPC-IDC 상호 연결을 설정해야 합니다.

이 시나리오에서는 CCN을 사용하여 vpc-Guangzhou, vpc-Nanjing 및 vpc-Shanghai의 세 네트워크를 상호 연결했으며 DTS를 통해 광저우 지역의 MySQL 데이터베이스를 대상 데이터베이스로 마이그레이션합니다. vpc-Nanjing 또는 vpc-Shanghai가 CCN과 연결된 VPC로 선택됩니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/5e1167c8de61fcc761e5681588732151.png" style="zoom:67%;" />

## 주의 사항 

- 전체 데이터 마이그레이션 중에 DTS는 원본 데이터베이스 리소스를 사용하므로 원본 데이터베이스의 로드와 부담이 증가할 수 있습니다. 데이터베이스 설정이 낮으면 사용량이 적은 시간에 데이터를 마이그레이션하는 것이 좋습니다.
- 전체 마이그레이션은 잠긴 테이블로 구현되어 몇 초 동안 쓰기 작업이 차단됩니다.

## 전제 조건

- [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/37785) 인스턴스를 생성해야 합니다.
- 원본 및 대상 데이터베이스는 [데이터 마이그레이션에서 지원하는 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42580)에 설명된 대로 마이그레이션 기능 및 버전에 대한 요구 사항을 충족해야 합니다.
- 모든 [준비 작업](https://intl.cloud.tencent.com/document/product/571/42652)을 마쳐야 합니다.
- 원본 데이터베이스에는 다음 권한이 있어야 합니다.
  - ‘전체 인스턴스’ 마이그레이션:
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO '마이그레이션 계정'@'%';  
GRANT SELECT ON *.* TO '마이그레이션 계정';
```
  - ‘지정 객체’ 마이그레이션:
```
CREATE USER ’마이그레이션 계정’@’%’ IDENTIFIED BY ’마이그레이션 비밀번호’;  
GRANT RELOAD,LOCK TABLES,REPLICATION CLIENT,REPLICATION SLAVE,SHOW DATABASES,SHOW VIEW,PROCESS ON *.* TO ’마이그레이션 계정’@’%’;  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO '마이그레이션 계정'@'%';  
GRANT SELECT ON `mysql`.* TO '마이그레이션 계정'@'%';
GRANT SELECT ON 마이그레이션 예정 데이터베이스.* TO '마이그레이션 계정';
```
- 대상 데이터베이스 필요 권한: ALTER, ALTER ROUTINE, CREATE,  CREATE ROUTINE, CREATE TEMPORARY TABLES,  CREATE USER,  CREATE VIEW,  DELETE,  DROP,  EVENT,  EXECUTE,  INDEX,  INSERT,  LOCK TABLES,  PROCESS,  REFERENCES,  RELOAD,  SELECT,  SHOW DATABASES,  SHOW VIEW,  TRIGGER,  UPDATE.

## 제한

- 기본 테이블 및 뷰만 마이그레이션할 수 있으며 함수, 트리거, 저장 프로시저와 같은 객체는 지원되지 않습니다.
- `information_schema`, `sys`, `performance_schema`, `__cdb_recycle_bin__`, `__recycle_bin__`, `__tencentdb__`, `mysql`을 포함한 시스템 데이터베이스/테이블 및 사용자 정보는 마이그레이션할 수 없습니다. 마이그레이션이 완료된 후 대상 데이터베이스의 보기, 저장 프로시저 또는 함수를 호출하려면 호출자에게 읽기/쓰기 권한을 부여해야 합니다. 
- 뷰를 내보낼 때 DTS는 원본 데이터베이스의 `DEFINER`([DEFINER = user1])에 해당하는 user1이 마이그레이션 대상의 user2와 동일한지 확인하고, 동일하지 않은 경우 DTS는 대상 데이터베이스에 있는 user1의 `SQL SECURITY` 속성을 `DEFINER`에서 `INVOKER`([INVOKER = user1])로 변경하고 대상 데이터베이스의 `DEFINER`를 마이그레이션 대상의 user2로 설정합니다([DEFINER = 마이그레이션 대상 user2]).
- 원본 MySQL 데이터베이스가 비 GTID 데이터베이스인 경우 DTS는 이에 대한 HA 스위치를 지원하지 않습니다. 전환되면 DTS 증분 동기화가 중단될 수 있습니다.
- InnoDB, MySIAM 및 TokuDB 데이터베이스 엔진이 있는 데이터만 마이그레이션할 수 있습니다. 다른 데이터 테이블 엔진은 마이그레이션 중에 기본적으로 건너뜁니다.
- 연결된 데이터 객체는 함께 마이그레이션해야 합니다. 그렇지 않으면 마이그레이션이 실패합니다. 일반적인 연결 관계에는 뷰-테이블 참조, 뷰-뷰 참조, 저장 프로시저/함수/트리거 뷰/테이블 참조, 기본/외래 키 연결 테이블이 포함됩니다.
- 증분 마이그레이션 중에 원본 데이터베이스에 분산 트랜잭션이 있거나 `STATEMENT` 형식의 Binlog문을 생성하면 마이그레이션이 실패됩니다.
- 잠금 없는 마이그레이션(원본 데이터베이스는 MySQL 5.6용 Alibaba Cloud ApsaraDB RDS, MySQL 5.6용 Alibaba Cloud PolarDB 또는 MySQL용 Amazon RDS이고 대상 데이터베이스는 MySQL용 TencentDB임)에서는 전체 마이그레이션 중에 DDL 작업이 지원되지 않습니다.

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
<li>MySQL 5.6 이상에서 gtid_mode 변수가 ON이 아니면 알람이 트리거됩니다. gtid_mode를 활성화하는 것이 좋습니다.</li>
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

#### CCN을 통한 네트워크 상호 연결 구성

[하나의 계정에서 네트워크 인스턴스 상호 연결](https://intl.cloud.tencent.com/document/product/1003/31986)의 지침에 따라 상호 연결을 설정합니다.

> ?CCN은 모든 리전 간에 10Kbps 미만의 대역폭만 무료로 제공합니다. 그러나 DTS에는 더 높은 대역폭이 필요합니다. 따라서 링크에서 대역폭 설정이 필요합니다.

#### DTS 마이그레이션 작업 설정
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 왼쪽 사이드바에서 **데이터 마이그레이션**을 선택한 다음 **마이그레이션 작업 생성**을 클릭하여 마이그레이션 작업 만들기 페이지로 들어갑니다.
2. 마이그레이션 작업 생성 페이지에서 대상 데이터베이스의 영역을 선택하고 **무료 평가판**을 클릭합니다. 현재 DTS 데이터 마이그레이션 기능은 무료입니다.
3. 원본과 대상 데이터베이스 설정 페이지에서 작업 설정, 원본 데이터베이스 설정 및 대상 데이터베이스 설정을 완료하고, 원본 데이터베이스와 대상 데이터베이스의 연결성 테스트 통과 시 **생성**을 클릭합니다.
>?연결 테스트가 실패하면 메시지가 표시됩니다. [문제 해결 가이드](https://intl.cloud.tencent.com/document/product/571/42552)의 지침에 따라 문제를 해결, 수정한 다음 다시 시도하십시오.
>
<table>
<thead><tr><th>설정 유형</th><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td rowspan=3>작업 설정</td>
<td>작업 이름</td>
<td>쉬운 작업 식별을 위해 의미 있는 이름을 설정합니다.</td></tr>
<tr>
<td>실행 모드</td>
<td>즉시 실행 및 예약 실행 지원: 즉시 실행은 작업 검증 통과 후 즉시 작업을 시작하고, 예약 실행은 작업 실행 시간을 설정하고 설정 시간이 되면 작업을 시작합니다. </td></tr>
<tr>
<td>태그</td>
<td>태그는 다양한 각도에서 리소스를 분류하여 관리하는 데 사용됩니다. 기존의 태그가 사용자의 요구에 부합하지 않을 경우 콘솔에서 태그를 관리할 수 있습니다. </td></tr>
<tr>
<td rowspan=9>원본 데이터베이스 설정</td>
<td>원본 데이터베이스 유형</td><td>‘MySQL’을 선택합니다. </td></tr>
<tr>
<td>서비스 제공자</td><td>‘기타’를 선택합니다.</td></tr>
<tr>
<td>액세스 유형</td><td>‘CCN’을 선택합니다. 액세스 유형에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/571/42652">준비 작업 개요</a>를 참고하십시오.</td></tr>
<tr>
<td>호스트 주소</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 IP 주소 또는 도메인 이름입니다. </td></tr>
<tr>
<td>포트</td><td>원본 MySQL 데이터베이스에 액세스하기 위한 포트입니다.</td></tr>
<tr>
<td>계정</td><td>특정 권한이 있어야 하는 원본 MySQL 데이터베이스의 계정입니다.</td></tr>
<tr>
<td>비밀번호</td><td>원본 MySQL 데이터베이스의 비밀번호입니다.</td></tr>
<tr>
<td>VPC 기반 CCN 인스턴스</td><td>VPC 기반 CCN 인스턴스만 지원됩니다. CCN과 연결된 네트워크 유형을 확인해야 합니다.</td></tr>
<tr>
<td>CCN 연결 VPC</td><td>네트워크 연결성을 보장하기 위해 반드시 다음 사항들을 확인하십시오.<br>선택한 CCN에 연결된 VPC와 소스 라이브러리 인스턴스의 호스트 서버 주소는 같은 리전에 있을 수 없으나, 소스 라이브러리가 자체구축 IDC의 MySQL인 경우에는 해당 사항을 고려하지 않아도 됩니다. <br>선택한 CCN에 연결된 VPC와 소스 라이브러리 인스턴스의 호스트 서버 주소는 같은 VPC에 있을 수 없습니다. 소스 라이브러리가 자체구축 IDC의 MySQL인 경우, 자체구축 IDC와 연결된 전용 게이트웨이가 있는 VPC와 선택한 VPC가 동일한 VPC일 수 없습니다. </td></tr>
<tr>
<td rowspan=6>대상 데이터베이스 설정</td>
<td>대상 데이터베이스 유형</td><td>‘MySQL’을 선택합니다. </td></tr>
<tr>
<td>액세스 유형</td><td>‘데이터베이스’를 선택합니다. </td></tr>
<tr>
<td>리전</td><td>이전 단계에서 선택한 리전을 선택합니다.</td></tr>
<tr>
<td>데이터베이스 인스턴스</td><td>대상 TencentDB 인스턴스 ID를 선택합니다.</td></tr>
<tr>
<td>계정</td><td>필요한 권한이 있어야 하는 대상 TencentDB의 계정입니다.</td></tr>
<tr>
<td>비밀번호</td><td>대상 TencentDB의 비밀번호입니다.</td></tr>
</tbody></table>
4. 마이그레이션 옵션 설정 및 마이그레이션 객체 선택 페이지에서 마이그레이션 유형과 마이그레이션 객체를 설정하고 **저장**을 클릭합니다.
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
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9b910b4d5cc7d3cc3c4bb0e44d1f408.png"  style="margin:0;">

5. 확인 작업 페이지에서 확인을 진행하고 확인 통과 후 **작업 실행**을 클릭합니다.
   확인이 실패한 경우 [확인 실패 수정](https://intl.cloud.tencent.com/document/product/571/42552) 설명 대로 문제를 수정하고 확인 작업을 다시 시작합니다.
 - 실패: 확인 항목 실패로 작업이 차단되었음을 나타냅니다. 문제를 수정하고 확인 작업을 다시 실행해야 합니다.
 - 알람: 확인 항목이 요구 사항을 완전히 충족하지 못함을 나타내며, 작업을 계속할 수 있지만 비즈니스에 영향을 미칩니다. 알람을 무시할지 아니면 문제를 해결하고 계속할지 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c63051d00dc78db93165a8ba0021eadd.png)
6. 데이터 마이그레이션 작업 리스트로 돌아가면 작업이 생성 중 상태가 되며, 1-2분 실행 후 데이터 마이그레이션 작업이 정상적으로 실행됩니다.
 - **구조적 마이그레이션** 또는 **전체 마이그레이션**을 선택합니다. 완료되면 작업이 자동 중지됩니다.
 - **전체 + 증분 마이그레이션** 선택: 전체 마이그레이션 완료 후 자동으로 증분 데이터 동기화를 진행하며, 증분 데이터 동기화는 자동 종료되지 않으므로 수동으로 **완료**를 클릭해 종료해야 합니다.
    - 증분 데이터 동기화를 수동으로 완료하고 비즈니스 전환을 수행할 적절한 시간을 선택합니다.
    - 마이그레이션 작업이 증분 동기화 단계에 있고 대기 시간이 없음을 알 수 있습니다. 몇 분 동안 원본 데이터베이스 쓰기를 중지하십시오.
    - 원본-대상 데이터베이스 데이터 간격이 0MB이고 원본-대상 데이터베이스 시간 지연이 0초인 경우 증분 동기화를 수동으로 완료합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1290cc971be591ff0a0c3b4cae9c167c.png)
7. (옵션) 작업 조회, 삭제 등 작업을 수행하려면 해당 작업을 클릭하고 **작업** 열에서 해당 작업을 선택합니다. 자세한 내용은 [작업 관리](https://intl.cloud.tencent.com/document/product/571/42637)를 참고하십시오.

### 비즈니스 컷오버(cut-over)

마이그레이션 작업 상태가 **작업 성공**이 되면 정식으로 컷오버할 수 있습니다. 자세한 내용은 [컷오버 개요](https://intl.cloud.tencent.com/document/product/571/42612)를 참고하십시오.

