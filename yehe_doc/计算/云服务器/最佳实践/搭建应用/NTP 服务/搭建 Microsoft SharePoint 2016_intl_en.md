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
![](https://main.qcloudimg.com/raw/9192efa291cfbed136db9a6e3a7c3e59.png)
3. Disable **IE Enhanced Security Configuration**, as shown below:
![](https://main.qcloudimg.com/raw/8b860bb5dfc44ec4993c3a899058b1ae.png)
4. Select **Dashboard** in the left sidebar, and click **Add roles and features**.
5. In the “Add Roles and Features Wizard” window, keep the default configurations and click **Next** 3 times.
6. On the **Server Roles** page, select **Active Directory Domain Services**, **DHCP Server**, **DNS Server**, **Web Server (IIS)**, and click **Add Features** in the pop-up window, as shown below:
![](https://main.qcloudimg.com/raw/532dc46bf0682427e9b210bf36e1986f.png)
7. Click **Next**.
8. On the **Features** page, select **.NET Framework 3.5 Features** to add features, as shown below:
![](https://main.qcloudimg.com/raw/44998bf3effff6bec51ea9c502ec8c9a.png)
9. Keep the default configurations and click **Next** until the configuration is complete.
10. Confirm the installation, and click **Install**.
11. After the installation is complete, restart the CVM.
12. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
13. Click <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> and select **Promote this server to a domain controller**, as shown below:
![](https://main.qcloudimg.com/raw/03def6c00f1bed979c9dde28ebbd2202.png)
14. <span id="step14"></span>In the **Active Directory Domain Services Configuration Wizard** window, select **Add a new forest**, enter a domain name in the **Root domain name** field, and click **Next**.
![](https://main.qcloudimg.com/raw/adb2e7cbed1580eebeb201d837f41efa.png)
15. <span id="step15"></span>Under **Type the Directory Services Restore Mode (DSRM) password**, set the password, and click **Next**.
![](https://main.qcloudimg.com/raw/dc24edd5f6d194cacc7b6ff8511417b7.png)
16. Keep the default configurations and click **Next** until the configuration is complete.
17. Click **Install**.
18. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
19. Click <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> and select **Complete DHCP configuration**, as shown below:
![](https://main.qcloudimg.com/raw/132eb061b6fd53da22b6211fd2411537.png)
20. In the **DHCP Post-Install configuration wizard** window, click **Next**.
21. Keep the default configurations and click **Commit** to complete the installation.
![](https://main.qcloudimg.com/raw/6dab6c5968282757ff2e146c74765772.png)
22. Click **Close**.

### Step 3: installing SQL Server 2014 database

1. Open the browser on CVM and download the SQL Server 2014 installation package from the SQL Server 2014 official site.
> You may also obtain the SQL Server 2014 installation package from a third-party website or other valid channels.
>
2. Double click the “Setup.exe” file to start the installation wizard, as shown below:
![](https://main.qcloudimg.com/raw/66c2d6df469197d5550ce2fbae3cc5c9.png)
3. Select **New SQL Server stand-alone installation or add features to an existing installation**.
4. On the **Product Key** page, enter the product key and click **Next**.
5. Select **I accept the license terms**, and click **Next**.
6. Keep the default configurations, and click **Next**.
7. After the installation check is complete, click **Next**.
8. Keep the default configurations, and click **Next**.
9. On the **Feature Selection** page, click **Select All** to select all features, and click **Next**.
![](https://main.qcloudimg.com/raw/15bb32c2d2121aadc092428911cefc16.png)
10. On the **Instance Configuration** page, select **Default instance**, and click **Next**.
![](https://main.qcloudimg.com/raw/3663ca417620325c7b45bc8c60996db7.png)
11. On the **Server Configuration -> Service Accounts** page, configure the account and password for SQL Server Database Engine and SQL Server Analysis Services, and click **Next**.
![](https://main.qcloudimg.com/raw/c0bb2b960115d66eda4e38b40a56fc78.png)
 - Set the account name of **SQL Server Database Engine** to “NT AUTHORITY\NETWORK SERVICE”.
 - Set the account name and password of **SQL Server Analysis Services** to the domain name and password configured in [14](#step14) to [15](#step15) in [Step 2: adding AD, DHCP, DNS, and IIS services](#AddAD_DHCP_DNS_IIS).
12. On the **Database Engine Configuration -> Server Configuration** page, select **Add Current User** to use the current account as the administrator account of SQL Server, and click **Next**.
![](https://main.qcloudimg.com/raw/c0218409bfb7044221cb6c0fe1862588.png)
13. On the **Analysis Services Configuration -> Account Provisioning** page, select **Add Current User** to grant the current account with administrator permissions for Analysis Services, and click **Next**.
![](https://main.qcloudimg.com/raw/43243a387cc67f20ea125fb2491df24d.png)
14. Keep the default configurations, and click **Next**.
15. On the **Distributed Replay Controller** page, click **Add Current User** to grant the current account with access permissions for the Distributed Replay controller service.
![](https://main.qcloudimg.com/raw/46158b2f9a6e5f802c2ae27a2f5f0970.png)
16. Keep the default configurations, and click **Next**.
17. Confirm the SQL Server configurations, and click **Install**.
18. After the installation is complete, click **Close**.


### Step 4: installing SharePoint 2016

1. Open the browser on CVM and download the Microsoft SharePoint 2016 installation package from the Microsoft SharePoint 2016 official site.
2. Open the “Microsoft SharePoint 2016” image file, double-click the executable file `prerequisiteinstaller.exe` of the preparation tool to install the Microsoft SharePoint 2016 Preparation Tool, as shown below:
![](https://main.qcloudimg.com/raw/2de50f6a3172bd870f86378e33f1f07e.png)
3. Open the installation wizard of the Microsoft SharePoint 2016 Preparation Tool and click **Next**.
![](https://main.qcloudimg.com/raw/e5cd9c8ca37b36984258050443fdf5f1.png)
4. Select **I accept the terms of the License Agreement(s)**, and click **Next**.
5. After the preparation tool is installed, click **Finish** to restart the CVM.
![](https://main.qcloudimg.com/raw/cc8f3bf7b151946d5fdd8f3882ea9549.png)
6. Open the “Microsoft SharePoint 2016” image file, double-click the installation file `setup.exe` to install Microsoft SharePoint 2016.
![](https://main.qcloudimg.com/raw/bf0369e20c77e1f57bfef3fef42fab31.png)
7. Enter the product key, and click **Continue**.
8. Select **I accept the terms of this agreement**, and click **Continue**.
9. Select the installation directory (this example keeps the default configuration but you can specify a directory as needed), and click **Install Now**.
![](https://main.qcloudimg.com/raw/0dbdfedb241b02a7f2fdaefb1a7599af.png)
10. When the installation is complete, select **Run the SharePoint Products Configuration Wizard now**, and click **Close**.
![](https://main.qcloudimg.com/raw/3fa47faa1f8bed1a8ec478260ee64481.png)

### Step 5: configuring SharePoint 2016

1. In the **SharePoint Products Configuration Wizard** window, click **Next**.
![](https://main.qcloudimg.com/raw/3e8d015ab34ab8de8172838dd21d31ac.png)
2. Click **Yes** in the pop-up dialog box to allow service restart during the configuration.
3. Select **Create a new server farm**, and click **Next**.
![](https://main.qcloudimg.com/raw/f87545fb79d747bf64c38131fbb318d4.png)
4. On the **Specify Configuration Database Settings** page, set the configuration database and the access account.
The SharePoint database is on the local host, so you need to enter the local database and account. Then, click **Next**.
![](https://main.qcloudimg.com/raw/cf9723c7885399e0e5004f1ecee4ea2d.png)
5. Enter the password of the server farm and click **Next**.
6. Select **Front-end** for “Multiple-Server Farm” and click **Next**.
![](https://main.qcloudimg.com/raw/95da6977363606dd62835d12bc9b7ae2.png)
7. Specify the port number of SharePoint Central Administration Web Application (this example uses “10000” but you can configure the number as needed), and click **Next**.
![](https://main.qcloudimg.com/raw/26ef65e1e8e229e9c67c2eafc40c0d32.png)
8. Confirm the SharePoint configurations, and click **Next**.
![](https://main.qcloudimg.com/raw/a0e8ee05fcc2fc4b6f717bb0e03287af.png)
9. After the configuration is complete, click **Finish**.

