DTS supports sync of self-built, TencentDB, and third-party cloud databases. Below are the specific network connection methods:

- Public Network: the source database can be accessed through a public IP.
- Self-Build on CVM: the source database is deployed in a [CVM](https://intl.cloud.tencent.com/document/product/213) instance.
- Direct Connect: the source database can be interconnected with VPCs through [Direct Connect](https://intl.cloud.tencent.com/document/product/216). 
- VPN Access: the source database can be interconnected with VPCs through [VPN Connection](https://intl.cloud.tencent.com/document/product/1037). 
- VPC: the source and target databases are both deployed in Tencent Cloud [VPCs](https://intl.cloud.tencent.com/document/product/215). The data sync feature supports the VPC access type. To use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Database: the source database is a TencentDB database.
- CCN: the source database can be interconnected with VPCs through [CCN](https://intl.cloud.tencent.com/document/product/1003).

For a third-party cloud database, you can select **Public Network** generally or select **VPC Access**, **Direct Connect**, or **CCN** based on your actual network conditions.

Databases that support sync are as detailed below:


| **Data Flow Direction**            | **Sync Direction** | **Source Database**                       | **Target Database**                   | **Data Initialization Type**           |
| --------------------- | ------------ | ------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| MySQL > TencentDB for MySQL        | To Tencent Cloud         | <li>Self-Built MySQL 5.5, 5.6, 5.7, and 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, and 8.0<li>Third-Party (AWS and Alibaba Cloud) MySQL 5.5, 5.6, and 5.7 | TencentDB for MySQL 5.5, 5.6, 5.7, and 8.0 | <li>Structure initialization<li>Full data initialization |
| TencentDB for MySQL > PostgreSQL | To Tencent Cloud         | TencentDB for MySQL 5.6 and 5.7 | Cloud Data Warehouse PostgreSQL (CDWPG) 1.0.0              | <li>Structure initialization<li>Full data initialization |
| TencentDB for MySQL > TDSQL-A for PostgreSQL | To Tencent Cloud | TencentDB for MySQL 5.6 and 5.7 | TDSQL-A for PostgreSQL | <li>Structure initialization<li>Full data initialization |
| MySQL > TDSQL-C | To Tencent Cloud         | <li>Local self-built MySQL 5.5, 5.6, and 5.7<li>TencentDB for MySQL 5.5, 5.6, and 5.7<li>Third-Party (Alibaba Cloud and AWS) MySQL 5.5, 5.6, and 5.7 | TDSQL-C 5.7 | <li>Structure initialization<li>Full data initialization |
| TDSQL-C > TencentDB for MySQL | To Tencent Cloud | TDSQL-C 5.7 | TencentDB for MySQL 5.7 and 8.0 | <li>Structure initialization<li>Full data initialization |
| TDSQL-C > TDSQL-C | To Tencent Cloud | TDSQL-C 5.7 | TDSQL-C 5.7 | <li>Structure initialization<li>Full data initialization |
| TencentDB for MySQL > local MySQL | From Tencent Cloud | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | MySQL 5.5, 5.6, 5.7, and 8.0 | - |

>?
>- "To Tencent Cloud" refers to scenarios where the target database is a Tencent Cloud database product. "From Tencent Cloud" refers to scenarios where the target database isn't a Tencent Cloud database product.
>- Sync requirement: at least one of the source and target databases must be a Tencent Cloud database instance.
>- The target database version must be above or equal to the source database version.

