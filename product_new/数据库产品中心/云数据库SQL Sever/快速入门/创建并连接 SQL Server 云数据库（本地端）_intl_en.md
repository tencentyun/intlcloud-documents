## Operation Scenario
This document describes how to use a Linux CVM instance equipped with a public IP to map the ports, connect to an instance through SQL Server Management Studio (SSMS), and run a simple query.
>The CVM and TencentDB instances must be under the same account and in the same VPC in the same region.

## Directions
For data security considerations, TencentDB for SQL Server currently doesn't open up public IP for instances. If you need a public IP, you can use the port mapping function of SSH2 to connect to, configure, and manage your instance from the internet.
1. On the [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) instance details page, view the private IP and port number of the instance, which will be used for configuring port mapping.
![](https://main.qcloudimg.com/raw/c92e46d1d767daef089cf689b4c11a5c.png)
2. Prepare a Linux CVM instance with a public IP. For more information, please see [Getting Started with Linux CVM](/doc/product/213/2936).
3. Log in to the Linux CVM instance locally with an SSH tool such as SecureCRT (used as an example in this document) or PuTTY. For the login method, please see [Logging in to Linux CVM Instances](/doc/product/213/5436).
4. Select **Options** > **Session Options** in the SecureCRT menu bar to enter the session properties settings page.
![](https://main.qcloudimg.com/raw/acbb1ad0a808ac59a0053063b75aab8b.png)
5. On the session properties settings page, select **Connection** > **Port Forwarding** > **Add** to enter the port mapping configuration page.
![](https://main.qcloudimg.com/raw/05f0cadcda75c6f931f34eb296a5ab6f.png)
6. On the port mapping configuration page, configure the corresponding parameters.
![](https://main.qcloudimg.com/raw/6b6b4a0ee3982ef6ec2261ce8cfc5559.png)
7. Download and install [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) locally. For more information on SSMS, please see [Use SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/database-engine/use-sql-server-management-studio?view=sql-server-2014).
8. Start SSMS locally. On the **Connect to server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
 - **Server type**: select "Database Engine".
 - **Server name**: enter the local IP address and port number and separate them with a comma, such as `10.0.0.1,4000`. The port number should be the same as that configured in step 6.
 - **Authentication**: select "SQL Server Authentication".
 - **Login** and **Password**: enter the account name and password you configured when creating the instance account on the **Account Management** page.
![](https://main.qcloudimg.com/raw/14d90aa2eda6c841680f0fdc74db8219.png)
5. Once connected to the database, you can view the standard built-in system databases (master, model, msdb, and tempdb) of SQL Server.
![](https://main.qcloudimg.com/raw/c65c02197b506bd5b326128f1a3983a0.png)
6. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS will return the TencentDB for SQL Server instance.
![](//mc.qcloudimg.com/static/img/fbf64c03c7addda9c80fdd3dac7bbebb/image.png)



