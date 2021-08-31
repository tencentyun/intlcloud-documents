본 문서에서는 DTS의 데이터 마이그레이션 기능을 통해 Alibaba Cloud RDS MySQL에서 TencentDB for MySQL로 데이터를 마이그레이션하는 것에 대해 소개합니다. DTS는 구조 마이그레이션, 전체 데이터 마이그레이션 및 증분 데이터 마이그레이션을 지원하며, 서비스를 중단하지 않고도 TencentDB for MySQL로 원활하게 데이터를 마이그레이션할 수 있습니다.

## [전제 조건](id:qttj)
- [TencentDB for MySQL 인스턴스 생성](https://intl.cloud.tencent.com/document/product/236/37785)이 완료되어 있어야 하며, MySQL 5.6, MySQL 5.7 버전이 지원되어야 합니다.
- 타깃 MySQL에 마이그레이션 계정을 생성해야 하며, 마이그레이션 예정 객체에 대한 모든 읽기 쓰기 권한 등 계정 권한이 필요합니다.
마이그레이션 예정인 소스 Alibaba Cloud RDS MySQL은 공용 네트워크를 통해 액세스할 수 있습니다. Alibaba Cloud RDS MySQL의 가용성을 공개로 설정해야 하며, MySQL 5.6, MySQL 5.7 버전을 지원해야 합니다.
- 소스 Alibaba Cloud RDS MySQL에 마이그레이션 계정을 생성해야 하며, 다음과 같은 계정 권한이 필요합니다.
```
CREATE USER ‘마이그레이션 계정’@‘%’ IDENTIFIED BY ‘마이그레이션 비밀번호’;  
GRANT RELOAD, LOCK TABLES, REPLICATION CLIENT, REPLICATION SLAVE, SHOW VIEW, PROCESS ON *.* TO ‘마이그레이션 계정’@‘%’;  
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO ‘마이그레이션 계정’@‘%’;  
GRANT SELECT ON `mysql`.* TO ‘마이그레이션 계정’@‘%’;
```
- 부분 DB 테이블 마이그레이션: `GRANT SELECT ON 마이그레이션 예정 데이터베이스.* TO ‘마이그레이션 계정’;`
- 전체 인스턴스 마이그레이션: `GRANT SELECT ON *.* TO ‘마이그레이션 계정’;`

## 주의 사항
- DTS가 전체 데이터 마이그레이션을 진행할 때 일정 원본 인스턴스 리소스를 점유함으로써 원본 인스턴스 부하가 높아져 데이터베이스 자체의 부담이 가중될 수 있습니다. 데이터베이스의 사양이 낮을 경우 서비스 사용량이 적은 시간대에 마이그레이션하는 것을 권장합니다.
- 소스 MySQL 중 마이그레이션 예정인 테이블은 기본 키가 있는 테이블만 지원합니다. 잠금 없는 마이그레이션으로 전체 데이터 마이그레이션 과정을 구현함으로써 전체 마이그레이션 과정에서 쓰기 작업을 방해하지 않아 비즈니스에 많은 영향을 미치지 않습니다. 데이터 마이그레이션을 시작하기 전에 소스 데이터 테이블에 기본 키를 추가할 것을 권장합니다.
- 전체 데이터의 잠금 없는 마이그레이션 중에 DDL 작업이 발생하는 경우, 마이그레이션에 실패할 수 있으니 DTS 전체 데이터 마이그레이션 중에는 DDL 작업을 하지 마십시오.
- TencentDB for MySQL의 스토리지 용량은 반드시 소스 Alibaba Cloud RDS MySQL 데이터베이스가 점유한 스토리지 용량의 1.2배 이상이어야 합니다.
- 소스 Alibaba Cloud RDS MySQL이 GTID 인스턴스가 아닌 경우, DTS가 원본 HA(Highly Available) 전환을 지원하지 않아 소스 RDS MySQL에 전환 발생 시 DTS 증분 동기화가 중단될 수 있습니다.

## 지원하는 마이그레이션 유형
- 구조 마이그레이션: DTS는 마이그레이션 객체의 구조 정의를 타깃 인스턴스로 마이그레이션하는 것을 지원하며, 현재 DTS가 구조 마이그레이션을 지원하는 객체로는 데이터베이스, 데이터 테이블, 뷰가 있습니다.
- 전체 마이그레이션: DTS는 소스 MySQL 데이터베이스 마이그레이션 객체의 모든 데이터를 타깃 TencentDB for MySQL로 마이그레이션하는 것을 지원합니다.
- 증분 동기화: DTS는 전체 데이터 마이그레이션을 바탕으로 소스 Alibaba Cloud RDS MySQL 데이터베이스의 binlog 정보를 읽어와 분석하고, 소스 Alibaba Cloud RDS MySQL의 증분 업데이트를 타깃 CVM MySQL로 동기화합니다. 증분 데이터 동기화를 통해 서비스를 중단하지 않고 애플리케이션을 Tencent Cloud로 원활하게 마이그레이션할 수 있습니다.

## 증분 동기화 지원 가능 SQL 작업
| 작업 유형 | 동기화 가능한 SQL 작업                                            |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, DELETE, REPLACE                              |
| DDL      | TABLE: CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, RENAEM TABLE <br>VIEW: CREATE VIEW, ALTER VIEW, DROP VIEW<br>INDEX: CREATE INDEX, DROP INDEX <br>DATABASE: CREATE DATABASE, ALTER DATABASE, DROP DATABASE |

## 사전 점검
데이터 마이그레이션 작업 시작 전에 사전 점검을 진행해야 하며, 점검 내용 및 점검 포인트는 다음과 같습니다.

| 점검 내용             | 점검 포인트                                                       |
| -------------------- | ------------------------------------------------------------ |
| 연결 데이터베이스 점검           | 소스 라이브러리와 타깃 라이브러리를 연결할 수 있습니다.                                     |
| 주변 점검             | 환경 변수를 점검합니다. innodb_stats_on_metadata=off                     |
| 버전 점검             | 소스 라이브러리와 타깃 라이브러리의 MySQL 버전은 5.6, 5.7이어야 하며, 소스 라이브러리의 버전은 타깃 라이브러리와 같거나 낮은 버전이어야 합니다. |
| 일부 인스턴스 매개변수 점검     | table_row_format이 Fixed가 아니어야 하며<br>소스 라이브러리와 타깃 라이브러리의 lower_case_table_names 변수가 반드시 일치해야 하고<br>타깃 max_allowed_packet 매개변수가 최소 4M인지 확인해야 하며<br>소스 라이브러리 변수의 connect_timeout은 반드시 10 이상이어야 합니다. |
| 소스 권한 점검       |  [전제 조건](#qttj)의 계정 권한과 동일해야 합니다.                                     |
| 타깃 권한 점검    | 타깃 TencentDB for MySQL의 계정은 다음과 같은 권한이 필요합니다. ALTER,  ALTER ROUTINE,  CREATE,  CREATE ROUTINE,  CREATE TEMPORARY TABLES,  CREATE USER,  CREATE VIEW,  DELETE,  DROP,  EVENT,  EXECUTE,  INDEX,  INSERT,  LOCK TABLES,  PROCESS,  REFERENCES,  RELOAD,  SELECT,  SHOW DATABASES,  SHOW VIEW,  TRIGGER,  UPDATE |
| 타깃 인스턴스 내용 충돌 확인 | 타깃 라이브러리에 소스 라이브러리와 충돌하는 DB 테이블이 없어야 합니다.                                 |
| 타깃 인스턴스 용량 점검     | 타깃 라이브러리 용량은 소스 라이브러리의 마이그레이션 예정 DB 테이블 용량의 1.2배 이상이어야 합니다. |
| Binlog 매개변수 점검       | 원본 binlog_format 변수가 ROW여야 하며<br>원본 log_bin 변수는 ON이어야 하고<br>원본 binlog_row_image 변수는 FULL이고<br>원본 gtid_mode 변수가 5.6 이상의 버전에서 ON이 아닐 경우, WARNING 알림이 발생할 수 있으므로 gtid_mode를 켜는 것이 좋으며<br>do_db, ignore_db를 설정할 수 없습니다.<br>원본 인스턴스가 슬레이브 데이터베이스인 경우, log_slave_updates 변수는 ON이어야 합니다.|
| 외래 키 종속 점검         | 외래 키 종속은 no action과 restrict의 두 가지 유형만 가능하며<br>일부 DB 테이블의 마이그레이션 시 외래 키 종속성이 있는 테이블은 반드시 모두 마이그레이션해야 합니다. |
| 뷰 점검             | 마이그레이션 타깃 user@host와 동일한 definer만 허용됩니다.                       |
| 기타 경고 항목 점검       | 소스 라이브러리와 타깃 라이브러리의 max_allowed_packet을 확인해 소스 라이브러리가 타깃 라이브러리보다 크면 경고가 발생하고<br>타깃 라이브러리의 max_allowed_packet이 1GB 미만이면 경고가 발생합니다.<br>소스 라이브러리와 타깃 라이브러리의 문자 세트가 일치하지 않을 경우에도 경고가 발생합니다.<br>전체 마이그레이션(증분 없음) 시 경고를 통해 사용자에게 이러한 잠김 없는 전체 마이그레이션의 경우 데이터 일관성을 보장할 수 없음을 공지합니다. |
| 테이블의 기본 키 유무 검사         | MySQL 5.6 마이그레이션 예정 테이블에는 반드시 기본 키가 있어야 하나, MySQL 5.7 등 다른 버전의 경우 이러한 제한이 없습니다.                  |

## 작업 순서
1. [DTS 데이터 마이그레이션 콘솔](https://console.cloud.tencent.com/dts/migration?rid=8&page=1&pagesize=20)에 로그인한 뒤 [마이그레이션 작업 생성]을 클릭해 신규 마이그레이션 작업 생성 페이지로 이동합니다.
2. 신규 마이그레이션 작업 생성 페이지에서 마이그레이션의 타깃 인스턴스 소재 리전을 선택하고 [0USD 구매]를 클릭하면 DTS 데이터 마이그레이션 기능을 무료로 이용하실 수 있습니다.
3. 소스와 타깃 데이터베이스 설정 페이지에서 작업 설정, 소스 라이브러리 설정 및 타깃 라이브러리 설정을 완료하고, 소스 라이브러리와 타깃 라이브러리의 연결성 테스트를 통과하면 [생성]을 클릭합니다.
>?연결성 테스트에 실패한 경우 알림에 따라 문제를 확인하고 해결한 뒤 재시도 하십시오.
>
<table>
<thead><tr><th>설정 유형</th><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td rowspan=3>작업 설정</td>
<td>작업 이름</td>
<td>작업을 쉽게 식별할 수 있도록 서비스 의미를 내포한 이름 설정</td></tr>
<tr>
<td>실행 모드</td>
<td>즉시 실행 및 예약 실행 지원: 즉시 실행은 작업 검증 통과 후 즉시 작업을 시작하고, 예약 실행은 작업 실행 시간을 설정하고 설정 시간이 되면 작업을 시작합니다. </td></tr>
<tr>
<td>태그</td>
<td>태그는 다양한 각도에서 리소스를 분류하여 관리하는 데 사용됩니다. 기존의 태그가 사용자의 요구에 부합하지 않을 경우 콘솔에서 태그를 관리할 수 있습니다. </td></tr>
<tr>
<td rowspan=9>소스 라이브러리 설정</td>
<td>소스 라이브러리 유형</td><td>‘MySQL’을 선택합니다. </td></tr>
<tr>
<td>서비스 제공업체</td><td>‘Alibaba Cloud’를 선택합니다. </td></tr>
<tr>
<td>데이터베이스 버전	</td><td>RDS 5.6 또는 RDS 5.7을 선택합니다. </td></tr>
<tr>
<td>액세스 유형</td><td>‘공용 네트워크’를 선택합니다. </td></tr>
<tr>
<td>소속 리전</td><td>소스 라이브러리 소속 리전은 DTS 서비스 아웃바운드 리전입니다. Alibaba Cloud RDS MySQL에서 가장 가까운 리전을 선택하십시오. </td></tr>
<tr>
<td>호스트 주소</td><td>Alibaba Cloud RDS MySQL 액세스 IP 주소로, Alibaba Cloud RDS MySQL의 기본 정보 페이지에서 데이터베이스의 액세스 주소를 얻을 수 있습니다. </td></tr>
<tr>
<td>포트</td><td>Alibaba Cloud RDS MySQL 액세스 포트로, 기본값은 3306입니다. </td></tr>
<tr>
<td>계정</td><td>Alibaba Cloud RDS MySQL의 데이터베이스 계정으로, 계정 권한이 요구에 부합해야 합니다. </td></tr>
<tr>
<td>비밀번호</td><td>Alibaba Cloud RDS MySQL의 데이터베이스 계정의 비밀번호입니다. </td></tr>
<tr>
<td rowspan=6>타깃 라이브러리 설정</td>
<td>타깃 라이브러리 유형</td><td>‘MySQL’을 선택합니다. </td></tr>
<tr>
<td>액세스 유형</td><td>‘CDB’를 선택합니다. </td></tr>
<tr>
<td>소속 리전</td><td>이전 단계에서 선택한 리전입니다. </td></tr>
<tr>
<td>데이터베이스 인스턴스</td><td>타깃 CDB 인스턴스 ID를 선택합니다. </td></tr>
<tr>
<td>계정</td><td>타깃 CDB 데이터베이스 계정으로, 계정 권한이 요구에 부합해야 합니다. </td></tr>
<tr>
<td>비밀번호</td><td>타깃 CDB 데이터베이스 계정의 비밀번호입니다. </td></tr>
</tbody></table>
4. 마이그레이션 옵션 설정 및 마이그레이션 객체 선택 페이지에서 마이그레이션 유형과 마이그레이션 객체를 설정하고 [저장]을 클릭합니다.
<table>
<thead><tr><th>설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>마이그레이션 유형</td>
<td>구조 마이그레이션만 진행하는 경우, 구조 마이그레이션을 선택하십시오. <br>데이터 전체 마이그레이션만 진행하는 경우, 전체 마이그레이션을 선택하십시오. <br>시스템 다운 없이 원활한 마이그레이션을 진행해야 하는 경우, 전체+증분 마이그레이션을 선택하십시오. </td></tr>
<tr>
<td>객체 마이그레이션</td>
<td>모든 인스턴스를 마이그레이션해야 하는 경우, information_schema, mysql, performance_schema, sys와 같은 시스템 라이브러리를 제외한 모든 인스턴스를 선택하십시오. <br>지정 DB 테이블 마이그레이션 진행 시 지정 객체를 선택하십시오. </td></tr>
<tr>
<td>객체 지정</td>
<td>소스 라이브러리 객체 중 마이그레이션을 진행할 객체를 선택한 뒤 해당 객체를 선택한 객체 상자로 이동합니다. </td></tr>
</tbody></table>

5. 검증 작업 페이지에서 검증을 진행하고 검증을 통과한 후 [작업 실행]을 클릭합니다.
 -  검증 작업 통과 후 선택한 실행 모드에 따라 마이그레이션 작업을 실행합니다.
 -  검증 작업이 통과되지 않은 경우 구체적인 검사 항목과 실패 원인을 확인하고 문제를 해결한 뒤 다시 검증 작업을 진행합니다.
6. 데이터 마이그레이션 작업 리스트로 돌아가면 작업이 생성 중 상태가 되며, 1-2분 실행 후 데이터 마이그레이션 작업이 정상적으로 실행됩니다.
 - 구조 마이그레이션 + 전체 마이그레이션 작업: 작업 완료 후 자동 종료되며, 작업을 취소해야 하는 경우가 아니라면 수동으로 종료하지 마십시오. 수동 종료 시 마이그레이션 데이터가 손실될 수 있습니다.
 - 전체 마이그레이션 + 증분 마이그레이션 작업: 전체 마이그레이션 완료 후 자동으로 증분 데이터 동기화를 진행하며, 증분 데이터 동기화는 자동 종료되지 않으므로 수동으로 [완료]를 클릭해 종료해야 합니다.
    - 적당한 시간을 선택하여 증분 데이터 동기화를 수동으로 완료하고 서비스 전환을 완료하십시오.
    - 마이그레이션 단계가 증분 동기화인지 여부와 지연 여부를 확인하고 소스 라이브러리 쓰기를 몇 분간 중단합니다.
    - 타깃 라이브러리와 소스 라이브러리의 차이가 0MB이고 딜레이가 0초일 경우, 수동으로 증분 동기화를 완료하십시오.
7. (옵션) 작업 ID를 클릭하여 작업 상세 보기 페이지로 들어가면 마이그레이션 상세 내용과 마이그레이션 객체 리스트를 확인할 수 있습니다.
