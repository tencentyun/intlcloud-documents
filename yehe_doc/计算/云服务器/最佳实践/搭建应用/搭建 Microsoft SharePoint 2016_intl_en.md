## Overview
This document introduces how to build Microsoft SharePoint 2016 on a CVM instance.

## Software
This document uses the CVM instance with the following hardware specification as an example:
- vCPU: 4 cores
- Memory: 8 GB

This document uses the following software versions as an example:
- Operating system: Windows Server 2012 R2 Datacenter 64-bit (English)
- Database: SQL Server 2014

## Prerequisites
Purchase a Windows CVM instance. See [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516).

## Directions

### Step 1. Log in to the Windows instance
You can either log in to the Windows instance by using [RDP](https://intl.cloud.tencent.com/document/product/213/5435) or [a remote desktop](https://intl.cloud.tencent.com/document/product/213/32498).


### Step 2. Add AD, DHCP, DNS, and IIS services[](id:AddAD_DHCP_DNS_IIS)
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
2. On the left sidebar, select **Local Server** and find **IE Enhanced Security Configuration**.
![](https://main.qcloudimg.com/raw/c2b0791555bbc910cea70732c75daa0f.png)
3. Disable **IE Enhanced Security Configuration**.
![](https://main.qcloudimg.com/raw/6acbf171bc703100401e48e362539b21.png)
4. On the left sidebar, select **Dashboard** and click **Add roles and features**.
5. In the **Add Roles and Features Wizard** window, keep the default configurations and click **Next** for the current window and the next two windows.
6. On the **Select server roles** page, select **Active Directory Domain Services**, **DHCP Server**, **DNS Server**, and **Web Server (IIS)** and click **Add Feature** in the pop-up window.
![](https://main.qcloudimg.com/raw/a2bb1c86c9277ca870c629ecf5b0d3f5.png)
7. Click **Next**.
8. On the **Features** page, select **.NET Framework 3.5 Features** and click **Add features** in the pop-up window.
![](https://main.qcloudimg.com/raw/bf47abbb95ad42b9d6c720c3bb2c846b.png)
9. Keep the default configuration and click **Next** for the current window and the next five windows.
10. Confirm the installation and click **Install**.
11. After the installation is complete, restart the CVM instance.


### Step 3. Configure the AD service
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
2. Click <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> and select **Promote this server to a domain controller**.
![](https://main.qcloudimg.com/raw/1e6aa1d75044898357709909bb969c6f.png)
3. [](id:step14) In the **Active Directory Domain Services Configuration Wizard** pop-up window, set **Select the deployment operation** to **Add a new forest**, enter the root domain name, and click **Next**.
![](https://main.qcloudimg.com/raw/017acc0e5939632f3808698f36320fd2.png)
4. [](id:step15) Set the Directory Services Restore Mode (DSRM) password and click **Next**.
![](https://main.qcloudimg.com/raw/078672b95294790e4985108bd58d8504.png)
5. Keep the default configuration and click **Next** for the current window and the next three windows.
6. Click **Install**.

### Step 4. Configure the DHCP service
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
2. Click <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> and select **Complete DHCP configuration**.
![](https://main.qcloudimg.com/raw/4c65a7990acc647866d73c1b5ba20a6c.png)
3. In the **DHCP Post-Install configuration wizard** pop-up window, click **Next**.
4. Keep the default configurations and click **Commit**.
![](https://main.qcloudimg.com/raw/4162a8fbde1b7af1d8fadacaa61965cf.png)
5. Click **Close**.

### Step 5. Install the SQL Server 2014 database

1. Open the browser in the CVM instance and download the SQL Server 2014 installation package from the SQL Server 2014 official site.
<dx-alert infotype="explain" title="">
You may also obtain the SQL Server 2014 installation package from a third-party website or other valid channels.
</dx-alert>
2. Double-click the `Setup.exe` file to open the SQL Server installation wizard. On the **SDL Server Installation Center**, click **New SDL Server stand-alone installation or add features to an existing installation**.
![](https://main.qcloudimg.com/raw/f2cc33aef5ec2662238ffeca56d08a7d.png)
3. Enter the product key and click **Next**.
4. Select **I accept the license terms** and click **Next**.
5. Keep the default configuration and click **Next**.
6. After the installation check is completed, click **Next**.
7. Keep the default configuration and click **Next**.
8. On the **Feature Selection** page, click **Select All** and click **Next**.
![](https://main.qcloudimg.com/raw/92eac7b681dae5937bafa484874ae122.png)
9. On the **Instance Configuration** page, select **Default instance** and click **Next**.
![](https://main.qcloudimg.com/raw/2bf1682b927b66224c574435ee35e7af.png)
10. On the **Server Configuration** page, configure the account and password for SQL Server Database Engine and SQL Server Analysis Services and click **Next**.
![](https://main.qcloudimg.com/raw/1310d9db077772be6dad6f58a698273e.png)
 - Set the account name of **SQL Server Database Engine** to "NT AUTHORITY\NETWORK SERVICE".
 - Set the account name and password of **SQL Server Analysis Services** to the domain name and password configured in [14](#step14) to [15](#step15) in [Step 2. Add AD, DHCP, DNS, and IIS services](#AddAD_DHCP_DNS_IIS).
11. On the **Database Engine Configuration** page, select **Add Current User** to use the current account as the admin account of SQL Server and click **Next**.
![](https://main.qcloudimg.com/raw/90ac80988b45a6b08650d97fd0d08c09.png)
12. On the **Analysis Services Configuration** page, select **Add Current User** to grant the current account the admin permission for **Analysis Services** and click **Next**.
![](https://main.qcloudimg.com/raw/5fda4e9b2ac31d8394ab0dfa14847d73.png)
13. Keep the default configuration and click **Next**.
14. On the **Distributed Replay Controller** page, click **Add Current User** to grant the current account the access permission of **Distributed Replay Controller** and click **Next**.
![](https://main.qcloudimg.com/raw/2b67cc38051c51cb88ba7bbb740027b3.png)
15. Keep the default configuration and click **Next** until the installation is completed.


### Step 6. Install SharePoint 2016

1. Open the browser in the CVM instance and download the Microsoft SharePoint 2016 installation package from the Microsoft SharePoint 2016 official site.
2. Open the `Microsoft SharePoint 2016` image file, double-click the `prerequisiteinstaller.exe` file of the preparation tool to install the Microsoft SharePoint 2016 Preparation Tool.
![](https://main.qcloudimg.com/raw/1c6c2e0970ea456bbabd4a77ef454a5e.png)
3. Open the installation wizard of the Microsoft SharePoint 2016 Preparation Tool and click **Next**.
![](https://main.qcloudimg.com/raw/4b42cde60ca558a7c905c6f8031e3a50.png)
4. Select **I accept the terms in the license agreement.** and click **Next**.
5. After the required prerequisites are installed, click **Finish** to restart the CVM instance.
![](https://main.qcloudimg.com/raw/a8c14625c359decb9941511e267ea2a6.png)
6. Open the Microsoft SharePoint 2016 image file and double-click the `setup.exe` installation file to install Microsoft SharePoint 2016.
![](https://main.qcloudimg.com/raw/2614739955551657148d9c3a72e566df.png)
7. Enter the product key and click **Continue**.
8. Select **I accept the terms of this agreement** and click **Next**.
9. Select the installation directory (this example keeps the default configuration but you can specify a directory as needed), and click **Install Now**.
![](https://main.qcloudimg.com/raw/3ea703e1632ec78b3f8f4b961c189208.png)
10. When the installation is completed, select **Run the SharePoint Products Configuration Wizard now** and click **Close**.
![](https://main.qcloudimg.com/raw/368fa9a4cdb3b47a77c554db855737e0.png)

### Step 7. Configure SharePoint 2016

1. In the **SharePoint Products Configuration Wizard** window, click **Next**.
![](https://main.qcloudimg.com/raw/73aa25130b0e24e6784760a28d6d8fe2.png)
2. Click **Yes** in the pop-up window to allow service restart during the configuration.
3. Select **Create a new server farm** and click **Next**.
![](https://main.qcloudimg.com/raw/b66da626c4883f2f2fb1b75bce6042f6.png)
4. Configure the database, specify the database access account, and click **Next**.
The SharePoint database is on the local host, so you need to enter the local database and account.
![](https://main.qcloudimg.com/raw/d1ccac780ddb9fb308b071fe385ad3f6.png)
5. Enter the password of the server farm and click **Next**.
6. Set **Multiple-Server Farm** to **Front-end** and click **Next**.
![](https://main.qcloudimg.com/raw/c23051f73ae543002bc9c15d3d2b3387.png)
7. Specify the port number of SharePoint Central Administration Web Application (this example uses `10000`), and click **Next**.
![](https://main.qcloudimg.com/raw/c7622761e6eb45b1935fccc851379b29.png)
8. Confirm the SharePoint configuration and click **Next**.
![](https://main.qcloudimg.com/raw/8d97c6aff42bb8b27fb3e108fa3d16d8.png)
9. After the SharePoint configuration is completed, click **Finish**.

