
## Overview
This document describes how to connect to a TencentDB for SQL Server instance through SQL Server Management Studio (SSMS) on a Windows CVM instance and run a simple query.
>?
>- The CVM and TencentDB instances are better to be under the same account and in the same VPC in the same region.
>- CVM and TencentDB instances in the same VPC in different AZs in the same region can directly interconnect through private IPs.
>- CVM and TencentDB instances in different regions or VPCs or under different accounts can interconnect through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18836) or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985).

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click an instance ID to enter the instance details page, and view the private IP and port number of the instance, which will be used for connecting to the TencentDB instance.
![](https://main.qcloudimg.com/raw/343f649c398b60f859c4aa5b47d7d47f.png)
2. Log in to the Windows CVM instance. For more information, see [Customizing Windows CVM Configurations](https://www.tencentcloud.com/document/product/213/10516). This document uses Windows Server 2012 R2 Standard Edition (64-bit) as an example.
3. Download and install [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) on the Windows CVM instance. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en-us/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
4. Start SSMS in the Windows CVM instance. On the **Connect to server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
 - **Server type**: Select Database Engine.
 - **Server name**: Enter the private IP and port number of the instance and separate them by comma. For example, if the private IP of the instance is `10.10.10.10` and the port number is `1433`, then enter `10.10.10.10,1433` here.
 - **Authentication**: Select SQL Server Authentication.
 - **Login** and **Password**: Enter the account name and password you configured when creating the instance account on the **Account Management** page.
![](https://main.qcloudimg.com/raw/31be70916eda52a393d97dcca5be90f8.png)
5. Once connected to the database, you can view the standard built-in system databases (master, model, msdb and tempdb) of SQL Server.
![](https://main.qcloudimg.com/raw/a25241cf8000e10bcf748abe99773a77.png)
6. You can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS returns the TencentDB for SQL Server instance.
![](https://qcloudimg.tencent-cloud.cn/raw/d90bfce08de4fa93a6f1fa3de21d17d3.png)
