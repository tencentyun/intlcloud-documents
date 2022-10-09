
This document describes how to connect to a TencentDB for SQL Server instance through SQL Server Management Studio (SSMS) from a local Windows computer and run a simple query.

## Connection Scenarios
The connection methods vary by TencentDB instance type:
You can connect to a TencentDB for SQL Server Dual-Server High Availability/Cluster Edition instance from a local computer in the following three methods:
- Option 1: Use VPN Connections, Direct Connect, or CCN as described in [Overview](https://intl.cloud.tencent.com/document/product/1037/32679), [Getting Started](https://intl.cloud.tencent.com/document/product/216/7557), or [Getting Started with the CCN](https://intl.cloud.tencent.com/document/product/1003/31985) respectively for connection, which are more secure and stable.
- Option 2: Connect to the instance over the public network by [enabling the public network address](#kqwwdz) or [binding the instance to CLB to enable public network access](#CLBKQWW) in the console.
- Option 3: Use a [Linux CVM instance with a public IP to map the ports](#WWIPLJSL).

You can connect to a TencentDB for SQL Server Basic Edition instance from a local system in the following two methods:
- Option 1: Use VPN Connections, Direct Connect, or CCN as described in [Overview](https://intl.cloud.tencent.com/document/product/1037/32679), [Getting Started](https://intl.cloud.tencent.com/document/product/216/7557), or [Getting Started with the CCN](https://intl.cloud.tencent.com/document/product/1003/31985) respectively for connection, which are more secure and stable.
- Option 2: Connect to the instance over the public network by [enabling the public network address](#kqwwdz) in the console.
- Option 3: Use a Linux CVM instance with a public IP to map the ports as instructed in [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).

The following describes certain connection options:
- Enabling the public network address in the console and connecting to the TencentDB for SQL Server instance from a local computer through SSMS.
- Binding the TencentDB for SQL Server instance to CLB and connecting to the instance from a local computer through SSMS.
- Using a Linux CVM instance with a public IP to map the ports and connecting to the TencentDB for SQL Server instance from a local computer through SSMS.

## Enabling the Public Network Address in the Console and Connecting to the TencentDB for SQL Server Instance from a Local Computer Through SSMS
[](id:kqwwdz)
### Step 1. Enable the public network address
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region and click the ID or **Manage** in the **Operation** column of the target instance in the instance list.
3. On the **Instance Details** tab, click **Enable** in **Basic Info** > **Public Network Address**.
4. In the **Enabling public network** window, read the note, indicate your consent, and click **OK**.
5. After public network access is enabled, view the public IP address and port number of the instance in **Basic Info** on the **Instance Details** tab.
>?For the detailed notes and steps of enabling public network access, see [Enabling/Disabling Public Network Address](https://www.tencentcloud.com/document/product/238/50230).

### Step 2. Connect to the TencentDB for SQL Server instance over the public network
1. Download and install [SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) locally. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
2. Start SSMS locally. On the **Connect to Server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
 - **Server type**: Select **Database Engine**.
 - **Server name**: Enter the public IP address and port number of the instance and separate them by comma.
 -  **Authentication**: Select **SQL Server Authentication**.
 -  **Login** and **Password**: Enter the account name and password you configured when creating the instance account on the **Account Management** tab.
![](https://main.qcloudimg.com/raw/14d90aa2eda6c841680f0fdc74db8219.png)
3. Once connected to the database, you can view the standard built-in system databases (master, model, msdb, and tempdb) of SQL Server.
![](https://main.qcloudimg.com/raw/c65c02197b506bd5b326128f1a3983a0.png)
4. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS will return the TencentDB for SQL Server instance.
![](https://qcloudimg.tencent-cloud.cn/raw/620a6143d5687581e9f2892e3fb76130.png)

## [Binding the TencentDB for SQL Server Instance to CLB to Enable Public Network Access and Connecting to the Instance from a Local Computer Through SSMS](id:CLBKQWW)
### Step 1. Purchase a CLB instance
>?If you already have a CLB instance in the same region as TencentDB for SQL Server, skip this step.
>
>Go to the [CLB purchase page](https://buy.intl.cloud.tencent.com/clb), select the configuration, and click **Buy Now**.
>!
>
>- Region: You need to select the region where the TencentDB for SQL Server instance is.
>- Network: You can select the same VPC as the instance or a different VPC.

### Step 2. Configure the CLB instance
1. Enable cross-VPC access (you can skip this step if the CLB instance and TencentDB for SQL Server instance are in the same VPC).
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the **Basic Info** page, click **Configure** in the **Real Server** section.
c. In the pop-up window, click **Submit**.

2. Configure a public network listener port.
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the instance management page, select the **Listener Management** tab and click **Create** below **TCP/UDP/TCP SSL Listener**.
![](https://qcloudimg.tencent-cloud.cn/raw/debe21b3f30a7970580ef852f49eccef.png)
c. In the pop-up window, complete the settings and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/eb615ec1f962220a8810c293400e488a.png)

### Step 3. Bind a TencentDB for SQL Server instance
1. After creating the listener, click it in **Listener Management** and click **Bind** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/3f96c6cc462304f626a1ec4c464b1132.png)
2. In the pop-up window, select **Other Private IPs** as the object type, enter the IP address and port of the TencentDB for SQL Server instance, and click **OK**.
>!The login account must be a standard account (bill-by-IP). If binding fails, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

### Step 4. Configure the TencentDB for SQL Server security group
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select a region, and click the ID of the target instance in the instance list or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Security Group** tab, click **Configure Security Group**, configure the security group rule to open all ports, and confirm that the security group allows access from public IPs. For more information on configuration, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789).

### Step 5. Connect to the TencentDB for SQL Server instance over the public network
1. Download and install [SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) locally. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
2. Start SSMS locally. On the **Connect to Server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
 - **Server type**: Select **Database Engine**.
 - **Server name**: Enter the local IP address and port number of the CLB instance and separate them by comma, such as `10.0.0.1,4000`.
 -  **Authentication**: Select **SQL Server Authentication**.
 -  **Login** and **Password**: Enter the account name and password you configured when creating the instance account on the **Account Management** tab.
![](https://main.qcloudimg.com/raw/14d90aa2eda6c841680f0fdc74db8219.png)
3. Once connected to the database, you can view the standard built-in system databases (master, model, msdb, and tempdb) of SQL Server.
![](https://main.qcloudimg.com/raw/c65c02197b506bd5b326128f1a3983a0.png)
4. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS will return the TencentDB for SQL Server instance.
![](https://qcloudimg.tencent-cloud.cn/raw/620a6143d5687581e9f2892e3fb76130.png)

## [Using a Linux CVM Instance with a Public IP to Map the Ports and Connecting to the Instance from a Local Computer Through SSMS](id:WWIPLJSL)

>?
>- The CVM and TencentDB instances must be in the same VPC in the same region under the same account.
>- For data security considerations, TencentDB for SQL Server doesn't support public IP. If you need to use a public IP, you can use the port mapping feature of SSH2 to connect to, configure, and manage an instance from the internet.

1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). On the instance details page, view the private IP and port number of the instance, which will be used for configuring port mapping.
![](https://main.qcloudimg.com/raw/343f649c398b60f859c4aa5b47d7d47f.png)
2. Prepare a Linux CVM instance with a public IP. For more information, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
3. Log in to the Linux CVM instance locally with an SSH tool such as SecureCRT (as demonstrated in this document). For the login method, see [Logging in to Linux Instance (Web Shell)](https://intl.cloud.tencent.com/document/product/213/5436).
4. Select **Options** > **Session Options** on the SecureCRT menu bar to enter the session properties settings page.
![](https://main.qcloudimg.com/raw/acbb1ad0a808ac59a0053063b75aab8b.png)
5. On the session properties settings page, select **Connection** > **Port Forwarding** > **Add** to enter the port mapping configuration page.
![](https://main.qcloudimg.com/raw/05f0cadcda75c6f931f34eb296a5ab6f.png)
6. On the port mapping configuration page, configure relevant parameters.
![](https://main.qcloudimg.com/raw/e364bded7f3611ef9da1eae0c1d575bd.png)
7. Download and install [SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) locally. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
8. Start SSMS locally. On the **Connect to Server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
 - **Server type**: Select **Database Engine**.
 - **Server name**: Enter the local IP address and port number and separate them by comma, such as `10.0.0.1,4000`. The port number should be the same as that configured in step 6.
 -  **Authentication**: Select **SQL Server Authentication**.
 -  **Login** and **Password**: Enter the account name and password you configured when creating the instance account on the **Account Management** tab.
![](https://main.qcloudimg.com/raw/14d90aa2eda6c841680f0fdc74db8219.png)
9. Once connected to the database, you can view the standard built-in system databases (master, model, msdb, and tempdb) of SQL Server.
![](https://main.qcloudimg.com/raw/c65c02197b506bd5b326128f1a3983a0.png)
10. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS will return the TencentDB for SQL Server instance.
![](https://qcloudimg.tencent-cloud.cn/raw/620a6143d5687581e9f2892e3fb76130.png)
