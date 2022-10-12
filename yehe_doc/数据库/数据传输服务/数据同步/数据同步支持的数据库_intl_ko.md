数据同步功能指两个数据源之间的数据实时同步，数据同步属于持续性任务，任务创建后会一直同步数据（几乎实时同步），保持源库和目标库的数据一致性。

Tencent Cloud DTS는 자체 구축 데이터베이스, CDB 및 타사 클라우드 벤더 데이터베이스 등의 TencentDB로 동기화를 지원합니다.

- 云上云下同步：将本地 IDC 自建数据库同步到腾讯云数据库实例，并且支持建立反向同步，腾讯云数据库实例同步到 IDC 自建，实现云上云下双向同步。
- 다중 클라우드 벤더 간의 동기화: 타사 클라우드 벤더 데이터베이스를 TencentDB 인스턴스로 동기화하여 이중 클라우드 동기화를 구현합니다.
- TencentDB 인스턴스 간의 동기화: 서로 다른 위치의 멀티액티브, 크로스보더 데이터 동기화, 다른 Tencent Cloud 계정에서의 데이터베이스 인스턴스 동기화 등.

원본 데이터베이스의 배포 형태에 따라 다양한 액세스 방식을 선택할 수 있으며, DTS가 지원하는 액세스 방식은 공용 네트워크/CVM 자체 구축/DC/VPN 액세스/CDB/CCN입니다. 각 액세스 방식은 해당 네트워크 조건이 필요합니다. [준비 작업 개요](https://intl.cloud.tencent.com/document/product/571/42652)를 참고하십시오.

数据同步支持复制拓扑结构，如一对多同步、多对一同步、双向同步、环形同步等，如需构建复杂拓扑，请参考对应配置指导，[构建双向同步数据结构](https://intl.cloud.tencent.com/document/product/571/42605)，[构建多对一同步数据结构](https://intl.cloud.tencent.com/document/product/571/42604)，[构建多活数据中心](https://intl.cloud.tencent.com/document/product/571/42603)。

## 同步支持的数据库类型和版本


| **数据流向**            | **同步方向** | **源数据库**                       | **目标数据库**                   |
| --------------------- | ------------ | ------------------------------------- | ---------------------------------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | Tencent Cloud         | <ul><li>자체 구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사<ul><li>Alibaba Cloud RDS 5.6, 5.7, 8.0<li>Alibaba Cloud PolarDB 5.6, 5.7, 8.0<li>AWS RDS MySQL 5.6, 5.7, 8.0<li>AWS Aurora MySQL 5.6, 5.7 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | Tencent Cloud | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 |
| [Percona > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | Tencent Cloud | 자체구축 Percona 5.5, 5.6, 5.7, 8.0 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 |
| [TDSQL-C > MySQL](https://intl.cloud.tencent.com/document/product/571/47348) | Tencent Cloud | 클라우드 네이티브 데이터베이스 TDSQL-C 5.7, 8.0 | TencentDB for MySQL 5.7, 8.0 |
| [TDSQL MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | Tencent Cloud | TencentDB TDSQL  MySQL 5.7, 8.0 | TencentDB for MySQL 5.7, 8.0 |
| [MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | Tencent Cloud | <li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | Tencent Cloud | <li>자체구축 MariaDB 5.7, 8.0, 10.0, 10.1<li>TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 | TencentDB for MariaDB 5.7, 8.0, 10.0, 10.1 |
| [Percona > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) |  Tencent Cloud | 자체구축 Percona 5.5、5.6、5.7、8.0 | TencentDB for MariaDB 5.7、8.0、10.0、10.1 |
| [TDSQL MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47350) | Tencent Cloud | TencentDB TDSQL MySQL 5.7、8.0、10.0、10.1 | TencentDB for MariaDB 5.7、8.0、10.0、10.1 |
| [MySQL > TDSQL-C MySQL](https://intl.cloud.tencent.com/document/product/571/47348) | Tencent Cloud         | <ul><li>자체구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사<ul><li>Alibaba Cloud RDS 5.6, 5.7, 8.0<li>Alibaba Cloud PolarDB 5.6, 5.7, 8.0<li>AWS RDS MySQL 5.6, 5.7, 8.0<li>AWS Aurora MySQL 5.6, 5.7 | 클라우드 네이티브 데이터베이스 TDSQL-C 5.7, 8.0 |
| [TDSQL-C > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/47348) | Tencent Cloud | 클라우드 네이티브 데이터베이스 TDSQL-C 5.7、8.0 | 클라우드 네이티브 데이터베이스 TDSQL-C 5.7、8.0 |
| [MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | Tencent Cloud         | <li>자체구축 데이터베이스 MySQL 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.6, 5.7, 8.0 | TencentDB TDSQL MySQL 5.7, 8.0 |
| [MariaDB > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | Tencent Cloud         | <li>자체구축 데이터베이스 MariaDB 5.7、8.0、10.0、10.1<li>TencentDB for MariaDB 5.7、8.0、10.0、10.1 | TencentDB TDSQL MySQL 5.7、8.0、10.0、10.1 |
| [Percona > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | Tencent Cloud         | 자체구축 Percona 5.5、5.6、5.7、8.0 | TencentDB TDSQL MySQL 5.7、8.0 |
| [TDSQL MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | Tencent Cloud | TencentDB TDSQL MySQL 5.7、8.0、10.0、10.1 | TencentDB TDSQL MySQL 5.7、8.0、10.0、10.1 |
| [云上数据库 MySQL > 云下 MySQL](https://intl.cloud.tencent.com/document/product/571/49880) | 出云 | 云数据库 MySQL 5.5、5.6、5.7、8.0 | <li>自建 MySQL 5.5、5.6、5.7、8.0<li>阿里云 MySQL 5.6、5.7、8.0 |

>?
>- 入云指目标库为腾讯云数据库实例的场景，出云指目标库为非腾讯云数据库实例的场景。
>- 동기화 요구 사항: 원본 및 대상 데이터베이스 중 하나 이상은 Tencent Cloud 데이터베이스 인스턴스여야 합니다.
>- 대상 데이터베이스 버전은 원본 데이터베이스 버전보다 높거나 같아야 합니다.
>- 当前如果用户需要使用 TDSQL MySQL（作为源库或者作为目标库）的同步功能，需 [提交工单](https://console.cloud.tencent.com/workorder/category) 进行申请。
>- 当前如果用户需要使用 MySQL/MariaDB/Percona 数据同步至 MariaDB ，MariaDB/Percona 数据同步至 MySQL 功能，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 进行申请。
>- 교차 계정 동기화 원본 데이터베이스와 대상 데이터베이스는 모두 Tencent Cloud 데이터베이스 인스턴스에 속하지만, 서로 다른 루트 계정 이름 아래에 있는 데이터베이스 인스턴스 간의 데이터 동기화는 [클라우드 데이터베이스 교차 계정 인스턴스 간 동기화](https://intl.cloud.tencent.com/document/product/571/47336)를 참고하십시오.
>

## 同步支持的关键功能

| **数据流向**                                                 | **同步方向** | **双向同步**                       | **数据初始化类型**               | **跨账号同步** | **源数据库接入类型**                              | **目标库接入类型**                       |
| ------------------------------------------------------------ | ------------ | ---------------------------------- | -------------------------------- | -------------- | ------------------------------------------------- | ---------------------------------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | 入云         | 支持                               | <li>结构初始化<li>全量数据初始化 | 支持           | 公网/云主机自建/专线接入/VPN 接入/云数据库/云联网 | 云数据库                                 |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | 入云         | 支持（仅云数据库之间支持双向同步） | <li>结构初始化<li>全量数据初始化 | 支持           | 公网/云主机自建/专线接入/VPN 接入/云数据库/云联网 | 云数据库                                 |
| [Percona > MySQL](https://intl.cloud.tencent.com/document/product/571/47344) | 入云         | 不支持                             | <li>结构初始化<li>全量数据初始化 | -              | 公网/云主机自建/专线接入/VPN 接入/云联网          | 云数据库                                 |
| [TDSQL-C > MySQL](https://intl.cloud.tencent.com/document/product/571/47348) | 入云         | 支持                               | <li>结构初始化<li>全量数据初始化 | 支持           | 云数据库                                          | 云数据库                                 |
| [TDSQL MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | 入云         | 支持                               | <li>结构初始化<li>全量数据初始化 | 支持           | 云数据库                                          | 云数据库                                 |
| [MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | 入云         | 支持（仅云数据库之间支持双向同步） | <li>结构初始化<li>全量数据初始化 | 支持           | 公网/云主机自建/专线接入/VPN 接入/云数据库/云联网 | 云数据库                                 |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | 入云         | 支持（仅云数据库之间支持双向同步） | <li>结构初始化<li>全量数据初始化 | 支持           | 公网/云主机自建/专线接入/VPN 接入/云数据库/云联网 | 云数据库                                 |
| [Percona > MariaDB](https://intl.cloud.tencent.com/document/product/571/47346) | 入云         | 不支持                             | <li>结构初始化<li>全量数据初始化 | -              | 公网/云主机自建/专线接入/VPN 接入/云联网          | 云数据库                                 |
| [TDSQL MySQL > MariaDB](https://intl.cloud.tencent.com/document/product/571/47350) | 入云         | 支持                               | <li>结构初始化<li>全量数据初始化 | 支持           | 云数据库                                          | 云数据库                                 |
| [MySQL > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/47348) | 入云         | 支持                               | <li>结构初始化<li>全量数据初始化 | 支持           | 公网/云主机自建/专线接入/VPN 接入/云数据库/云联网 | 云数据库                                 |
| [TDSQL-C > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/47348) | 入云         | 支持                               | <li>结构初始化<li>全量数据初始化 | 支持           | 云数据库                                          | 云数据库                                 |
| [MySQL > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | 入云         | 支持（仅云数据库之间支持双向同步） | <li>结构初始化<li>全量数据初始化 | 支持           | 公网/云主机自建/专线接入/VPN 接入/云数据库/云联网 | 云数据库                                 |
| [MariaDB > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | 入云         | 支持（仅云数据库之间支持双向同步） | <li>结构初始化<li>全量数据初始化 | 支持           | 公网/云主机自建/专线接入/VPN 接入/云数据库/云联网 | 云数据库                                 |
| [Percona > TDSQL MySQL](https://intl.cloud.tencent.com/document/product/571/47350) | 入云         | 不支持                             | <li>结构初始化<li>全量数据初始化 | -              | 公网/云主机自建/专线接入/VPN 接入/云联网          | 云数据库                                 |
| [云上数据库 MySQL > 云下 MySQL](https://intl.cloud.tencent.com/document/product/571/49880) | 出云         | 支持                               | <li>结构初始化<li>全量数据初始化 | -              | 云数据库                                          | 公网/云主机自建/专线接入/VPN 接入/云联网 |