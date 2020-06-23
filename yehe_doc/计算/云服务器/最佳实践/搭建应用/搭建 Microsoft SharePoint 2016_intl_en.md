## Overview
This document introduces how to build Microsoft SharePoint 2016 on a CVM instance.

## Software Versions
This document uses the CVM instance with the following hardware specification as an example:
- vCPU: 4 cores
- Memory: 8 GB

This document uses the following software versions as an example:
- Operating system: Windows Server 2012 R2 Datacenter 64-bit (Chinese)
- Database: SQL Server 2014

## Prerequisites
You have purchased a Windows CVM. If you have not yet, see [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516).

## Directions

### Step 1: logging in to the Windows instance
You can either [logging in to a Windows instance using the RDP file (recommended)](https://intl.cloud.tencent.com/document/product/213/5435) or [logging into a Windows instance via remote desktop](https://intl.cloud.tencent.com/document/product/213/32498).

<span id="AddAD_DHCP_DNS_IIS"></span>
### Step 2: adding AD, DHCP, DNS and IIS services
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
2. Select **Local Server** in the left sidebar, and locate **IE Enhanced Security Configuration**, as shown below:
![](https://main.qcloudimg.com/raw/c2b0791555bbc910cea70732c75daa0f.png)
3. Disable **IE Enhanced Security Configuration**, as shown below:
![](https://main.qcloudimg.com/raw/6acbf171bc703100401e48e362539b21.png)
4. Select **Dashboard** in the left sidebar, and click **Add roles and features**.
5. In the “Add Roles and Features Wizard” window, keep the default configurations and click **Next** 3 times.
6. On the **Server Roles** page, select **Active Directory Domain Services**, **DHCP Server**, **DNS Server**, **Web Server (IIS)**, and click **Add Features** in the pop-up window, as shown below:
![](https://main.qcloudimg.com/raw/a2bb1c86c9277ca870c629ecf5b0d3f5.png)
7. Click **Next**.
8. On the **Features** page, select **.NET Framework 3.5 Features** to add features, as shown below:
![](https://main.qcloudimg.com/raw/bf47abbb95ad42b9d6c720c3bb2c846b.png)
9. Keep the default configurations and click **Next** until the **Confirmation** page appears.
10. Confirm the installation, and click **Install**.
11. After the installation is complete, restart the CVM.
12. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager*.
13. Click <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> and select **Promote this server to a domain controller**, as shown below:
![](https://main.qcloudimg.com/raw/1e6aa1d75044898357709909bb969c6f.png)
14. <span id="step14"></span>In the **Active Directory Domain Services Configuration Wizard** window, select **Add a new forest**, enter a domain name in the **Root domain name** field, and click **Next**.
![](https://main.qcloudimg.com/raw/017acc0e5939632f3808698f36320fd2.png)
15. <span id="step15"></span>Under **Type the Directory Services Restore Mode (DSRM) password**, set the password, and click **Next**.
![](https://main.qcloudimg.com/raw/078672b95294790e4985108bd58d8504.png)
16. Keep the default configurations and click **Next** until the configuration is complete.
17. Click **Install**.
18. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
19. Click <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> and select **Complete DHCP configuration**, as shown below:
![](https://main.qcloudimg.com/raw/4c65a7990acc647866d73c1b5ba20a6c.png)
20. In the **DHCP Post-Install configuration wizard** window, click **Next**.
21. Keep the default configurations and click **Commit** to complete the installation.
![](https://main.qcloudimg.com/raw/4162a8fbde1b7af1d8fadacaa61965cf.png)
22. Click **Close**.

### Step 3: installing SQL Server 2014 database

1. Open the browser on CVM and download the SQL Server 2014 installation package from the SQL Server 2014 official site.
> You may also obtain the SQL Server 2014 installation package from a third-party website or other valid channels.
>
2. Double click the “Setup.exe” file to start the installation wizard, as shown below:
![](https://main.qcloudimg.com/raw/f2cc33aef5ec2662238ffeca56d08a7d.png)
3. Select **New SQL Server stand-alone installation or add features to an existing installation**.
4. On the **Product Key** page, enter the product key and click **Next**.
5. Select **I accept the license terms**, and click **Next**.
6. Keep the default configurations, and click **Next**.
7. After the installation check is complete, click **Next**.
8. Keep the default configurations, and click **Next**.
9. On the **Feature Selection** page, click **Select All** to select all features, and click **Next**.
![](https://main.qcloudimg.com/raw/92eac7b681dae5937bafa484874ae122.png)
10. On the **Instance Configuration** page, select **Default instance**, and click **Next**.
![](https://main.qcloudimg.com/raw/2bf1682b927b66224c574435ee35e7af.png)
11. On the **Server Configuration -> Service Accounts** page, configure the account and password for SQL Server Database Engine and SQL Server Analysis Services, and click **Next**.
![](https://main.qcloudimg.com/raw/1310d9db077772be6dad6f58a698273e.png)
 - Set the account name of **SQL Server Database Engine** to “NT AUTHORITY\NETWORK SERVICE”.
 - Set the account name and password of **SQL Server Analysis Services** to the domain name and password configured in [14](#step14) to [15](#step15) in [Step 2: adding AD, DHCP, DNS, and IIS services](#AddAD_DHCP_DNS_IIS).
12. On the **Database Engine Configuration -> Server Configuration** page, select **Add Current User** to use the current account as the administrator account of SQL Server, and click **Next**.
![](https://main.qcloudimg.com/raw/90ac80988b45a6b08650d97fd0d08c09.png)
13. On the **Analysis Services Configuration -> Account Provisioning** page, select **Add Current User** to grant the current account with administrator permissions for Analysis Services, and click **Next**.
![](https://main.qcloudimg.com/raw/5fda4e9b2ac31d8394ab0dfa14847d73.png)
14. Keep the default configurations, and click **Next**.
15. On the **Distributed Replay Controller** page, click **Add Current User** to grant the current account with access permissions for the Distributed Replay controller service.
![](https://main.qcloudimg.com/raw/2b67cc38051c51cb88ba7bbb740027b3.png)
16. Keep the default configurations, and click **Next**.
17. Confirm the SQL Server configurations, and click **Install**.
18. After the installation is complete, click **Close**.


### Step 4: installing SharePoint 2016

1. Open the browser on CVM and download the Microsoft SharePoint 2016 installation package from the Microsoft SharePoint 2016 official site.
2. Open the “Microsoft SharePoint 2016” image file, double-click the executable file `prerequisiteinstaller.exe` of the preparation tool to install the Microsoft SharePoint 2016 Preparation Tool, as shown below:
![](https://main.qcloudimg.com/raw/1c6c2e0970ea456bbabd4a77ef454a5e.png)
3. Open the installation wizard of the Microsoft SharePoint 2016 Preparation Tool and click **Next**.
![](https://main.qcloudimg.com/raw/4b42cde60ca558a7c905c6f8031e3a50.png)
4. Select **I accept the terms of the License Agreement(s)**, and click **Next**.
5. After the preparation tool is installed, click **Finish** to restart the CVM.
![](https://main.qcloudimg.com/raw/a8c14625c359decb9941511e267ea2a6.png)
6. Open the “Microsoft SharePoint 2016” image file, double-click the installation file `setup.exe` to install Microsoft SharePoint 2016.
![](https://main.qcloudimg.com/raw/2614739955551657148d9c3a72e566df.png)
7. Enter the product key, and click **Continue**.
8. Select **I accept the terms of this agreement**, and click **Continue**.
9. Select the installation directory (this example keeps the default configuration but you can specify a directory as needed), and click **Install Now**.
![](https://main.qcloudimg.com/raw/3ea703e1632ec78b3f8f4b961c189208.png)
10. When the installation is complete, select **Run the SharePoint Products Configuration Wizard now**, and click **Close**.
![](https://main.qcloudimg.com/raw/368fa9a4cdb3b47a77c554db855737e0.png)

### Step 5: configuring SharePoint 2016

1. In the **SharePoint Products Configuration Wizard** window, click **Next**.
![](https://main.qcloudimg.com/raw/73aa25130b0e24e6784760a28d6d8fe2.png)
2. Click **Yes** in the pop-up dialog box to allow service restart during the configuration.
3. Select **Create a new server farm**, and click **Next**.
![](https://main.qcloudimg.com/raw/b66da626c4883f2f2fb1b75bce6042f6.png)
4. On the **Specify Configuration Database Settings** page, set the configuration database and the access account.
The SharePoint database is on the local host, so you need to enter the local database and account. Then, click **Next**.
![](https://main.qcloudimg.com/raw/d1ccac780ddb9fb308b071fe385ad3f6.png)
5. Enter the password of the server farm and click **Next**.
6. Select **Front-end** for “Multiple-Server Farm” and click **Next**.
![](https://main.qcloudimg.com/raw/c23051f73ae543002bc9c15d3d2b3387.png)
7. Specify the port number of SharePoint Central Administration Web Application (this example uses “10000” but you can configure the number as needed), and click **Next**.
![](https://main.qcloudimg.com/raw/c7622761e6eb45b1935fccc851379b29.png)
8. Confirm the SharePoint configurations, and click **Next**.
![](https://main.qcloudimg.com/raw/8d97c6aff42bb8b27fb3e108fa3d16d8.png)
9. After the configuration is complete, click **Finish**.

