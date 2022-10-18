데이터 마이그레이션은 원본 데이터베이스를 대상 데이터베이스로 복사하는 것으로 전체 데이터베이스 마이그레이션을 목적으로 하는 단기 일회성 작업으로 마이그레이션이 완료되면 새 데이터베이스에 작업을 연결합니다.

DTS는 원본 데이터베이스를 자체 구축한 데이터베이스, Tencent Cloud 데이터베이스 및 타사 클라우드 벤더 데이터베이스 등의 마이그레이션을 지원합니다.

- 자체 구축 데이터베이스를 클라우드로 마이그레이션: 로컬 IDC 자체 구축 데이터베이스, CVM의 자체 구축 데이터베이스, 경량 애플리케이션 서버의 경량 데이터베이스 등을 Tencent Cloud 데이터베이스로 마이그레이션합니다.
- Tencent Cloud 데이터베이스의 인스턴스 간 마이그레이션: 데이터베이스 버전 업그레이드, 리전 간 마이그레이션(중국 내/외 리전 간 포함), 서로 다른 Tencent Cloud 계정에 있는 데이터베이스 인스턴스 마이그레이션 등.
- 타사 클라우드 벤더에서 마이그레이션: 다른 클라우드 벤더(예: Alibaba Cloud, AWS 등)에서 Tencent Cloud로 마이그레이션합니다.

원본 데이터베이스의 배포 형태에 따라 다양한 액세스 방식을 선택할 수 있으며, DTS가 지원하는 액세스 방식은 공용 네트워크/CVM 자체 구축/DC/VPN 액세스/CDB/CCN입니다. 각 액세스 방식은 해당 네트워크 조건이 필요합니다. [준비 작업 개요](https://intl.cloud.tencent.com/document/product/571/42652)를 참고하십시오.

DTS 마이그레이션을 지원하는 데이터베이스는 다음과 같습니다.

| **데이터 스트림 방향**   | **마이그레이션 방향** | **원본 데이터베이스 유형 및 버전**   | **대상 데이터베이스 유형 및 버전** |   **마이그레이션 유형** | **계정 간 마이그레이션** | **원본 데이터베이스 액세스 유형** |
| ------------- | -----------  | -------------------- | ---------------------- | -------------- | ------------- | ------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/42645) | Tencent Cloud         | <ul><li>자체 구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사<ul><li>Alibaba Cloud RDS 5.5, 5.6, 5.7, 8.0<li>Alibaba Cloud PolarDB 5.6, 5.7, 8.0<li>AWS RDS MySQL 5.6, 5.7, 8.0<li>AWS Aurora MySQL 5.6, 5.7 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | Tencent Cloud | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [Percona > MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | Tencent Cloud | 자체구축 Percona 5.5, 5.6, 5.7, 8.0 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [TDSQL MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47366) | Tencent Cloud         | TencentDB TDSQL  MySQL 5.7, 8.0                               | TencentDB for MySQL 5.7, 8.0                                 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 | TencentDB |
| [MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/42641) | Tencent Cloud | <li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/42641)                                | Tencent Cloud         | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1                    | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [Percona > MariaDB](https://intl.cloud.tencent.com/document/product/571/42641)                                | Tencent Cloud         | 자체구축 Percona 5.5, 5.6, 5.7, 8.0                              | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1                    | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [TDSQL MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47366) | Tencent Cloud        | TencentDB TDSQL  MySQL 5.7, 8.0, 10.0, 10.1                   | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1                   | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 | TencentDB |
| [MySQL > TDSQL-C MySQL](https://intl.cloud.tencent.com/document/product/571/47364) | Tencent Cloud         | <ul><li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사<ul><li>Alibaba Cloud RDS 5.5, 5.6, 5.7, 8.0<li>Alibaba Cloud PolarDB 5.6, 5.7, 8.0<li>AWS RDS MySQL 5.6, 5.7, 8.0<li>AWS Aurora MySQL 5.6, 5.7 | 클라우드 네이티브 데이터베이스 TDSQL-C 5.7, 8.0                            | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [MariaDB > TDSQL-C MySQL](https://intl.cloud.tencent.com/document/product/571/47364) | Tencent Cloud | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | 클라우드 네이티브 데이터베이스 TDSQL-C 5.7, 8.0 | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [Percona > TDSQL-C MySQL](https://intl.cloud.tencent.com/document/product/571/47364) | Tencent Cloud         | 자체구축 Percona 5.5, 5.6, 5.7, 8.0                              | 클라우드 네이티브 데이터베이스 TDSQL-C 5.7, 8.0                            | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/42642) | Tencent Cloud         | <li>자체구축 MySQL 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.6, 5.7, 8.0 | TencentDB TDSQL MySQL 5.7, 8.0                            | <li>전체 마이그레이션<li>전체 + 증분 마이그레이션             | 지원          | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [MariaDB > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/42642) | Tencent Cloud | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1</li><li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1</li><dx-alert infotype="explain" title="설명">MariaDB > TDSQL MySQL(MariaDB)동종 마이그레이션 대상 라이브러리의 버전이 원본 라이브러리보다 크거나 같으며, 이종 마이그레이션은 현재 MariaDB 10.1 > TDSQL MySQL(Percona 5.7)의 이종 마이그레이션만 지원합니다.</dx-alert> | TencentDB TDSQL  MySQL 5.7, 8.0, 10.0, 10.1 | <li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [Percona > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/42642) | Tencent Cloud | 자체구축 Percona 5.5, 5.6, 5.7, 8.0 | TencentDB TDSQL  MySQL 5.7, 8.0 | <li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | - | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [TDSQL MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47366) | Tencent Cloud | TencentDB TDSQL  MySQL 5.7, 8.0, 10.0, 10.1 | TencentDB TDSQL  MySQL 5.7, 8.0, 10.0, 10.1,  | <li>구조적 마이그레이션<li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 | TencentDB |
| [PostgreSQL > PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640) | Tencent Cloud | <li>자체구축 PostgreSQL 9.3, 9.4, 9.5, 9.6, 10, 11, 12, 13, 14<li>TencentDB for PostgreSQL 10, 11, 12, 13<li>타사(All)PostgreSQL 9.3, 9.4, 9.5, 9.6, 10, 11, 12, 13, 14<br><dx-alert infotype="explain" title="설명">증분 마이그레이션은 버전 9.4 이상에서만 지원됩니다.</dx-alert> | TencentDB for PostgreSQL 10, 11, 12, 13 | <li>전체 마이그레이션<li>구조적 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [MongoDB > MongoDB](https://intl.cloud.tencent.com/document/product/571/42639) | Tencent Cloud    | <li>자체구축 MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2<li>TencentDB for MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2<li>타사(Alibaba Cloud) MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2 | TencentDB for MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, 4.2 | <li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 지원 | 공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |
| [SQL Server > SQL Server](https://intl.cloud.tencent.com/document/product/571/42638) | Tencent Cloud | <li>자체구축 SQL Server 2008R2, 2012, 2014, 2016, 2017, 2019<li>TencentDB for SQL Server 2008R2, 2012, 2014, 2016, 2017, 2019<li>타사(Alibaba Cloud 및 AWS) SQL Server 2008R2, 2012, 2014, 2016, 2017, 2019 | TencentDB for SQL Server  2008R2, 2012, 2014, 2016, 2017, 2019 | <li>전체 마이그레이션<li>전체 + 증분 마이그레이션 | 미지원 |공용 네트워크/CVM 자체구축/DC/VPN 액세스/CDB/CCN |

>?
>- Tencent Cloud로는 대상 데이터베이스가 Tencent Cloud 데이터베이스 제품인 시나리오를 나타냅니다. 위에서 언급한 ‘Tencent Cloud 데이터베이스’는 Tencent Cloud 데이터베이스 인스턴스를 나타냅니다.
>- 교차 계정 마이그레이션 원본 데이터베이스와 대상 데이터베이스는 모두 Tencent Cloud 데이터베이스 인스턴스에 속하지만, 서로 다른 루트 계정 이름 아래에 있는 데이터베이스 인스턴스 간의 데이터 마이그레이션은 [클라우드 데이터베이스 교차 계정 인스턴스 간 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42646)을 참고하십시오. 
>- 각 데이터베이스 마이그레이션에 대한 버전 요구 사항은 다음과 같습니다.
>   - MySQL/TDSQL for MySQL/MariaDB/TDSQL-C: 대상 데이터베이스 버전은 원본 데이터베이스 버전 이상이어야 합니다. 버전은 주요 버전 번호로 구분됩니다. 예를 들어 v5.6.x를 v5.6.x, v5.7.x 이상으로 마이그레이션할 수 있습니다.
>   - PostgreSQL: 전체 마이그레이션에서 대상 데이터베이스 버전은 원본 데이터베이스 버전보다 크거나 같아야 합니다. 증분 마이그레이션에서는 v10.x 이상의 버전 간 마이그레이션이 지원됩니다. 
>   - MongoDB: 다른 버전 간의 마이그레이션이 지원됩니다.
>   - SQL Server: 기본 버전에서 High Availability Edition(Dual-Server High Availability Edition 및 Cluster Edition 포함)으로의 마이그레이션만 지원되며 대상 데이터베이스의 버전 번호는 원본 데이터베이스의 버전 번호보다 높아야 합니다.
>- 위의 표는 NewDTS에서 지원하는 기능을 나타낸 것이므로 Redis에서 데이터를 마이그레이션해야 하는 경우 [Migration with DTS](https://intl.cloud.tencent.com/document/product/239/31941)를 사용하여 작업하십시오.

  
