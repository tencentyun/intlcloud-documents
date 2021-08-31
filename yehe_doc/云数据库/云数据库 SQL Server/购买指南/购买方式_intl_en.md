
## Prerequisites
To purchase instances, you need to verify your identity first. For more information, please see the [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Purchasing Instances in the TencentDB Console
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click **Create Instance** at the top of the instance list.
2. Select the desired configuration of the database and read and indicate your consent to the Terms of Service on the purchase page. After confirming that everything is correct, click **Buy Now**.
 - Billing Mode: pay-as-you-go
 - Region and AZ: for more information, please see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/238/7520).
 - Network: VPC (recommended) and the classic network are supported. For more information on the differences and connectivity testing, please see [Network Environment](https://intl.cloud.tencent.com/document/product/238/32562).
 >?
 >- It is recommended that the CVM and TencentDB instances should be under the same account and in the same VPC in the same region.
 >- As the classic network resources become increasingly scarce and cannot be expanded, Tencent Cloud accounts registered after June 13, 2017 can create instances (including CVM and TencentDB) only in a VPC rather than the classic network.
 >- If your business has to use the [classic network](https://intl.cloud.tencent.com/document/product/215/31807), please submit a ticket for application.
 - Instance Type: Dual-Server High-Availability Edition and Cluster Edition are supported.
 >?The Cluster Edition currently supports SQL Server 2017 Enterprise and SQL Server 2019 Enterprise, which use the Always On technology to build SQL Server clusters with high performance, availability, reliability, and ease of maintenance.
 - Database Version: the Enterprise and Standard Editions of SQL Server 2008 R2, SQL Server 2012, SQL Server 2016, SQL Server 2017, and SQL Server 2019 are supported. Each AZ supports different database versions.
 - Select an instance specification and required capacity.
 - Multi-AZ: currently, only the Shanghai, Beijing, and Guangzhou regions support selecting multi-AZ. By combining multiple AZs into a single "multi-AZ", the multi-AZ deployment mode protects databases from database instance failures and AZ outage.
 - Select the quantity and length of purchase.
3. After the purchase is made, return to the instance list and view the created instance. When the running status becomes **Running**, the instance is successfully created.

## Purchasing Instances via an API
For more information on how to purchase TencentDB instances via an API, please see [CreateDBInstances](https://intl.cloud.tencent.com/document/product/238/32119).
