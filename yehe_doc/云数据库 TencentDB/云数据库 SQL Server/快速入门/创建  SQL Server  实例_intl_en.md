## Operation Scenarios
This document describes how to create an instance in the TencentDB for SQL Server Console.

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
### Creating instance
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) and click **Create Instance** in the instance list.
![](https://main.qcloudimg.com/raw/7abd65a18810994b0c34c75450a41868.png)
2. Select the desired configuration of the database and read and indicate your consent to the Terms of Service on the purchase page. After confirming that everything is correct, click **Buy Now**.
 - Billing Mode: pay-as-you-go billing is supported.
 - Region and AZ: for more information, please see [Regions and AZs](https://intl.cloud.tencent.com/document/product/238/7520).
 - Network: VPC (recommended) and the classic network are supported. For more information on the differences and connectivity testing, please see [Network Environment](https://intl.cloud.tencent.com/document/product/238/32562).
  >?
 >- It is recommended that the CVM and TencentDB instances be under the same account and in the same VPC in the same region.
 >- As the classic network resources are becoming increasingly scarce and cannot be expanded, the classic network is no longer supported for accounts registered after June 13, 2017. This means that instances (such as CVM and CLB instances) cannot be created in the classic network; instead, they can only be created in VPCs.
 >- If your business has to use the [classic network](https://intl.cloud.tencent.com/document/product/215/31807), please submit a ticket for application.
 - Instance Type: Dual-Server High-Availability Edition and Cluster Edition are supported.
 >?The Cluster Edition currently supports only SQL Server 2017 Enterprise, which uses the AlwaysOn technology to build SQL Server clusters with high performance, availability, reliability, and ease of maintenance.
 - Database Version: SQL Server 2008, SQL Server 2012, SQL Server 2016, and SQL Server 2017 (Enterprise/Standard) are supported. The versions available may vary by AZ.
 - Select an instance specification and required disk capacity.
 - Multi-AZ: currently, only the Shanghai, Beijing, and Guangzhou regions support selecting multi-AZ. By combining multiple AZs into a single "multi-AZ", the multi-AZ deployment mode protects databases from database instance failures and AZ outage.
 - Select the quantity and length of purchase.
3. After the purchase is made, return to the instance list. When the running status becomes **Running**, the instance is successfully created.

<span id = "cjzh"></span>
### Creating account
1. In the [instance list](https://console.cloud.tencent.com/sqlserver), click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Manage Account** > **Create Account** and enter relevant information in the pop-up dialog box. After confirming that everything is correct, click **OK**.
>?The account name and password will be used when connecting to TencentDB for SQL Server. Please store them properly.
>
![](https://main.qcloudimg.com/raw/8093d54af8d7f5699a8b18c5bff87986.png)

### Creating database
1. In the [instance list](https://console.cloud.tencent.com/sqlserver), click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Manage Database** > **Create Database** and enter relevant information in the pop-up dialog box. After confirming that everything is correct, click **OK**
.
 - Database Name: it can contain up to 32 letters, digits, and underscores and must start with a letter.
 - Support Character Set: select the character set to be used by the database. Currently, most native character sets are supported.
 - Authorize Account: you can authorize existing accounts to access the database. If you haven't created an account yet, please see [Creating account](#cjzh).
 - Remarks: it can contain up to 256 characters.
![](https://main.qcloudimg.com/raw/6bb212145f1cf97837ed7aa6be0bf05c.png)

