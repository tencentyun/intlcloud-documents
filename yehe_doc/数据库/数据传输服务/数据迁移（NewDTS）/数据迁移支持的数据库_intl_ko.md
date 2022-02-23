
DTS는 자체 구축한 TencentDB 및 타사 클라우드 데이터베이스의 마이그레이션을 지원합니다. 다음은 구체적인 네트워크 연결 방법입니다.
- 공용 네트워크: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.

- CVM에서 자체 구축: 원본 데이터베이스가 [CVM](https://intl.cloud.tencent.com/document/product/213) 인스턴스에 배포됩니다.

- Direct Connect: 원본 데이터베이스는 [Direct Connect](https://intl.cloud.tencent.com/document/product/216)를 통해 VPC와 상호 연결될 수 있습니다. 

- VPN 액세스: 원본 데이터베이스는 [VPN 연결](https://intl.cloud.tencent.com/document/product/1037)을 통해 VPC와 상호 연결될 수 있습니다. 

- 데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.

- CCN: 원본 데이터베이스는 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 통해 VPC와 상호 연결될 수 있습니다.

타사 클라우드 데이터베이스의 경우 일반적으로 공용 네트워크를 선택하거나 실제 네트워크 조건에 따라 VPC 액세스, DC 또는 CCN을 선택할 수 있습니다.

마이그레이션을 지원하는 데이터베이스는 다음과 같습니다.

| **데이터 스트림 방향**   | **마이그레이션 방향** | **원본 데이터베이스 유형 및 버전**   | **대상 데이터베이스 유형 및 버전** |   **마이그레이션 유형** | **버전 간 마이그레이션** |
| ------------- | -----------  | -------------------- | ---------------------- | -------------- | -------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/42645) | Tencent Cloud         | <li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사(Alibaba Cloud 및 AWS)MySQL 5.6, 5.7, 8.0 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | Tencent Cloud | <li>자체구축 MariaDB 5.5, 10.0, 10.1, 10.2, 10.3, 10.4, 10.5, 10.6<li>TencentDB for MariaDB 5.5, 10.0, 10.1, 10.2, 10.3, 10.4, 10.5, 10.6 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 |
| [MariaDB(Percona)> MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | Tencent Cloud | <li>자체구축 Percona 5.5, 5.6, 5.7, 8.0<li>TencentDB for MariaDB (Percona) 5.5, 5.6, 5.7, 8.0 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 |
| [MySQL > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/42643) | Tencent Cloud | <li>자체구축 MySQL 5.5, 5.6, 5.7<li>타사(Alibaba Cloud 및 AWS) MySQL 5.6, 5.7 | TDSQL-C 5.6, 5.7 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - |
| [MySQL > TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/571/42642) | Tencent Cloud | <li>자체구축 MySQL 5.6, 5.7<li>TencentDB for MySQL 5.6, 5.7 | TDSQL for MySQL 5.7 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - |
| [MySQL > MariaDB(Percona)](https://intl.cloud.tencent.com/document/product/571/42641) | Tencent Cloud | <li>자체구축 MySQL 5.6, 5.7<li>TencentDB for MySQL 5.6, 5.7 | TencentDB for MariaDB (Percona) 5.7 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/42641) | Tencent Cloud | <li>자체구축 MariaDB 10.0.1, 10.1.9<li>TencentDB for MariaDB 10.1.9 | TencentDB for MariaDB 10.1.9 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - |
| [MariaDB(Percona)> MariaDB(Percona)](https://intl.cloud.tencent.com/document/product/571/42641) | Tencent Cloud | <li>자체구축 MariaDB(Percona) 5.7<li>TencentDB for MariaDB (Percona)  5.7 | TencentDB for MariaDB (Percona) 5.7 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - |
| [PostgreSQL > PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640) | Tencent Cloud | <li>자체구축 PostgreSQL 9.3, 9.5, 9.6, 10, 11, 12<li>TencentDB for PostgreSQL 9.3, 9.5, 9.6, 10, 11, 12<li>타사(All)PostgreSQL 9.3, 9.5, 9.6, 10, 11, 12 | TencentDB for PostgreSQL 9.3, 9.5, 9.6, 10, 11, 12 | <li>전체 마이그레이션<li>구조적 마이그레이션 | 지원, v13에서 v12로의 마이그레이션도 지원 |
| [PostgreSQL > PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640) | Tencent Cloud | PostgreSQL 10, 11, 12 | TencentDB for PostgreSQL 10，11，12 | 전체 + 증분 마이그레이션 | 미지원 |
| [MongoDB > MongoDB](https://intl.cloud.tencent.com/document/product/571/42639) | Tencent Cloud    | <li>자체구축 MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2<li>TencentDB for MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2<li>타사(Alibaba Cloud) MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2 | TencentDB for MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 |
| [SQL Server > SQL Server](https://intl.cloud.tencent.com/document/product/571/42638) | Tencent Cloud | <li>자체구축 SQL Server 2008R2, 2012, 2014, 2016, 2017, 2019<li>TencentDB for SQL Server 2008R2, 2012, 2014, 2016, 2017, 2019<li>타사(Alibaba Cloud 및 AWS) SQL Server 2008R2, 2012, 2014, 2016, 2017, 2019 | TencentDB for SQL Server  2008R2, 2012, 2014, 2016, 2017, 2019 | <li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 |

> ?
> - Tencent Cloud 마이그레이션 방향은 대상 데이터베이스가 TencentDB 데이터베이스 제품인 시나리오를 나타냅니다.
>- MySQL/TDSQL for MySQL/MariaDB: 대상 데이터베이스 버전은 원본 데이터베이스 버전 이상이어야 합니다. 버전은 주요 버전 번호로 구분됩니다. 예를 들어 v5.6.x를 v5.6.x, v5.7.x 이상으로 마이그레이션할 수 있습니다.
> - PostgreSQL: 전체 마이그레이션에서 대상 데이터베이스 버전은 원본 데이터베이스 버전보다 크거나 같아야 합니다. 증분 마이그레이션에서는 v10.x 이상의 버전 간 마이그레이션이 지원됩니다. 
>- MongoDB: 다른 버전 간의 마이그레이션이 지원됩니다.
>- SQL Server: 기본 버전에서 High Availability Edition(Dual-Server High Availability Edition 및 Cluster Edition 포함)으로의 마이그레이션만 지원되며 대상 데이터베이스의 버전 번호는 원본 데이터베이스의 버전 번호보다 높아야 합니다. 
