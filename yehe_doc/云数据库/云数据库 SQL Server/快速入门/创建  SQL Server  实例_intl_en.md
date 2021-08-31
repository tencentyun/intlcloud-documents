
## Overview
This document describes how to create an instance in the TencentDB for SQL Server console.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
### Creating an instance
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click **Create Instance** at the top of the instance list.
![](https://main.qcloudimg.com/raw/7abd65a18810994b0c34c75450a41868.png)
2. Select the desired configuration of the database and read and indicate your consent to the Terms of Service on the purchase page. After confirming that everything is correct, click **Buy Now**.
 - Billing Mode: pay-as-you-go
 - Region and AZ: for more information, please see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/238/7520).
 - Network: VPC (recommended) and the classic network are supported. For more information on the differences and connectivity testing, please see [Network Environment](https://intl.cloud.tencent.com/document/product/238/32562).
  >?
 >- It is recommended that the CVM and TencentDB instances should be under the same account and in the same VPC in the same region.
 >- As the classic network resources become increasingly scarce and cannot be expanded, Tencent Cloud accounts registered after June 13, 2017 can create instances (including CVM, Cloud Load Balancer, etc.) only in a VPC rather than the classic network.
 >- If your business needs to use the [classic network](https://intl.cloud.tencent.com/document/product/215/31807), please submit a ticket for application.
 - Instance Type: Dual-Server High-Availability Edition and Cluster Edition are supported.
 >?The Cluster Edition currently supports SQL Server 2017 Enterprise and SQL Server 2019 Enterprise, which use the Always On technology to build SQL Server clusters with high performance, availability, reliability, and ease of maintenance.
 - Database Version: the Enterprise and Standard Editions of SQL Server 2008 R2, SQL Server 2012, SQL Server 2016, SQL Server 2017, and SQL Server 2019 are supported. Each AZ supports different database versions.
 - Select an instance specification and required capacity.
 - Multi-AZ: currently, only the Shanghai, Beijing, and Guangzhou regions support selecting multi-AZ. By combining multiple AZs into a single "multi-AZ", the multi-AZ deployment mode protects databases from database instance failures and AZ outage.
 - Select the quantity and length of purchase.
3. After the purchase is made, return to the instance list. When the running status becomes **Running**, the instance is successfully created.

### [Creating database accounts](id:cjzh)
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Select **Account Management** > **Create Account** and enter relevant information in the pop-up dialog box. After confirming that everything is correct, click **OK**.
>?The created account name and password will be used when connecting to TencentDB for SQL Server. Please store them properly.
>
![](https://main.qcloudimg.com/raw/8093d54af8d7f5699a8b18c5bff87986.png)

### Creating databases
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Select the **Manage Database** tab, click **Create Database**, and enter relevant information in the pop-up dialog box. After confirming that everything is correct, click **OK**
.
 - Database Name: it can contain up to 32 letters, digits, and underscores, and must start with a letter.
 - Supported Character Set: select the character set to be used by the database. Currently, most native character sets are supported.
 - Authorize Account: you can authorize existing accounts to access the database. If you haven't created an account yet, please see [Creating database accounts](#cjzh).
 - Remarks: it can contain up to 256 characters.
![](https://main.qcloudimg.com/raw/6bb212145f1cf97837ed7aa6be0bf05c.png)

