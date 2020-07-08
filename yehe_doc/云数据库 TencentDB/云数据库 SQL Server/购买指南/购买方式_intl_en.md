## Prerequisites
To make a purchase, you need to verify your identity first. For more information, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Purchasing at Official Website
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) and click **Create** in the instance list.
3. Select the desired configuration of the database on the purchase page. After confirming that everything is correct, click **Buy Now**.
 - Billing Mode: pay-as-you-go billing is supported.
 - Region and AZ: for more information, please see [Regions and AZs](https://intl.cloud.tencent.com/document/product/238/7520).
 - Network: the basic network and VPC are supported. For more information on the differences and connectivity testing, please see [Network Environment](https://intl.cloud.tencent.com/document/product/238/32562).
 - Instance Type: Dual-Server High-Availability Edition and Cluster Edition are supported.
 >The Cluster Edition currently supports only SQL Server 2017 Enterprise, which uses the Always On technology to build SQL Server clusters with high performance, availability, reliability, and ease of maintenance.
 - Database Version: SQL Server 2008, SQL Server 2012, SQL Server 2016, and SQL Server 2017 (Enterprise/Standard) are supported. The versions available may vary by AZ.
 - Multi-AZ: currently, only the Shanghai, Beijing, and Guangzhou regions support selecting multi-AZ. By combining multiple AZs into a single "multi-AZ", the multi-AZ deployment mode protects databases from database instance failures and AZ outage.
 - Select an instance specification and required disk capacity.
 - Select the quantity and length of purchase.
3. After the purchase is made, return to the instance list and view the created instance. When the running status becomes **Running**, the instance is successfully created.


## Purchasing Through API
For more information on how to purchase a TencentDB instance through the API, please see [Creating Instance](https://intl.cloud.tencent.com/document/product/238/32119).
