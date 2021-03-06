데이터 전송 서비스(DTS)는 binlog를 기반으로 하는 증분 데이터 구독 기능을 제공합니다. 간단한 몇 가지 작업을 거치면 CDB TencentDB의 증분 업데이트 데이터를 구독할 수 있습니다.

데이터 구독 Kafka 버전은 Kafka 클라이언트를 통해 데이터 소비를 직접 지원합니다. 데이터 구독 기능을 통해 소스 라이브러리의 증분 데이터 변경 구독을 쉽게 실현할 수 있어 캐시 업데이트, ETL(데이터 웨어하우스 기술) 실시간 동기화, 서비스 비동기화 등 CDB와 이종 시스템 간의 데이터 동기화를 편리하게 구축할 수 있습니다.
>?데이터 구독 Kafka 버전의 데이터 구독 메시지는 중간 스토리지 Kafka에 기본적으로 1일(24시간) 보관됩니다. 유효 시간 내에 소비하지 않을 경우 구독 데이터가 손실될 수 있습니다.
>
## 전제 조건
- TencentDB for MySQL, TencentDB for MariaDB 또는 TDSQL MySQL 버전의 구독 준비가 완료되어야 합니다.
 - TencentDB for MySQL은 MySQL 5.6, MySQL 5.7 동기화 버전을 지원해야 합니다.
 - TencentDB for MariaDB는 MariaDB 10.0.10, MariaDB 10.1.9, Percona 5.7.17 동기화 버전을 지원해야 합니다.
 - TDSQL MySQL 버전은 Percona 5.7.17 동기화 버전을 지원해야 합니다.
- 원본 인스턴스에서 binlog가 활성화되어야 합니다.
- 소스 라이브러리에 `__tencentdb__` 데이터베이스가 생성되어야 합니다.
- 구독 계정이 원본 인스턴스에 생성되어야 합니다. 필요한 계정 권한은 다음과 같습니다. REPLICATION CLIENT, REPLICATION SLAVE, PROCESS 및 모든 대상의 SELECT 권한.
구체적인 권한 부여 명령은 다음과 같습니다:.
```
create user ‘마이그레이션 계정’ IDENTIFIED BY ‘계정 비밀번호’:
grant SELECT, REPLICATION CLIENT, REPLICATION SLAVE, PROCESS on *.* to '마이그레이션 계정'@'%';
grant ALL PRIVILEGES on `__tencentdb__`.* to '마이그레이션 계정'@'%';
flush privileges;
```

## TDSQL MySQL 버전 데이터 구독 설명
- 데이터 구독 소스가 TDSQL MySQL 버전인 경우, 직접적으로 권한 부여 명령을 실행하여 권한을 부여할 수 없습니다. 따라서 [TDSQL 콘솔](https://console.cloud.tencent.com/tdsqld)에서 인스턴스 이름을 클릭하여 계정 관리 페이지로 들어간 뒤 구독 계정 권한을 추가해야 합니다.
구독 계정에 필요한 권한은 위의 권한 부여 명령에서 언급된 권한입니다. 구독 계정에 `__tencentdb__`의 권한을 부여하려면 콘솔의 권한 수정 팝업창에서 객체 수준의 권한을 선택하고 모든 권한을 체크합니다.
- 데이터 구독 소스가 TDSQL MySQL 버전인 경우, 인스턴스는 서브 파티션의 파티션 테이블 생성을 지원하지 않습니다. 인스턴스가 구독 작업을 시작하기 전에 이미 서브 파티션의 파티션 테이블이 존재하는 경우 인증 작업이 실패하게 되며, 구독 작업 실행 중에 인스턴스가 서브 파티션의 파티션 테이블을 생성하는 경우 구독 작업 오류 보고 후 작업이 일시 중단됩니다.
서브 파티션에 관한 자세한 내용은 [서브 파티션](https://intl.cloud.tencent.com/document/product/1042/33361)을 참조하십시오.
- 데이터 구독 소스가 TDSQL MySQL 버전인 구독 작업의 경우, 각 샤드의 DDL 작업이 구독되어 Kafka로 전달되므로 하나의 파티션 테이블의 DDL 작업에서 중복된 DDL 명령이 나타날 수 있습니다. 예를 들어, 인스턴스 A에 3개의 샤드가 있고 테이블 A가 파티션 테이블이라고 할 때, 테이블 A에 대해 3개의 DDL 명령이 구독됩니다.
- Kafka의 모든 메시지의 메시지 헤더에는 key/value 형식의 샤딩 정보가 담겨 있으며, key는 ShardId, value는 SQL 투과 전송 ID입니다. [샤딩 관리](https://console.cloud.tencent.com/tdsqld)를 참조하시면 SQL 투과 전송 ID별로 해당 정보의 출처가 어느 샤드인지 구분할 수 있습니다.

## 구독을 지원하는 SQL 작업
|  유형      | 데이터 변경                    | 구조 변경                                                    | 데이터+구조 변경 |
| ------ | --------------------------- | ----------------------------------------------------------- | ------------- |
| 전체 인스턴스 | DML: INSERT, UPDATE, DELETE | DDL: CREATE DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE | DML+DDL       |
| 데이터베이스 | DML: INSERT, UPDATE, DELETE | DDL: CREATE TABLE, ALTER TABLE, DROP TABLE    | DML+DDL       |
| 데이터 테이블 | DML: INSERT, UPDATE, DELETE | DDL: ALTER TABLE, DROP TABLE                            | DML+DDL       |

## 작업 순서
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/dss)에 로그인한 뒤 왼쪽 메뉴에서 [데이터 구독]을 선택해 [데이터 구독 생성]을 클릭합니다.
2. 데이터 구독 생성 페이지에서 적합한 구성을 선택하고 [즉시 구매]를 클릭합니다.
 - 과금 방식: 정액 과금제 및 종량제 과금 방식을 지원합니다.
 - 리전: 리전은 구독하려는 데이터베이스의 인스턴스 구독과 일치해야 합니다.
 - 데이터베이스: 현재 MySQL, Percona, MariaDB를 지원합니다. 구체적인 데이터베이스 유형에 따라 선택하십시오.
 - 버전: [kafka 버전]을 선택하면 Kafka 클라이언트를 통한 직접 소비를 지원합니다.
 - 구독 인스턴스 이름: 현재 데이터 구독 인스턴스의 이름을 편집합니다.
3. 구매 성공 후, 데이터 구독 리스트로 돌아가 '작업'열의 [구독 설정]을 클릭해 새로 구입한 구독의 설정을 진행합니다. 설정 완료 후 사용할 수 있습니다.
4. 데이터베이스 구독 설정 페이지에서 적합한 설정을 선택하고 [다음 단계]를 클릭합니다.
 - 인스턴스: 원하는 데이터베이스 인스턴스를 선택합니다. TencentDB for MySQL은 현재 MySQL 5.6, MySQL 5.7 고가용성 버전의 마스터 인스턴스를 지원합니다. 읽기 전용 인스턴스와 재해 복구 인스턴스는 데이터 구독을 지원하지 않습니다.
 - 데이터베이스 계정: 구독 인스턴스의 계정과 비밀번호를 추가합니다. 계정은 구독 작업에 필요한 REPLICATION CLIENT, REPLICATION SLAVE, PROCESS 및 모든 대상의 SELECT 권한을 갖추고 있습니다. 권한 최소화 원칙에 따라 부여된 권한은 더 많거나 적을 수 없습니다. 그렇지 않으면 인증에 실패할 수 있다는 점을 유의하십시오.
5. 구독 유형 및 대상 선택 페이지에서 구독 유형을 선택하고 [설정 저장]을 클릭합니다.
구독 유형은 데이터 업데이트, 구조 업데이트 및 전체 인스턴스를 포함합니다. 구독 유형을 선택한 후, 데이터베이스와 데이터 테이블을 포함하여 구독 데이터 대상을 선택합니다.
  - 데이터 업데이트: 데이터 INSERT, UPDATE, DELETE 작업을 포함하여 선택한 대상의 데이터 업데이트를 구독합니다.
  - 구조 업데이트: 구독 인스턴스 내 모든 대상의 구조를 생성, 수정 및 삭제합니다.
  - 전체 인스턴스: 해당 구독 인스턴스의 모든 대상의 데이터 업데이트 및 구조 업데이트를 포함합니다.
6. 사전 검증 페이지에서 2~3분에 걸쳐 사전 검증 작업이 실행됩니다. 사전 검증이 완료된 후, [실행]을 클릭하여 데이터 구독 작업 설정을 완료합니다.
>?검증에 실패하면 오류 알림에 따라 구독할 인스턴스에서 수정하고 다시 검증을 진행합니다.
>
7. 실행을 클릭하면 구독 작업이 초기화되며 3~4분 동안 실행됩니다. 초기화에 성공하면 '실행 중' 상태로 변합니다.

## 데이터 소비
구독 인스턴스가 ‘실행 중’ 상태가 되면 데이터 소비를 시작할 수 있습니다. 소비 로직에 대한 자세한 내용은 [데이터 소비 Demo](https://intl.cloud.tencent.com/document/product/571/39538)를 참조하십시오. 다양한 언어의 Demo 코드를 참고용으로 제공하고 있으며 핵심 소비 프로세스와 데이터 구조에 대한 설명도 제공합니다.

## 후속 작업
데이터 구독 Kafka 버전은 사용자가 여러 개의 소비자 그룹을 만들어 다지점 소비를 할 수 있도록 지원합니다. 자세한 내용은 [신규 소비자 그룹](https://intl.cloud.tencent.com/zh/document/product/571/39534)을 참조하십시오.
