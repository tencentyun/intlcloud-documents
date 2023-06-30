## Overview
This document describes how to install MySQL 8.0.19 on a CVM instance with the Windows Server 2012 R2 DataCenter 64-bit English installed.
SQL Server is more popular on Windows. However, it is commercial and requires you to obtain your own license. As an alternative, you can purchase a [TencentDB for SQL Server instance](https://intl.cloud.tencent.com/zh/products/sqlserver).

## Directions

### Downloading MySQL
1. Log in to your CVM.
2. Open a browser and go to the [MySQL official website](https://www.mysql.com/) to download the MySQL installation file.

### Installing MySQL

1. Double-click the MySQL installation file. The **Choosing a Setup Type** window appears. Select **Developer Default** and click **Next**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/46578b0e47c0a8283c72680070578916.png)
2. In the **Check Requirements** window that appears, click **Execute** and resolve unmet requirements.
3. Click **Next**.
4. In the **Installation** window, click **Execute** to install the required packages.
5. Click **Next** when the package installation completes to open the **Product Configuration** window.


### Configuring MySQL

#### Configuring MySQL service

1. In the **Product Configuration** window, click **Next*.
2. In the **High Availability** window, select **Standalone MySQL Server / Classic MySQL Replication** and click **Next**, as shown below.
![](https://qcloudimg.tencent-cloud.cn/raw/821c0ab18a477ffdf3458889ff698b08.png)
3. In the **Type and Networking** window, keep the default configuration, and click **Next**.
<dx-alert infotype="explain" title="">
- TCP/IP network is enabled by default.
- Port 3306 is used by default.
</dx-alert>
4. In the **Authentication Method** window, select <b>Use Legacy Authentication Method(Retain MySQL 5.x Compatibility)</b> and click **Next**.
In this document, this option is set to set up a WordPress website as an example. You can set it as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/599dff879af20e25ce1d8e7fb5b1a33f.png)
5. Set the password for the `root` user and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/a85f3a6affb6d71dda27a7a1fe5a5870.png)
6. In the **Windows Service ** window, keep the default configuration, and click **Next**.
7. In the **Apply Configuration** window, click **Execute**.
8. Click **Finish**.

#### Configuring MySQL router

1. In the **Product Configuration** window, click **Next*.
2. In the **MySQL Router Configuration** window, keep the default configuration and click **Finish**.
![](https://qcloudimg.tencent-cloud.cn/raw/f13a5db6d40390a3b5c650e00720d587.png)

#### Configuring MySQL samples

1. In the **Product Configuration** window, click **Next*.
2. In the **Connect To Server** window, input the root password, and click **Check**.
3. After the password is successfully authenticated, click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/5e4157ae76b5ae7aa4f7e9d99f40bfe8.png)
4. In the **Apply Configuration** window, click **Execute**.
5. Click **Finish** to complete the MySQL sample configuration.
6. In the **Product Configuration** window, click **Next*.
7. In the **Installation Complete** window, select the MySQL environment component you want to start and click **Finish**.
   - If MySQL Workbench as shown below starts, MySQL has been successfully installed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7f960c3d6e8c26f9fb68ee9de5d5b96b.png)
   - If MySQL Shell as shown below starts, MySQL has been successfully installed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/985d2e239aae0bcc1d84f51e3eecd296.png)


### Adding security group rules

Add an inbound rule to open the port 3306 to the security group that is bound to the CVM instance on which MySQL is installed.
For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).





