TencentDB for MySQL supports both private and public network addresses, with the former enabled by default for you to access your instance over the private network and the latter enabled or disabled as needed. To access your database instance from a Linux or Windows CVM instance over the public network, you can enable the public network address. You can also enable public network access through CLB, but you must configure security group rules in this case.

This document describes how to enable public network access through CLB and connect to an instance through MySQL Workbench.

## Prerequisites
You have applied for using the backend service feature.
1. Go to the [Cross-Region CLB Binding 2.0 Application](https://cloud.tencent.com/apply/p/y72ehzwbwzk) page.
2. Fill out and submit the application.
3. [Submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=14&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20CLB&level3_id=1068&radio_title=%E9%85%8D%E9%A2%9D/%E7%99%BD%E5%90%8D%E5%8D%95&queue=96&scene_code=41669&step=2) to add the allowed types for the account.
 - If the CLB and TencentDB for MySQL instances are in the same VPC, add the `CLB_IP_VPCGW` and `CLB_IP_LB` types.
 - If the CLB and TencentDB for MySQL instances are in different VPCs, add the `CLB_IP_User ` type.

## Step 1. Purchase a CLB instance
>?If you already have a CLB instance in the same region as TencentDB for MySQL, skip this step.
>
Go to the [CLB purchase page](https://buy.cloud.tencent.com/clb), select the configuration, and click **Buy Now**.
>!
>- Region: You need to select the region where the TencentDB for MySQL instance is.
>- Network: You can select the same VPC as the instance or a different VPC.

## Step 2. Configure the CLB instance
The following describes how to configure the CLB instance in the same VPC as the database instance and in a different VPC respectively.

### Scenario 1. Deploying the CLB instance in the same VPC as the TencentDB for MySQL instance
1. Enable cross-VPC access so that the CLB instance can be bound to another private IP.
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the **Basic Info** page, click **Configure** in the **Real Server** section.
c. In the pop-up window, click **Submit**.

2. Configure a public network listener port.
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the instance management page, select the **Listener Management** tab and click **Create** below **TCP/UDP/TCP SSL Listener**.
c. In the pop-up window, complete the settings and click **Submit**.

### Scenario 2. Deploying the CLB instance in a different VPC as the TencentDB for MySQL instance
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

## Step 3. Bind a TencentDB for MySQL instance
1. After creating the listener, click it in **Listener Management** and click **Bind** on the right.
2. In the pop-up window, select **Other Private IPs** as the object type, enter the IP address and port of the TencentDB for MySQL instance, and click **OK**.
>!The login account must be a standard account (bill-by-IP). If binding fails, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

## Step 4. Configure the TencentDB for MySQL security group
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance) and select a region. In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Security Group** tab, click **Configure Security Group**, configure the security group rule to open all ports, and confirm that the security group allows access from public IPs. For more information on configuration, see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/I4a8207_37.png)

## Step 5. Connect to the instance through the MySQL Workbench client
1. Download MySQL Workbench from [MySQL Community Downloads](https://dev.mysql.com/downloads/) and install it.
 1. Go to the download page and click **MySQL Workbench**.
 2. Click **Download** after **Windows (x86, 64-bit), MSI Installer**.
 3. Click **No thanks, just start my download**.
2. After MySQL Workbench is installed, open it and click the plus sign after **MySQL Connections** to add the information of the target instance.
![](https://qcloudimg.tencent-cloud.cn/raw/1bdd5024d708284fd8dc06b2177e0ea6.png)
3. In the pop-up window, configure the following items and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/ec8f7b944542bc28721446a1e2dbede5.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Connection Name</td>
<td>Name the connection.</td></tr>
<tr>
<td>Connection Method</td>
<td>Select **Standard (TCP/IP)**.</td></tr>
<tr>
<td>Hostname</td>
<td>Enter the address of the CLB instance. You can view the VIP information in the basic information on the CLB instance details page.</td></tr>
<tr>
<td>Port</td>
<td>Enter the port of the CLB instance. You can view the TCP port number in listener management on the CLB instance details page.</td></tr>
<tr>
<td>Username</td>
<td>Enter the account name of the target MySQL instance, i.e., the account created in **Database Management** > **Account Management** on the instance management page.</td></tr>
<tr>
<td>Store in Vault...</td>
<td>Enter the account password of the target MySQL instance in the **Password** field and save it.</td></tr>
</tbody></table>
4. Return to the MySQL Workbench homepage and click the just configured instance to connect to it.
![](https://qcloudimg.tencent-cloud.cn/raw/04cb6e563f25bedcaad235be50890aec.png)
5. The UI after successful connection is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/ad6c60db6691f5b2f825d36362877fe7.png)
