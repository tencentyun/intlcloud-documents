## Overview
This article describes how to install MySQL 8.0 on a CVM instance with Windows Server 2012 R2 Datacenter Edition 64bit. 
SQL Server is perhaps the most popular database software on Windows. However, it is commercial and requires you to obtain your own license. As an alternative, you can purchase [CDB instances for Tencent Cloud SQLServer database](https://intl.cloud.tencent.com/product/sqlserver?from_cn_redirect=1).

## Procedure

### Downloading MySQL
1. Log in to your CVM instance.
2. Open a browser window and go to the [official MySQL site](https://www.mysql.com/) to download the MySQL installation file.

### Installing MySQL

1. Launch the MySQL installer by double-clicking the installation file. The **Choose a Setup Type** window appears. Select **Developer Default** and click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/4077db7bfe9f7b97e1d7ddd649efa966.png)
2. In the **Check Requirements** window that appears, click **Execute** and resolve unmet requirements as shown in the figure below:
![](https://main.qcloudimg.com/raw/16a5f7190d7720562681528072cf8129.png)
3. Click **Next**.
4. In the **Installation** window, click **Execute** to install the required packages, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1b4a3e338bb816e7c47b4603a7a1dbb4.png)
5. Click **Next** when the package installation finishes to open the **Product Configuration** window.


### Configuring MySQL

#### Configuring MySQL service

1. In the **Product Configuration** window, click **Next** to open the **High Availability** window.
2. Select **Standalone MySQL Server / Classic MySQL Replication** and click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5355f286598388f9e9846bf8122e6d98.png)
3. In the **Type and Networking** window, keep the default configuration. Click **Next**, as shown in the following figure:
> 
> - TCP/IP network is enabled by default.
> - Port 3306 is used by default.
> 
![](https://main.qcloudimg.com/raw/fbece2fafb34beb5825ae294a8e214fd.png)
4. In the **Authentication Method** window, keep the default configuration. Click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/402624aaf02dce01ca2912d3548c03de.png)
5. Set a root password and click **Next** as shown in the following figure:
![](https://main.qcloudimg.com/raw/a0472f0b93c590997e78c2f590a0f901.png)
6. In the **Windows Service** window, keep the default configuration and click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a85625c446218a275e743ff0ec599ece.png)
7. In the **Apply Configuration** window, click **Execute**.
![](https://main.qcloudimg.com/raw/2ee6000630d88774951ddf8aaea16fbb.png)
8. Click **Finish** to complete MySQL configuration.

#### Configuring MySQL Router

1. In the **Product Configuration** window, click **Next**.
2. In the **MySQL Router Configuration** window, keep the default configuration and click **Finish**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/adece1334b6e1579eb2ace782cf47c59.png)

#### Configuring MySQL samples

1. In the **Product Configuration** window, click **Next**.
2. In the **Connect to Server** window, input the root password. Click **Check**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/ab8637391012a14ab2e5160c61675912.png)
3. After the password is successfully authenticated, click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/bff0aece8da11d15a52f4db91b4d7e69.png)
4. In the **Apply Configuration** window, click **Execute**.
![](https://main.qcloudimg.com/raw/8fe1f90eed50860e064044b314719cf6.png)
5. Click **Finish** to complete the MySQL sample configuration.
6. In the **Product Configuration** window, click **Next**.
7. In the **Installation Complete** window, select the MySQL environment component you want to start and click **Finish**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/13f46296b85b00ce7e3bd08be13108c9.png)
 - If MySQL Workbench starts, MySQL is successfully installed, as shown in the following figure:
![](https://main.qcloudimg.com/raw/288f4cfbf1a9671b73dff64a940e0dc1.png)
 - If MySQL Shell starts, MySQL is successfully installed, as shown in the following figure:
![](https://main.qcloudimg.com/raw/90b788ffe3a8f92e0e5e70f35fb94356.png)


### Adding Security Group Rules

Add an inbound rule to allow traffic on port 3306 to the security group that is bound to the CVM instance on which MySQL is installed.




