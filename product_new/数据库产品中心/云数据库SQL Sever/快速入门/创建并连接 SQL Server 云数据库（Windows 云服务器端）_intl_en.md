## Operation Scenario
This document describes how to connect to a TencentDB for SQL Server instance through SQL Server Management Studio (SSMS) in a Windows CVM instance and run a simple query.
>?The CVM and TencentDB instances must be under the same account and in the same VPC in the same region.

## Directions
1. On the [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) instance details page, view the private IP and port number of the instance, which will be used for connecting to the TencentDB instance.
2. Log in to the Windows CVM instance. For more information, please see [Getting Started with Windows CVM](https://intl.cloud.tencent.com/document/product/213/10516). This document uses Windows Server 2012 R2 Standard Edition (64-bit) as an example.
3. Download and install [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) in the Windows CVM instance. For more information on SSMS, please see [Use SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/database-engine/use-sql-server-management-studio?view=sql-server-2014).
![](https://main.qcloudimg.com/raw/019e13af6a6db7bf831cad9d7000279e.png)
4. Start SSMS in the Windows CVM instance. On the **Connect to server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
 - **Server type**: select "Database Engine".
 - **Server name**: enter the private IP and port number of the instance and separate them with a comma. For example, if the private IP and port number of the instance are `10.10.10.10:1433`, then enter `10.10.10.10,1433` here.
 - **Authentication**: select "SQL Server Authentication".
 - **Login** and **Password**: enter the account name and password you configured when creating the instance account on the **Account Management** page.
![](//mc.qcloudimg.com/static/img/1cac47c4fc515d30d2cb5a0ef0141e22/image.png)
5. Once connected to the database, you can view the standard built-in system databases (master, model, msdb, and tempdb) of SQL Server.
![](https://main.qcloudimg.com/raw/a25241cf8000e10bcf748abe99773a77.png)
6. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS will return the TencentDB for SQL Server instance.
![](//mc.qcloudimg.com/static/img/fbf64c03c7addda9c80fdd3dac7bbebb/image.png)

