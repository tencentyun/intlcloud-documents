## Overview
This document describes how to use IIS to build an FTP site on a Windows Lighthouse instance.

## Software
The following software programs are used to build the FTP service:
 - Windows OS: This document uses the Windows Server 2012 system image as an example.
 - IIS: Web server. This document uses IIS 8.5 as an example.

## Directions
### Step 1. Log in to the Lighthouse instance
You can log in to the Windows instance via [VNC](https://intl.cloud.tencent.com/document/product/1103/46399) or [remote desktop connection](https://intl.cloud.tencent.com/document/product/1103/46400).

### Step 2. Install the FTP service on IIS
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-3px 0px"> to open the server manager.
2. In the **Server Manager** window, click **Add roles and features**.
![](https://qcloudimg.tencent-cloud.cn/raw/a37eb121a7accec2917eeef14c23f671.png)
3. In the **Add Roles and Features Wizard** pop-up window, click **Next** to enter the **Installation Type** page.
4. Select **Role-based or feature-based installation** and click **Next**.
5. On the **Select destination server** page, keep the default configurations and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/89aa3902db2d1368cd9cf2da668b646c.png)
6. On the **Select server roles** page, select **Web Server (IIS)** and click **Add Feature** in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/aaa90e51922b1ab22a5c10fa339c7e74.png)
7. Click **Next** for the next three pages to enter the **Select role services** page.
8. On the **Select role services** page, select **FTP Service** and **FTP Extensibility** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/a8adc8975f4c8e656f5c70ced26b9190.png)
9. Click **Install**.
10. After the installation is completed, click **Close**.

### Step 3. Set up the FTP username and password[](id:user)

<dx-alert infotype="explain" title="">
Follow the steps below to configure your FTP username and password. If you plan to use anonymous access only, skip this section.
</dx-alert>

1. In the **Server Manager** window, select **Tools** > **Computer Management** on the top-right navigation bar to open the **Computer Management** window.
2. On the **Computer Management** page, select **System Tools** > **Local Users and Groups** > **Users** on the left sidebar.
3. In the right of the **Users** page, right-click the blank space and select **New User**.
![](https://qcloudimg.tencent-cloud.cn/raw/ae99d281d2a84691779feafe2df8c141.png)
4. On the **New User** page, configure the username and password as prompted and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/d8bb177cbe77fca93526153d8b256684.png)
Set the main parameters as follows:
  - **Username**: Custom. This document uses `ftpuser` as an example.
  - **Password** and **Confirm Password**: Set a custom password that meets the following requirements:
    - Cannot contain the username or more than two consecutive characters of the username.
    - Must contain at least six characters.
    - Must contain characters in at least three of the four character types: `[A - Z]`, `[a - z]`, `[0 - 9]`, and special symbols (such as `!$#%`). 
  - Deselect **User must change password at next logon** and select **Password never expires**.
    Select options based on your actual needs. This document uses **Password never expires** as an example.
5. Click **Close**. You can see the created `ftpuser` in the list.
	
### Step 4. Set the shared folder permission

<dx-alert infotype="explain" title="">
This document uses the `C:\test` folder as the shared folder of the FTP site. The folder contains the `test.txt` file you want to share with others. Create the `C:\test` folder and the `test.txt` file under it as instructed. You can also use any other folder as needed.
</dx-alert>

1. On the desktop, click <img src="https://main.qcloudimg.com/raw/863967bab67b6cd83ce5f0924e1b19c8.png" style="margin:-3px 0px"> to open the **This PC** window.
2. Select and right-click the `test` folder under the C drive. Select **Properties**.
3. In the **test Properties** window, select the **Security** tab.
4. Select `Everyone` and click **Edit**.
If **Group or user names** does not contain `Everyone`, see [Adding `Everyone` user](#add) to add the user.
![](https://qcloudimg.tencent-cloud.cn/raw/b68570f496b1ded1215e0aa30b064424.png)
5. [](id:step5)On the **Permissions for test** page, set the permission for `Everyone` and click **OK**.
This document uses granting `Everyone` all permissions as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/9b4acbebba138e39c6f572d21f5d17bd.png)
6. Click **OK** to complete the configuration.


### Step 5. Add an FTP site
1. In the **Server Manager** window, select **Tools** > **Internet Information Services (IIS) Manager** on the top-right navigation bar.
2. In the **Internet Information Services (IIS) Manager** pop-up window, expand your server in the left sidebar, right-click **Sites**, and select **Add FTP Site**.
![](https://qcloudimg.tencent-cloud.cn/raw/37c37446d72ad332aed4f3fb7f729ded.png)
3. On the **Site Information** page, enter the following information and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/66623044cec7b4b318a7704601be708d.png)
    - **FTP site name**: Name of your FTP site. This document uses `ftp` as an example.
    - **Physical path**: Path of the shared folder with permissions configured. This document uses `C:\test` as an example.
4. On the **Binding and SSL Settings** page, enter the following information and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/02682dc26ba3fdd74904e59baa498e97.png) 
   Configure the main parameters as follows:
     - **Binding**: The **IP Address** defaults to **All Unassigned**. The default FTP port number is 21. You can set a custom port number.
     - **SSL**: Select an option. In this document, **No SSL** is selected.
       -  **No SSL**: No SSL is used.
       - **Allow SSL**: Allow the FTP server to connect with clients with or without SSL.
      - **Require SSL**: SSL encryption is required for communication between the FTP server and clients.
   If you select **Allow SSL** or **Require SSL**, you can select an existing SSL certificate in **SSL Certificates** or [create an SSL certificate](#ssl).
5. On the **Authentication and Authorization Information** page, enter the following information and click **Next** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3187833727a8a8e58f589ddb00c789f1.png)
 - **Authentication**: Select an identity verification method. This document uses **Basic** as an example.
    - **Anonymous**: Allow users that provide the anonymous or FTP username to access the content.
	 - **Basic**: Require users to provide valid user names and passwords to access the content. Under this mode, passwords are transmitted without encryption. Therefore, select this authentication mode only when you know that the connection between the clients and the FTP server is secure (for example, by using SSL).
 - **Authorization**: Select one of the following options from the **Allow access to** drop-down list. This document uses the specified `ftpuser` user as an example.
	    - **All users**: All users, anonymous or identified, can access the content.
	        - **Anonymous users**: Anonymous users can access the content.
	        - **Specified role or user group**: Only the specified roles or members of the specified groups can access the content. If you choose this option, you need to specify the roles or user groups.
	        - **Specified users**: Only the specified user can access the content. If you choose this option, you need to specify the username.
 - **Permissions**: Set permissions as needed. This document selects both **Read** and **Write** permissions.
    - **Read**: Allow the authorized user to read the shared content.
    - **Write**: Allow the authorized user to write into the directory.
7. Click **Finish** to successfully create the FTP site.

### Step 6. Configure the security group and firewall
1. After the FTP site is created, add an inbound rule that allows traffic to the FTP port based on the FTP access mode:
 - **Active mode**: Open ports 20 and 21.
 - **Passive mode**: Open the ports 21 and 1024–65535.
For more information on how to open ports, see [Adding firewall rule](https://intl.cloud.tencent.com/document/product/1103/41393#.E6.B7.BB.E5.8A.A0.E9.98.B2.E7.81.AB.E5.A2.99.E8.A7.84.E5.88.99).
2. (Optional) See Microsoft documentation to configure firewall for the FTP site, so that the FTP server can accept passive connections from the firewall.

### Step 7. Test the FTP site
You can use tools such as the FTP client software, browser, or file manager to verify the FTP server. This document uses the file manager of the client as an example.
1. Configure Internet Explorer as needed:
 - Firewall has been configured (active mode):
 Open Internet Explorer on the **Client**, select **Tools** > **Internet Options** > **Advanced**, deselect **Use Passive FTP (for firewall and DSL model compatibility)**, and click **OK**.
 - Firewall has not been configured (passive mode):
    1. Open Internet Explorer on the **FTP Server**, select **Tools** > **Internet Options** > **Advanced**, deselect **Use Passive FTP (for firewall and DSL model compatibility)**, and click **OK**.
    2. Open Internet Explorer on the **Client**, select **Tools** > **Internet Options** > **Advanced**, select **Use Passive FTP (for firewall and DSL model compatibility)**, and click **OK**.
2. Open the computer where the client is installed and enter the following path in the search box:
```
ftp://Lighthouse instance public IP:21
```
![](https://qcloudimg.tencent-cloud.cn/raw/82387088e689998764a2dc6b78d13543.png)
3. In the pop-up window, enter the username and password configured in [creating the FTP username and password](#user).
4. You can upload and download files after a successful login.

## Appendix
### Adding `Everyone` user[](id:add)
1. In the **test Properties** window, select the **Security** tab and click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/2076b58ac4165f6e7c1058a87fdcfa6d.png)
2. On the **Permissions for test** page, click **Add**.
3. On the **Select Users or Groups** page, click **Advanced**.
4. In the pop-up window, click **Find Now**.
5. Select `Everyone` under **Search results** and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/50183d05372803e1320117aa8e4b34a4.png)
6. On the **Select Users or Groups** page, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/6900461836c0bcdc54b117d24db9f776.png)
Proceed to [step 5](#step5) to configure the permission for `Everyone`.

### Creating instance certificate[](id:ssl)
1. In the **Server Manager** window, select **Tools** > **Internet Information Services (IIS) Manager** on the top-right navigation bar.
2. In the **Internet Information Services (IIS) Manager** pop-up window, select the server on the left sidebar and double-click **Server Certificates** on the right panel.
![](https://qcloudimg.tencent-cloud.cn/raw/f760f6708ffea380bee28935ca05cdff.png)
3. Select **Create Self-Signed Certificate** in the right operation column.
4. In the **Create Self-Signed Certificate** pop-up window, enter the certificate name and storage type.
This document uses creating an SSL certificate for personal storage as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/71236a423b7a4039c368167a8a4b37b0.png)
5. Click **OK**.
