
## 확인 사항
다음 문서를 참고하여 데이터베이스의 작업 권한이 있는지 확인하십시오.

- 데이터 마이그레이션을 위한 권한 요구 사항

   - [MySQL/TDSQL-C/MariaDB/Percona 간의 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42645)
   - [MySQL/MariaDB/Percona/TDSQL MySQL 및 TDSQL MySQL 간의 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/47366)
   -  [PostgreSQL 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42640)
   -  [MongoDB 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42639)
   -  [SQL Server 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42638)

- 데이터 동기화를 위한 권한 요구 사항
   - [MySQL/TDSQL-C/MariaDB/Percona 간의 데이터 동기화](https://intl.cloud.tencent.com/document/product/571/47344)
   - [MySQL/MariaDB/Percona/TDSQL MySQL 및 TDSQL MySQL 간의 데이터 동기화](https://intl.cloud.tencent.com/document/product/571/47350)


- 데이터 구독을 위한 권한 요구 사항
   - [MySQL/MariaDB/TDSQL MySQL/TDSQL-C MySQL 데이터 구독](https://intl.cloud.tencent.com/document/product/571/47354)    
   - [TDSQL for PostgreSQL 데이터 구독](https://intl.cloud.tencent.com/document/product/571/47357)   

## TDSQL for PostgreSQL 확인 내용
REPLICATION 권한(예: pg_roles.rolreplication)이 있어야 합니다.

구독한 테이블의 select 권한이 있어야 합니다. 전체 데이터베이스 구독의 경우 schema 아래의 모든 테이블에 대한 select 권한이 있어야 합니다.

## 수정 방법

작업 권한이 없는 경우 확인 세부 사항의 권한 요구 사항에 따라 권한을 부여하고 확인 작업을 다시 실행합니다.

