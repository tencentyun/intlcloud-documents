
DTS supports migration of self-built, TencentDB, and third-party cloud databases. Below are the specific network connection methods:
- Public Network: the source database can be accessed through a public IP.

- Self-Build on CVM: the source database is deployed in a [CVM](https://intl.cloud.tencent.com/document/product/213) instance.

- Direct Connect: the source database can be interconnected with VPCs through [Direct Connect](https://intl.cloud.tencent.com/document/product/216). 

- VPN Access: the source database can be interconnected with VPCs through [VPN Connection](https://intl.cloud.tencent.com/document/product/1037). 

- Database: the source database is a TencentDB database.

- CCN: the source database can be interconnected with VPCs through [CCN](https://intl.cloud.tencent.com/document/product/1003).

For a third-party cloud database, you can select **Public Network** generally or select **VPC Access**, **Direct Connect**, or **CCN** based on your actual network conditions.

Databases that support migration are as detailed below:

| **Data Flow Direction**   | **Migration Direction** | **Source Database Type and Version**   | **Target Database Type and Version** |   **Migration Type** | **Cross-version Migration** |
| ------------- | -----------  | -------------------- | ---------------------- | -------------- | -------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/42645) | To Tencent Cloud         | <li>Self-Built MySQL 5.5, 5.6, 5.7, and 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, and 8.0<li>Third-Party (Alibaba Cloud and AWS) MySQL 5.6, 5.7, and 8.0 | TencentDB for MySQL 5.5, 5.6, 5.7, and 8.0 | <li>Structural migration<li>Full migration<li>Full + incremental migration | Supported |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | To Tencent Cloud | <li>Self-Built MariaDB 5.5, 10.0, 10.1, 10.2, 10.3, 10.4, 10.5, and 10.6<li>TencentDB for MariaDB 5.5, 10.0, 10.1, 10.2, 10.3, 10.4, 10.5, and 10.6 | TencentDB for MySQL 5.5, 5.6, 5.7, and 8.0 | <li>Structural migration<li>Full migration<li>Full + incremental migration | Yes |
| [MariaDB (Percona) > MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | To Tencent Cloud | <li>Self-Built Percona 5.5, 5.6, 5.7, and 8.0<li>TencentDB for MariaDB (Percona) 5.5, 5.6, 5.7, and 8.0 | TencentDB for MySQL 5.5, 5.6, 5.7, and 8.0 | <li>Structural migration<li>Full migration<li>Full + incremental migration | Supported |
| [MySQL > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/42643) | To Tencent Cloud | <li>Self-Built MySQL 5.5, 5.6, and 5.7<li>Third-Party (Alibaba Cloud and AWS) MySQL 5.6 and 5.7 | TDSQL-C 5.6 and 5.7 | <li>Structural migration<li>Full migration<li>Full + incremental migration | - |
| [MySQL > TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/571/42642) | To Tencent Cloud | <li>Self-Built MySQL 5.6 and 5.7<li>TencentDB for MySQL 5.6 and 5.7 | TDSQL for MySQL 5.7 | <li>Structural migration<li>Full migration<li>Full + incremental migration | - |
| [MySQL > MariaDB (Percona)](https://intl.cloud.tencent.com/document/product/571/42641) | To Tencent Cloud | <li>Self-Built MySQL 5.6 and 5.7<li>TencentDB for MySQL 5.6 and 5.7 | TencentDB for MariaDB (Percona) 5.7 | <li>Structural migration<li>Full migration<li>Full + incremental migration | - |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/42641) | To Tencent Cloud | <li>Self-Built MariaDB 10.0.1 and 10.1.9<li>TencentDB for MariaDB 10.1.9 | TencentDB for MariaDB 10.1.9 | <li>Structural migration<li>Full migration<li>Full + incremental migration | - |
| [MariaDB (Percona) > MariaDB (Percona)](https://intl.cloud.tencent.com/document/product/571/42641) | To Tencent Cloud | <li>Self-Built MariaDB (Percona) 5.7<li>TencentDB for MariaDB (Percona) 5.7 | TencentDB for MariaDB (Percona) 5.7 | <li>Structural migration<li>Full migration<li>Full + incremental migration | - |
| [PostgreSQL > PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640) | To Tencent Cloud | <li>Self-Built PostgreSQL 9.3, 9.5, 9.6, 10, 11, and 12<li>TencentDB for PostgreSQL 9.3, 9.5, 9.6, 10, 11, and 12<li>Third-Party (all) PostgreSQL 9.3, 9.5, 9.6, 10, 11, and 12 | TencentDB for PostgreSQL 9.3, 9.5, 9.6, 10, 11, and 12 | <li>Full migration<li>Structural migration | Supported. Migration from v13 to v12 is also supported |
| [PostgreSQL > PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640) | To Tencent Cloud | PostgreSQL 10, 11, and 12 | TencentDB for PostgreSQL 10, 11, and 12 | Full + incremental migration | Not supported |
| [MongoDB > MongoDB](https://intl.cloud.tencent.com/document/product/571/42639) |To Tencent Cloud   | <li>Self-Built MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, and 4.2<li>TencentDB for MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, and 4.2<li>Third-Party (Alibaba Cloud) MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, and 4.2 | TencentDB for MongoDB 3.0, 3.2, 3.4, 3.6, 4.0, and 4.2 | <li>Structural migration<li>Full migration<li>Full + incremental migration | Supported |
| [SQL Server > SQL Server](https://intl.cloud.tencent.com/document/product/571/42638) | To Tencent Cloud | <li>Self-Built SQL Server 2008 R2, 2012, 2014, 2016, 2017, and 2019<li>TencentDB for SQL Server 2008 R2, 2012, 2014, 2016, 2017, and 2019<li>Third-Party (Alibaba Cloud and AWS) SQL Server 2008 R2, 2012, 2014, 2016, 2017, and 2019 | TencentDB for SQL Server 2008 R2, 2012, 2014, 2016, 2017, and 2019 | <li>Full migration<li>Full + incremental migration | Supported |

> ?
> - "To Tencent Cloud" refers to scenarios where the target database is a TencentDB database product.
>- MySQL/TDSQL for MySQL/MariaDB: the target database version must be greater than or equal to the source database version. The versions are differentiated by the major version number; for example, v5.6.x can be migrated to v5.6.x, v5.7.x, and above.
> - PostgreSQL: in full migration, the target database version must be greater than or equal to the source database version; in incremental migration, migration between versions above v10.x is supported. 
>- MongoDB: migration between different versions is supported.
>- SQL Server: only migration from Basic Edition to High Availability Edition (including Dual-Server High Availability Edition and Cluster Edition) is supported, and the version number of the target database must be above that of the source database. 
