
This document describes how to create a TencentDB for SQL Server instance, connect to the database instance using SQL Server Management Studio (SSMS) in a Windows CVM instance and run a simple query, as well as how to delete the database instance.
If you need to connect to a TencentDB for SQL Server instance using SSMS locally, see [Creating and Connecting to a TencentDB for SQL Server Instance (from Local Machine)](/doc/product/238/11627).

>! You must have a Tencent Cloud account before creating a TencentDB for SQL Server instance. For more information about how to register a Tencent Cloud account, see [here](https://cloud.tencent.com/document/product/378/17985).

## Creating a TencentDB for SQL Server Instance
1. Log in to the [TencentDB Console](https://console.cloud.tencent.com/cdb) and select **SQL Server** > **Instance List*.
![](https://main.qcloudimg.com/raw/c8a5843dc5f1ddecb1e7767f848ca895.png)
2. Click **+Create** and select desired database configurations on the purchase page. After confirming everything is correct, click **Buy Now**.
 - **Billing Method**: Pay-as-you-go.
 - **Region** and **AZ**: For more information, see [Regions and AZs](/doc/product/236/8458). This document uses Guangzhou and Guangzhou Zone 3 as an example.
 - **Network Type** Basic network and private network are supported. For the difference between VPC and basic network, see [Network Environment](/doc/product/213/5227). This document uses the basic network as an example.
 - **Database Version**: SQL Server 2008 R2, SQL Server 2012, and SQL Server 2016 SP1 are supported. Available versions may vary in different availability zones. This document uses SQL Server 2012 as an example.
 - Select an instance specification and required capacity.
 - Select the quantity and length of purchase.
![](https://main.qcloudimg.com/raw/85a55961d655af3870919df938dddaf0.png)
3. Return to the SQL Server instance list and view the instance just created. If the running status is **running**, the instance has been successfully created.
4. In the **Operation** column of the instance, click **Manage** to enter the instance details page.
5. On the instance details page, click **Account Management** > **Create an Account** and enter relevant information on the account creation page that pops up. Check that all the information is correct and click **OK**.
**The account name and password entered in this step will be used when connecting to TencentDB for SQL Server. Please store them properly.** This document uses "test" as an example.
![](//mc.qcloudimg.com/static/img/1cac253d8eb9029bbaf10aa385b4c0bd/image.png)
6. On the instance details page, select **Database Management** > **Create a Database** and enter relevant information on the database creation page that pops up. Check that all the information is correct and click **OK**.
In this step, grant the database's **read-write** or **read-only** permission to the account created in the previous step.
![](//mc.qcloudimg.com/static/img/8db9f2aaa65978c0e0005739c7861aad/image.png)

## Connecting to a TencentDB for SQL Server Instance (from a Windows-based CVM Instance)
1. Log in to Tencent Windows CVM. If you do not have a Tencent Windows CVM instance, see [Getting Started with Windows-based CVM](/doc/product/213/2764). This document uses 64-bit Windows Server 2012 R2 Standard as an example.
2. Download and install [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) in the Windows-based CVM instance. For more information on SSMS, see Microsoft's official document - [Use SQL Server Management Studio](https://docs.microsoft.com/zh-cn/sql/database-engine/use-sql-server-management-studio?view=sql-server-2014).
3. On the TencentDB for SQL Server instance details page, click **Instance Details** to view the private IP and port number of the instance. **The private IP and port number here will be used when connecting to TencentDB.**
![](https://main.qcloudimg.com/raw/05866d097de8b621b3a27b230ed6de8c.png)
4. Start SSMS in the Windows-based CVM instance. In the **Connect to Server** interface, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
![](//mc.qcloudimg.com/static/img/1cac47c4fc515d30d2cb5a0ef0141e22/image.png)
 - Server type: Select Database Engine.
 - Server name: Type or paste the private IP and port number of the database instance and separate them with **commas**. For example, if the private IP and port number obtained in the previous step are: `10.10.10.10:1433`, then enter `10.10.10.10, 1433` here. Be sure to use **English punctuation marks**.
 - Authentication: Select SQL Server Authentication.
 - Login and Password: Enter the account and password set when the account of the instance was created. This document uses "test" as an example.
5. Once connected to the database, you can view the standard built-in system databases (master, model, msdb and tempdb) of SQL Server.
![](//mc.qcloudimg.com/static/img/a39d9db6f6a4050d1fa4285a53b55157/image.png)
6. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS returns the SQL Server version of TencentDB instance.
![](//mc.qcloudimg.com/static/img/fbf64c03c7addda9c80fdd3dac7bbebb/image.png)

## Deleting a TencentDB for SQL Server Instance
1. On the TencentDB for SQL Server instance details page, click **Account Management** > **Delete Account**. It takes time to delete the account. Please wait patiently.
![](//mc.qcloudimg.com/static/img/7ce670ca67766ed32d088b4f733c56b6/image.png)
2. On the instance details page, select **Database Management** > **Delete Database**. It takes time to delete the database. Please wait patiently.
![](//mc.qcloudimg.com/static/img/fa68b790fe7a12e1c17bfde648ac6e98/image.png)
3. Currently, manual deletion is not supported by TencentDB for SQL Server instance. Service will automatically stop if it is not renewed after expiration, .

