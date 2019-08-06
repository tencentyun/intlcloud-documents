This document describes how to create a TencentDB for SQL Server instance, perform port mapping using a Linux-based CVM instance with a public IP, connect to the database instance using SQL Server Management Studio (SSMS) to run a simple query, and delete the database instance.
If you need to connect to a TencentDB for SQL Server instance using SSMS from a Windows-based CVM instance, see [Creating and Connecting to a TencentDB for SQL Server Instance (from a Windows-based CVM Instance)](https://intl.cloud.tencent.com/document/product/238/11626).

>! You must have a Tencent Cloud account before creating a TencentDB for SQL Server instance. For more information about how to register a Tencent Cloud account, see [here](https://cloud.tencent.com/document/product/378/17985).

## Creating a TencentDB for SQL Server Instance
1. Log in to the [TencentDB Console](https://console.cloud.tencent.com/cdb) and select **SQL Server** > **Instance List*.
![](https://main.qcloudimg.com/raw/54a8f7715ece96bf548501e01a71b53f.png)
2. Click **+Create** and select the desired configuration of the database on the purchase page. After confirming everything is correct, click **Buy Now**.
 - **Billing Method**: Pay-as-you-go.
 - **Region** and **AZ**: For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/238/7520). This document uses Guangzhou and Guangzhou Zone 3 as an example.
 - **Network Type** Basic network and private network are supported. For the difference between VPC and basic network, see [Network Environment](https://intl.cloud.tencent.com/document/product/213/5227). This document uses a basic network as an example.
 - **Database Version**: SQL Server 2008 R2, SQL Server 2012, and SQL Server 2016 SP1 are supported. The versions available may vary by AZ. This document uses SQL Server 2012 as an example.
 - Select an instance specification and required capacity.
 - Select the quantity and length of purchase.
![](https://main.qcloudimg.com/raw/7ead0ec46e5cb4311d7519c9476d1b1f.png)
3. Return to the SQL Server instance list and view the instance just created. If the running status is **running**, the instance has been successfully created.
4. In the **Operation** column of the instance, click **Manage** to enter the instance details page.
5. On the instance details page, click **Account Management** > **Create Account** and enter relevant information on the account creation page that pops up. After confirming everything is correct, click **OK**.
**The account name and password entered in this step will be used when connecting to TencentDB for SQL Server. Please store them properly.** This document uses "test" as an example.
![](https://main.qcloudimg.com/raw/c7bbc414640b605570305235f1cf38b5.png)
6. On the instance details page, select **Database Management** > **Create a Database** and enter relevant information on the database creation page that pops up. After confirming everything is correct, click **OK**.
In this step, grant the database's **read-write** or **read-only** permission to the account created in the previous step.
![](https://main.qcloudimg.com/raw/00b91db7079783fcc468af4bf501776a.png)

## Connecting to a TencentDB for SQL Server Instance (from Local Machine)
For data security considerations, TencentDB for SQL Server currently doesn't support public IP. If you need to use a public IP, you can use the port mapping function of SSH2 to connect to, configure and manage an instance from the internet. This document uses SecureCRT as an example for demonstration.
1. On the TencentDB for SQL Server instance details page, click **Instance Details** to view the private IP and port number of the instance. **The private IP and port number here will be used when configuring port mapping.**
![](https://main.qcloudimg.com/raw/c92e46d1d767daef089cf689b4c11a5c.png)
2. Prepare a Linux-based CVM instance **with a public IP**. If you don't have one yet, see [Getting Started - Linux-based CVM](https://intl.cloud.tencent.com/document/product/213/2936).
3. Log in to the Linux-based CVM instance locally using an SSH tool such as SecureCRT or PuTTY. For the login method, see [Logging in to a Linux-based Instance](https://intl.cloud.tencent.com/document/product/213/5436).
4. Select **Options** > **Session Options** in the SecureCRT menu bar to enter the session properties settings.
![](//mc.qcloudimg.com/static/img/6f48c98d69986fd497535ec8760a0a49/image.png)
5. On the session properties settings page, select **Connection** > **Port Forwarding** > **Add** to enter the port mapping configuration page.
![](//mc.qcloudimg.com/static/img/8a489ede3e8ae598a6530e77b9481eab/image.png)
6. On the port mapping configuration page, configure the corresponding parameters.
![](https://main.qcloudimg.com/raw/6b6b4a0ee3982ef6ec2261ce8cfc5559.png)
7. Download and install [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) locally. For more information on SSMS, see Microsoft's official document - [Use SQL Server Management Studio](https://docs.microsoft.com/zh-cn/sql/database-engine/use-sql-server-management-studio?view=sql-server-2014).
8. Start SSMS locally. In the **Connect to Server** interface, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
![](//mc.qcloudimg.com/static/img/1cac47c4fc515d30d2cb5a0ef0141e22/image.png)
 - Server type: Select Database Engine.
 - Server name: Type or paste the local IP address and port number and separate them with a**commas**. The port number needs to be the same as that configured in step 6, such as `10.0.0.1，4000`. Be sure to use **English punctuation marks**.
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
![](https://main.qcloudimg.com/raw/0e668ae3c6f69d5a6c58d40aa0af1e49.png)
2. On the instance details page, select **Database Management** > **Delete Database**. It takes time to delete the database. Please wait patiently.
![](https://main.qcloudimg.com/raw/146965f91d643c86ed2dd416ad67d728.png)
3. Currently, manual deletion is not supported by TencentDB for SQL Server instance. Service will automatically stop if it is not renewed after expiration, .



