
In this tutorial, you can create a TencentDB for SQL Server instance. Then, connect to the database instance using SQL Server Management Studio (SSMS) in a Windows-based CVM instance and run a simple query. Finally, you will delete the database instance.
If you need to connect to a TencentDB for SQL Server instance using SSMS locally, see the Getting Started Tutorial - [Creating and Connecting to a TencentDB for SQL Server Instance (from Local Side)](/document/product/238/11627).

> **Note:**
> You must have a Tencent Cloud account before creating a TencentDB for SQL Server instance. If you don't have one yet, please enter the relevant information on the [registration page](https://cloud.tencent.com/register) to register for one.

## I. Creating a TencentDB for SQL Server Instance
In this step, you will create a database instance using the Tencent Cloud Console.
1. Log in to the [TencentDB Console](https://console.cloud.tencent.com/cdb).
![](//mc.qcloudimg.com/static/img/7f454c8f988ec22c4045b33c47571024/image.png)
2. In the navigation bar on the right, select the type of TencentDB instance to be created. Here, select **SQL Server**. Click **+ Create** to enter the TencentDB for SQL Server purchase interface.
![](//mc.qcloudimg.com/static/img/798911fbe873e0a59de7d749b365c0ca/image.png)
3. In the TencentDB for SQL Server purchase interface, select the database-related configurations. After confirming everything is correct, click **Purchase now**.
 - Billing method. Currently, only "prepaid" is supported.
 - Region and availability zone. This tutorial takes "Guangzhou" and "Guangzhou Zone 3" as an example. For region descriptions, see [Regions and Availability Zones](/doc/product/236/8458).
 - Network environment. Basic network and VPC are supported. This tutorial uses a basic network as an example. For the differences between basic network and VPC, see [Network Environments](/doc/product/213/5227).
 - Database version. SQL Server 2008 R2 and SQL Server 2012 are available. This may vary for different availability zones subject to actual conditions. This tutorial takes "SQL Server 2012" as an example.
 - Instance specifications and required disks.
 - Quantity and duration to be purchased.
![](//mc.qcloudimg.com/static/img/1630495ca9ca9001b4cdef32e1b85364/image.png)
4. Go to the [TencentDB Console](https://console.cloud.tencent.com/cdb) and select **SQL Server** to view the TencentDB instance just created. If the running state shows **running**, the TencentDB for SQL Server instance has been successfully created.
![](//mc.qcloudimg.com/static/img/eedd98d6992bdb6e06d25d8380365e89/image.png)
5. In the TencentDB for SQL Server management interface, click **Manage** to enter the instance details page.
![](//mc.qcloudimg.com/static/img/aeb4d8c1b053c4ea9dbb6f5a9a48fc4d/image.png)
6. On the instance details page, click **Account management** > **Create account** to open the account creation page. Enter the relevant information to create an account. After confirming everything is correct, click **OK**. **The account name and password entered in this step will be used when connecting to TencentDB for SQL Server. Please store them properly.** This tutorial takes "test" as an example.
![](//mc.qcloudimg.com/static/img/1cac253d8eb9029bbaf10aa385b4c0bd/image.png)
7. On the instance details page, click **Database management** > **Create database** to pop up the database creation page. Enter the relevant information to create a database. After confirming everything is correct, click **OK**. In this step, grant the database's **read-write** or **read-only** permission to the account created in step 6.
![](//mc.qcloudimg.com/static/img/8db9f2aaa65978c0e0005739c7861aad/image.png)

## II. Connecting to a TencentDB for SQL Server Instance (from a Windows-based CVM Instance)
1. Log in to the Windows-based CVM instance. If you don't have one yet, see [Getting Started - Windows-based CVM](/doc/product/213/2764). This tutorial takes Windows Server 2012 R2 Standard Edition 64-bit English Version as an example.
2. Download and install [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) in the Windows-based CVM instance. For more information on SSMS, see Microsoft's official documentation - [Using SQL Server Management Studio][1].
3. On the TencentDB for SQL Server instance details page, click **Instance details** to view the private IP and port number of the instance. **The private IP and port number here will be used when connecting to TencentDB.**
![](//mc.qcloudimg.com/static/img/6dcf51fc839f1ea7c47c26609b711ede/image.png)
4. Start SSMS in the Windows-based CVM instance. In the **Connect to Server** interface, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
![](//mc.qcloudimg.com/static/img/1cac47c4fc515d30d2cb5a0ef0141e22/image.png)
 - Server type. Select Database Engine.
 - Server name. Type or paste the private IP and port number of the database instance and separate them with a **comma**. For example, if the private IP and port number obtained in step 3 are: `10.10.10.10:1433`, then enter `10.10.10.10, 1433` here. Be sure to use **English punctuation marks**.
 - Authentication. Select SQL Server Authentication.
 - Login and Password. The account name and password you entered when creating the account in step 6 in section I. This tutorial takes "test" as an example.
5. Once connected to the database, you can view the standard built-in system databases (master, model, msdb and tempdb) of SQL Server.
![](//mc.qcloudimg.com/static/img/a39d9db6f6a4050d1fa4285a53b55157/image.png)
6. Now you can start creating your own databases and running queries for them, Click **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS returns the SQL Server version of TencentDB instance.
![](//mc.qcloudimg.com/static/img/fbf64c03c7addda9c80fdd3dac7bbebb/image.png)

## III. Deleting a TencentDB for SQL Server Instance
1. On the TencentDB for SQL Server instance details page, click **Account management** > **Delete account**. It takes a certain amount of time to delete the account. Please be patient.
![](//mc.qcloudimg.com/static/img/7ce670ca67766ed32d088b4f733c56b6/image.png)
2. On the TencentDB for SQL Server instance details page, click **Database management** > **Delete**. It takes a certain amount of time to delete the database. Please be patient.
![](//mc.qcloudimg.com/static/img/fa68b790fe7a12e1c17bfde648ac6e98/image.png)
3. The TencentDB for SQL Server instance does not support manual deletion for the time being. If it is not renewed after expiration, it will be stopped automatically.

[1]:https://msdn.microsoft.com/zh-cn/library/ms174173(v=sql.105).aspx
