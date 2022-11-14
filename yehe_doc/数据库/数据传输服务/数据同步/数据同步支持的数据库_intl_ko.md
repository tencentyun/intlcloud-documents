데이터 동기화는 연속 작업 형태로 두 데이터 소스 간의 데이터를 실시간으로 동기화하는 것을 말합니다. 작업이 생성된 후 데이터는 소스 데이터베이스와 대상 데이터베이스 간의 일관성을 유지하기 위해 거의 실시간으로 지속적으로 동기화됩니다.

Tencent Cloud DTS는 자체 구축 데이터베이스, CDB 및 타사 클라우드 벤더 데이터베이스 등의 TencentDB로 동기화를 지원합니다.

- 클라우드-로컬 동기화: DTS는 IDC 기반 자체 구축 데이터베이스를 TencentDB 인스턴스와 동기화하거나 그 반대로 동기화할 수 있습니다.
- 다중 클라우드 벤더 간의 동기화: 타사 클라우드 벤더 데이터베이스를 TencentDB 인스턴스로 동기화하여 이중 클라우드 동기화를 구현합니다.
- TencentDB 인스턴스 간의 동기화: 서로 다른 위치의 멀티액티브, 크로스보더 데이터 동기화, 다른 Tencent Cloud 계정에서의 데이터베이스 인스턴스 동기화 등.

원본 데이터베이스의 배포 형태에 따라 다양한 액세스 방식을 선택할 수 있으며, DTS가 지원하는 액세스 방식은 공용 네트워크/CVM 자체 구축/DC/VPN 액세스/CDB/CCN입니다. 각 액세스 방식은 해당 네트워크 조건이 필요합니다. [준비 작업 개요](https://intl.cloud.tencent.com/document/product/571/42652)를 참고하십시오.

데이터 동기화는 일대다, 다대일, 양방향 및 링 동기화와 같은 다양한 복잡한 토폴로지 구조를 지원합니다. 복잡한 토폴로지를 생성하려면 [양방향 동기화 데이터 구조 생성](https://intl.cloud.tencent.com/document/product/571/42605), [다대일 동기화 데이터 구조 생성](https://intl.cloud.tencent.com/document/product/571/42604) 또는 [멀티 사이트 Active-Active IDC 구축](https://intl.cloud.tencent.com/document/product/571/42603)을 참고하십시오.

## 동기화에서 지원하는 데이터베이스 유형 및 버전


| **데이터 플로우 방향**            | **동기화 방향** | **소스 데이터베이스**                       | **대상 데이터베이스**                   |
| --------------------- | ------------ | ------------------------------------- | ---------------------------------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | To Tencent Cloud         | <ul><li>자체 구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사 클라우드 데이터베이스<ul><li>Alibaba Cloud RDS 5.6, 5.7, 8.0<li>Alibaba Cloud PolarDB 5.6, 5.7, 8.0<li>AWS RDS MySQL 5.6, 5.7, 8.0<li>AWS Aurora MySQL 5.6, 5.7 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | To Tencent Cloud | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 |
| [Percona > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | To Tencent Cloud | 자체구축 Percona 5.5, 5.6, 5.7, 8.0 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 |
| [TDSQL-C > MySQL](https://intl.cloud.tencent.com/document/product/571/47348) | To Tencent Cloud |  TDSQL-C for MySQL 5.7, 8.0 | TencentDB for MySQL 5.7, 8.0 |
| [TDSQL MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud | TencentDB TDSQL  MySQL 5.7, 8.0 | TencentDB for MySQL 5.7, 8.0 |
| [MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | To Tencent Cloud | <li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | To Tencent Cloud | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 |
| [Percona > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) |  To Tencent Cloud | 자체구축 Percona 5.5, 5.6, 5.7, 8.0 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 |
| [TDSQL MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud | TencentDB TDSQL MySQL 5.7, 8.0, 10.0, 10.1 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 |
| [MySQL > TDSQL-C MySQL](https://intl.cloud.tencent.com/document/product/571/47348) | To Tencent Cloud         | <ul><li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사 클라우드 데이터베이스<ul><li>Alibaba Cloud RDS 5.6, 5.7, 8.0<li>Alibaba Cloud PolarDB 5.6, 5.7, 8.0<li>AWS RDS MySQL 5.6, 5.7, 8.0<li>AWS Aurora MySQL 5.6, 5.7 | TDSQL-C for MySQL 5.7, 8.0 |
| [TDSQL-C > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/47348) | To Tencent Cloud | TDSQL-C for MySQL 5.7, 8.0 |  TDSQL-C for MySQL 5.7, 8.0 |
| [MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud         | <li>자체구축 MySQL 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.6, 5.7, 8.0 | TDSQL for MySQL 5.7, 8.0 |
| [MariaDB > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud         | <li>자체구축 데이터베이스 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | TencentDB TDSQL MySQL 5.7, 8.0, 10.0, 10.1 |
| [Percona > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud         | 자체구축 Percona 5.5, 5.6, 5.7, 8.0 | TencentDB TDSQL MySQL 5.7, 8.0 |
| [TDSQL MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud | TencentDB TDSQL MySQL 5.7, 8.0, 10.0, 10.1 | TencentDB TDSQL MySQL 5.7, 8.0, 10.0, 10.1 |
| [TencentDB for MySQL > 로컬/타사 MySQL](https://intl.cloud.tencent.com/document/product/571/49880) | From Tencent Cloud | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>Alibaba Cloud MySQL 5.6, 5.7, 8.0 |

>?
>- To Tencent Cloud는 대상 데이터베이스가 TencentDB 인스턴스인 시나리오를 나타냅니다. From Tencent Cloud는 대상 데이터베이스가 TencentDB 인스턴스가 아닌 시나리오를 나타냅니다.
>- 동기화 요구 사항: 원본 및 대상 데이터베이스 중 하나 이상은 Tencent Cloud 데이터베이스 인스턴스여야 합니다.
>- 대상 데이터베이스 버전은 원본 데이터베이스 버전보다 높거나 같아야 합니다.
>- TDSQL for MySQL의 동기화 기능(소스 또는 대상 데이터베이스)을 사용하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 신청하십시오.
>- MySQL/MariaDB/Percona에서 TencentDB for MariaDB로 또는 MariaDB/Percona에서 TencentDB for MySQL로 데이터를 동기화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 신청하십시오.
>- 교차 계정 동기화는 서로 다른 루트 계정에 있는 원본 및 대상 TencentDB 인스턴스 간의 데이터 동기화를 나타냅니다. 자세한 지침은 [교차 계정 TencentDB 인스턴스 동기화](https://intl.cloud.tencent.com/document/product/571/47336)를 참고하십시오.
>

## 동기화에서 지원하는 주요 기능

| **데이터 플로우 방향**                                                 | **동기화 방향** | **양방향 동기화**                       | **데이터 초기화 유형**               | **교차 계정 동기화** | **소스 데이터베이스 액세스 유형**                              | **대상 데이터베이스 액세스 유형**                       |
| ------------------------------------------------------------ | ------------ | ---------------------------------- | -------------------------------- | -------------- | ------------------------------------------------- | ---------------------------------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | To Tencent Cloud         | 지원                               | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/데이터베이스/CCN | 데이터베이스                                 |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | To Tencent Cloud         | 지원됨(양방향 동기화는 TencentDB 인스턴스 간에만 지원됨) | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/데이터베이스/CCN | 데이터베이스                                 |
| [Percona > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | To Tencent Cloud         | 미지원                             | <li>구조 초기화<li>전체 데이터 초기화 | -              | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/CCN          | 데이터베이스                                 |
| [TDSQL-C > MySQL](https://intl.cloud.tencent.com/document/product/571/47348) | To Tencent Cloud         | 지원                               | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 데이터베이스                                          | 데이터베이스                                 |
| [TDSQL MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud         | 지원                               | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 데이터베이스                                          | 데이터베이스                                 |
| [MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | To Tencent Cloud         | 지원됨(양방향 동기화는 TencentDB 인스턴스 간에만 지원됨) | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/데이터베이스/CCN | 데이터베이스                                 |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | To Tencent Cloud         | 지원됨(양방향 동기화는 TencentDB 인스턴스 간에만 지원됨) | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/데이터베이스/CCN | 데이터베이스                                 |
| [Percona > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | To Tencent Cloud         | 미지원                             | <li>구조 초기화<li>전체 데이터 초기화 | -              | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/CCN          | 데이터베이스                                 |
| [TDSQL MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud         | 지원                               | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 데이터베이스                                          | 데이터베이스                                 |
| [MySQL > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/47348) | To Tencent Cloud         | 지원                               | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/데이터베이스/CCN | 데이터베이스                                 |
| [TDSQL-C > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/47348) | To Tencent Cloud         | 지원                               | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 데이터베이스                                          | 데이터베이스                                 |
| [MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud         | 지원됨(양방향 동기화는 TencentDB 인스턴스 간에만 지원됨) | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/데이터베이스/CCN | 데이터베이스                                 |
| [MariaDB > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) |  To Tencent Cloud         | 지원됨(양방향 동기화는 TencentDB 인스턴스 간에만 지원됨) | <li>구조 초기화<li>전체 데이터 초기화 | 지원           | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/데이터베이스/CCN | 데이터베이스                                 |
| [Percona > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | To Tencent Cloud         | 미지원                             | <li>구조 초기화<li>전체 데이터 초기화 | -              | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/CCN          | 데이터베이스                                 |
| [TencentDB for MySQL > 로컬/타사 MySQL](https://intl.cloud.tencent.com/document/product/571/49880) | From Tencent Cloud         | 지원                               | <li>구조 초기화<li>전체 데이터 초기화 | -              | 데이터베이스                                          | 공중망/CVM에서 자체 구축/직접 연결/VPN 액세스/CCN |