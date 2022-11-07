TencentDB for SQL Server supports both private and public network addresses, with the former enabled by default for you to access your instance over the private network and the latter enabled or disabled as needed. To access your database instance from a Linux or Windows CVM instance over the public network, you can enable the public network address. You can also enable public network access through CLB, but you must configure security group rules in this case.

This document describes how to enable public network access through CLB, connect to the instance through SQL Server Management Studio (SSMS), and run a simple query.

## Step 1. Purchase a CLB instance
>?If you already have a CLB instance in the same region as TencentDB for SQL Server, skip this step.
>
>Go to the [CLB purchase page](https://buy.intl.cloud.tencent.com/clb), select the configuration, and click **Buy Now**.
>!
>
>- Region: You need to select the region where the TencentDB for SQL Server instance is.
>- Network: You can select the same VPC as the instance or a different VPC.

## Step 2. Configure the CLB instance
The following describes how to configure the CLB instance in the same VPC as the database instance and in a different VPC respectively.

### Scenario 1. Deploying the CLB instance in the same VPC as the TencentDB for SQL Server instance
1. Enable cross-VPC access so that the CLB instance can be bound to another private IP.
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the **Basic Info** page, click **Configure** in the **Real Server** section.
c. In the pop-up window, click **Submit**.

2. Configure a public network listener port.
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the instance management page, select the **Listener Management** tab and click **Create** below **TCP/UDP/TCP SSL Listener**.
![](https://qcloudimg.tencent-cloud.cn/raw/b30504cee130711bbef74021f19415fe.png)
c. In the pop-up window, complete the settings and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/d4cecb308bbb741997b54753f9a3b983.png)

### Scenario 2. Deploying the CLB instance in a different VPC as the TencentDB for SQL Server instance
1. Enable cross-VPC access so that the CLB instance can be bound to another private IP.
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the **Basic Info** page, click **Configure** in the **Real Server** section.
c. In the pop-up window, click **Submit**.
d. Click **Add SNAT IP** under **Backend service**.
e. In the pop-up window, select a **Subnet**, click **Add** next to **Assign IP**, select **Auto** or manually enter the assigned IP, and click **Save**.
2. Configure a public network listener port.
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the instance management page, select the **Listener Management** tab and click **Create** below **TCP/UDP/TCP SSL Listener**.
![](https://qcloudimg.tencent-cloud.cn/raw/d0f5d8224e839d2a2c8fd27f155e5916.png)
c. In the pop-up window, complete the settings and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/742ad6617e66d2baeece8986c137d414.png)

## Step 3. Bind a TencentDB for SQL Server instance
1. After creating the listener, click it in **Listener Management** and click **Bind** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/7ffb1699243706eac9fc303863bbc76a.png)
2. In the pop-up window, select **Other Private IPs** as the object type, enter the IP address and port of the TencentDB for SQL Server instance, and click **OK**.
>!The login account must be a standard account (bill-by-IP). If binding fails, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

## Step 4. Configure the TencentDB for SQL Server security group
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select a region, and click the ID of the target instance in the instance list or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Security Group** tab, click **Configure Security Group**, configure the security group rule to open all ports, and confirm that the security group allows access from public IPs. For more information on configuration, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789).
![](https://qcloudimg.tencent-cloud.cn/raw/37a72a8346be3934e21b003a43f31095.png)

## Step 5. Connect to the TencentDB for SQL Server instance over the public network
1. Download and install [SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) locally. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
2. Start SSMS locally. On the **Connect to Server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
![](https://main.qcloudimg.com/raw/14d90aa2eda6c841680f0fdc74db8219.png)
 - **Server type**: Select **Database Engine**.
 - **Server name**: Enter the local IP address and port number of the CLB instance and separate them by comma, such as `10.0.0.1,4000`.
 -  **Authentication**: Select **SQL Server Authentication**.
 -  **Login** and **Password**: Enter the account name and password you configured when creating the instance account on the **Account Management** tab.
3. Once connected to the database, you can view the standard built-in system databases (master, model, msdb, and tempdb) of SQL Server.
![](https://main.qcloudimg.com/raw/c65c02197b506bd5b326128f1a3983a0.png)
4. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS will return the TencentDB for SQL Server instance.
![](https://qcloudimg.tencent-cloud.cn/raw/620a6143d5687581e9f2892e3fb76130.png)

