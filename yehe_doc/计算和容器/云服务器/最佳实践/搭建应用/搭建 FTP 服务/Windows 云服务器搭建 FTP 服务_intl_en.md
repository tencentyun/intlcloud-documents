## Overview
This document describes how to use IIS to build an FTP site on a Windows CVM instance.

## Software
This document uses the following software versions as an example to build the FTP service.
 - Operating system: Windows. This document uses Windows Server 2012 as an example.
 - Web server: IIS. This document uses IIS 8.5 as an example.

## Directions
### Step 1. Log in to the Windows CVM
[Log in to Windows instance using RDP (recommended)](https://intl.cloud.tencent.com/document/product/213/5435).
You can also use other login methods that you are more comfortable with: [log in to a Windows CVM instance using a remote desktop](https://intl.cloud.tencent.com/document/product/213/32498).

### Step 2. Install the FTP service on IIS
1 On the desktop, click <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-3px 0px"> to open the server manager. The **Server Manager** window will appear.
2. Click **Add roles and features**.
![](https://main.qcloudimg.com/raw/1d941b3c877a420513e494971a834f37.png)
3. In the **Add Roles and Features Wizard** pop-up window, click **Next** to access the **Installation Type** page.
4. Select **Role-based or feature-based installation** and click **Next**.
5. On the **Select destination server** page, keep the default configurations and click **Next**.
![](https://main.qcloudimg.com/raw/41f775ccbcd8e984b72bc096efa668d4.png)
6. On the **Select server roles** page, check **Web Server (IIS)** and click **Add Feature** in the window that pops up.
![](https://main.qcloudimg.com/raw/f23fe1b8415c0f75c54309b652781aa4.png)
7. Click **Next** 3 times to access the **Select role services** page.
8. Check **FTP Service** and **FTP Extensibility**, and click **Next**.
![](https://main.qcloudimg.com/raw/1fa84c69d96c16f2ea0f10e51b0607bb.png)
9. Click **Install** to start installing the FTP service.
10. After the installation is completed, click **Close**.

<span id="user"></span>

### Step 3. Create an FTP username and password

>?The following steps create an FTP account with password authentication. If you plan to use anonymous access only, skip this section.
>
1. In the “Server Manager” window, select **Tools** > **Computer Management** in the top-right navigation bar to open the “Computer Management” window.
2. Select **System Tools** > **Local Users and Groups** > **Users** on the left sidebar.
3. On the right panel of the **Users** interface, right-click the blank space and select **New User**, as shown below:
![](https://main.qcloudimg.com/raw/60bad9ff725b8fe4386c2eed9c5ff63a.png)
4. On the **New User** page, configure the username and password according to the following instructions. Click **Create**.
![](https://main.qcloudimg.com/raw/1bc9cb2c2000361f6699c155e25d7630.png)
Set the main parameters as follows:
  - User name: custom. This document uses `ftpuser` as an example.
  - Password and Confirm password: custom. The password must contain uppercase and lowercase letters and digits. This document uses `tf7295TFY` as an example.
  - Clear **User must change password at next logon**, and check **Password never expires**.
    Select options based on your actual needs. This document uses **Password never expires** as an example.
5. Click **Close**. You can see the newly created user `ftpuser` in the list.
	
### Step 4. Set the shared folder permission
>? This document uses the `C:\test` folder as the shared folder of the FTP site. It contains the `test.txt` file you want to share with others. Create the `C:\test` folder and the `test.txt` file under it as instructed. You can also use any other folder as needed.
>
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/863967bab67b6cd83ce5f0924e1b19c8.png" style="margin:-3px 0px"> to open the **This PC** window.
2. Select and right-click the `test` folder under the C drive. Select **Properties**.
3. In the **test Properties** window, select the **Security** tab.
4. Select `Everyone` and click **Edit**.
If “Group or user names” does not contain `Everyone`, refer to [Adding Everyone](#add) to add the user.
![](https://main.qcloudimg.com/raw/aec3d0557deef26ca3ff8005da86603f.png)
5. <span id="step5"></span>On the “Permissions for test” page, set the permission for `Everyone` and click **OK**.
This document uses granting `Everyone` all permissions as an example.
![](https://main.qcloudimg.com/raw/ccdfda072d8a476a08773b7fcf979ec7.png)
6. Click **OK** to complete the configuration.


### Step 5. Add an FTP site
1. In the **Server Manager** window, select **Tools** > **Internet Information Services (IIS) Manager** in the top-right navigation bar.
2. In the **Internet Information Services (IIS) Manager** pop-up window, expand your server in the left sidebar, right-click **Sites**, and select **Add FTP Site**, as shown below:
![](https://main.qcloudimg.com/raw/3d2c1a2708939cd5a8d7bf3bdf9aa1ff.png)
3. On the **Site Information** page, enter the following information and click **Next**.
![](https://main.qcloudimg.com/raw/76761e667657b80bfdd2d2403d64ba3c.png)
    - **FTP site name**: name of your FTP site. This document uses `ftp` as an example.
    - **Physical path**: path of the shared folder with the permission configured. This document uses `C:\test` as an example.
4. On the **Binding and SSL Settings** page, enter the following information and click **Next**.
![](https://main.qcloudimg.com/raw/355c3de0e19d7e1c161c51156bf0965f.png)  
Configure the main parameters as follows:
     - **Binding**: the **IP Address** defaults to **All Unassigned**. The default FTP port number is 21. You can set a custom port number.
     - **SSL**: select an option. In this document, **No SSL** is selected.
       -  **No SSL**: no SSL is used.
       - **Allow SSL**: allow the FTP server to connect with clients with or without SSL.
      - **Require SSL**: SSL encryption is required for communication between the FTP server and clients.
   If you choose **Allow SSL** or **Require SSL**, you can select an existing SSL certificate in “SSL Certificates”, or [create an SSL certificate](#ssl).
5. On the **Authentication and Authorization Information** page, enter the following information and click **Next**.
![](https://main.qcloudimg.com/raw/0f3be2c7ba449240cdac3f3c767e668c.png)
 - **Authentication**: select an identity verification method. This document uses **Basic** as an example.
    - **Anonymous**: allow users that provide the anonymous or FTP username to access the content.
	 - **Basic**: require users to provide valid user names and passwords to access the content. Under this mode, passwords are transmitted without encryption. Therefore, select this authentication mode only when you know that the connection between the clients and the FTP server is secure (for example, by using SSL).
 - **Authorization**: select one of the following options from the **Allow access to** drop-down list. This document uses the specified `ftpuser` user as an example.
	    - **All users**: all users, anonymous or identified, can access the content.
	        - **Anonymous users**: anonymous users can access the content.
	        - **Specified role or user group**: only the specified roles or members of the specified groups can access the content. If you choose this option, you need to specify the roles or user groups.
	        - **Specified users**: only the specified user can access the content. If you choose this option, you need to specify the username.
 - **Permissions**: configure the permissions for the authorized users. This document takes setting the **Read** and **Write** permissions as an example.
    - **Read**: allow the authorized user to read the shared content.
    - **Write**: allow the authorized user to write into the directory.
6. Click **Finish** to successfully create the FTP site.

### Step 6. Configure the security group and firewall
1. After the FTP site is created, add an inbound rule that allows traffic to the FTP port based on the FTP access mode:
 - **Active mode**: open the ports 20 and 21.
 - **Passive mode**: open the ports 21 and 1024-65535 (for example, open the ports 5000-6000).
For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
2. (Optional) Refer to [Microsoft documentation](https://docs.microsoft.com/en-us/previous-versions/orphan-topics/ws.11/hh831655(v=ws.11)) on how to configure the firewall so that the FTP server is able to accept passive connections from the firewall.

### Step 7. Test the FTP site
You can use tools such as the FTP client software, browser, or file manager to verify the FTP server. This document uses the file manager of the client as an example.
1. Configure Internet Explorer as needed:
 - Firewall configured (active mode):
 Open an Internet Explorer window on the **Client** side and select **Tools** > **Internet Options** > **Advanced**. Uncheck **Use Passive FTP for the firewall and the DSL modem compatibility** and click **OK**.
 - Firewall has not been configured (passive mode):
    1. Open an Internet Explorer window on the **FTP server** side and select **Tools** > **Internet Options** > **Advanced**. Uncheck **Use Passive FTP for the firewall and the DSL modem compatibility** and click **OK**.
    2. Open an Internet Explorer window on the **Client** side and select **Tools** > **Internet Options** > **Advanced**. Check **Use Passive FTP for the firewall and the DSL modem compatibility** and click **OK**.
2. Open the PC where the client is installed, type the following address in the address box of the browser, and press **Enter**.
```
ftp://CVM public IP address:21
```
![](https://main.qcloudimg.com/raw/d3d5a93170bb990f47ecd9f24c3e89ab.png)
3. In the pop-up window, enter the username and password configured in [creating the FTP username and password](#user).
In this document, the username is `ftpuser`, and the password is `tf7295TFY`.
4. You can upload and download files after a successful login.

## Appendix
<span id="add"></span>

### Adding Everyone

1. In the **test Properties** window, select the **Security** tab and click **Edit**.
![](https://main.qcloudimg.com/raw/f3f056e833fc63c97f23eef646ea8a10.png)
2. On the **Permissions for test** page, click **Add**.
3. On the **Select Users or Groups** dialog box, click **Advanced**.
4. In the pop-up window, click **Find Now**.
5. Select `Everyone` under **Search results** and click **OK**.
![](https://main.qcloudimg.com/raw/32a9d44822ed4db0e82167d0cfb94835.png)
6. On the **Select Users or Groups** dialog box, click **OK**.
![](https://main.qcloudimg.com/raw/1245acedba4be051cf234423460a4345.png)
Go to [Step 5](#step5) to configure the permission for `Everyone`.

<span id="ssl"></span>

### Creating a server certificate

1. In the **Server Manager** window, select **Tools** > **Internet Information Services (IIS) Manager** in the top-right navigation bar.
2. In the **Internet Information Services (IIS) Manager** pop-up window, select the server in the left sidebar and double-click **Server Certificates** on the right panel.
![](https://main.qcloudimg.com/raw/8fc9f67a26475b891f4c50d9c670c08c.png)
3. Select **Create Self-Signed Certificate** in the right operation column.
4. In the **Create Self-Signed Certificate** pop-up window, enter a certificate name and the storage type.
This document uses creating an SSL certificate for personal storage as an example.
![](https://main.qcloudimg.com/raw/0db81917b5b1e20af19d4d687d0d7fda.png)
5. Click **OK**.
