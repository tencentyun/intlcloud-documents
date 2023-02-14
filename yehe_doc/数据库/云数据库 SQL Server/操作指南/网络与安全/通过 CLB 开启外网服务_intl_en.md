TencentDB for SQL Server supports both private and public network addresses, with the former enabled by default for you to access your instance over the private network and the latter enabled or disabled as needed. To access your database instance from a Linux or Windows CVM instance over the public network, you can enable the public network address. You can also enable public network access through CLB, but you must configure security group rules in this case.

This document describes how to bind a TencentDB for SQL Server instance to CLB to enable public network access, connect to the instance through SQL Server Management Studio (SSMS), and run a simple query.

## Prerequisites
You have applied for using the backend service feature.
1. Go to the [Cross-Region CLB Binding 2.0 Application](https://cloud.tencent.com/apply/p/y72ehzwbwzk) page.
2. Fill out and submit the application.
3. [Submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=14&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20CLB&level3_id=1068&radio_title=%E9%85%8D%E9%A2%9D/%E7%99%BD%E5%90%8D%E5%8D%95&queue=96&scene_code=41669&step=2) to add the allowed types for the account.
 - If the CLB and TencentDB for SQL Server instances are in the same VPC, add the `CLB_IP_VPCGW` and `CLB_IP_LB` types.
 - If the CLB and TencentDB for SQL Server instances are in different VPCs, add the `CLB_IP_User ` type.

## Step 1. Purchase a CLB instance
>?If you already have a CLB instance in the same region as TencentDB for SQL Server, skip this step.
>
Go to the [CLB purchase page](https://buy.cloud.tencent.com/clb), select the configuration, and click **Buy Now**.
>!
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
c. In the pop-up window, complete the settings and click **Submit**.

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
c. In the pop-up window, complete the settings and click **Submit**.

## Step 3. Bind a TencentDB for SQL Server instance
1. After creating the listener, click it in **Listener Management** and click **Bind** on the right.
2. In the pop-up window, select **Other Private IPs** as the object type, enter the IP address and port of the TencentDB for SQL Server instance, and click **OK**.
>!The login account must be a standard account (bill-by-IP). If binding fails, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

## Step 4. Configure the TencentDB for SQL Server security group
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select a region, and click the ID of the target instance in the instance list or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Security Group** tab, click **Configure Security Group**, configure the security group rule to open all ports, and confirm that the security group allows access from public IPs. For more information on configuration, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789).

## Step 5. Connect to the TencentDB for SQL Server instance over the public network
1. Download and install [SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) locally. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
2. Start SSMS locally. On the **Connect to Server** page, enter the relevant information to connect to TencentDB. Click **Connect** and wait a few minutes before SSMS connects to your database instance.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Yv5d706_47.png)
 - **Server type**: Select **Database Engine**.
 - **Server name**: Enter the local IP address and port number of the CLB instance and separate them by a comma, such as `10.0.0.1,4000`.
 -  **Authentication**: Select **SQL Server Authentication**.
 -  **Login** and **Password**: Enter the account name and password you configured when creating the instance account on the **Account Management** tab.
3. Once connected to the database, you can view the standard built-in system databases (master, model, msdb and tempdb) of SQL Server.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/tkFj449_49.png)
4. Now you can start creating your own databases and running queries for them. Select **File** > **New** > **Query with Current Connection** and type the following SQL query:
```
select @@VERSION
```
Run the query. SSMS returns the SQL Server version of TencentDB instance.
![](https://qcloudimg.tencent-cloud.cn/raw/620a6143d5687581e9f2892e3fb76130.png)

