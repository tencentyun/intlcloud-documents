## Introduction
This describes how to use IIS to build an FTP site on a Tencent Cloud Virtual Machine (CVM) instance that runs Windows.

## Software Requirements
The following software are needed for building the FTP service:
 - OS: Windows Server 2012 
 - Web server: IIS 8.5

## Directions
### Step 1: log in to the CVM
- [Log in to a CVM on Windows Using an RDP File (Recommended)](http://intl.cloud.tencent.com/document/product/213/5435).
- [Log in to a Windows CVM Using a Remote Desktop](https://intl.cloud.tencent.com/document/product/213/32498).

### Step 2: install the FTP service on IIS
1. Click <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-3px 0px"> to open the server manager. The **Server Manager** windows appears.
2. Click **Add Roles and Features**, as shown in the figure below. The **Guide to Adding Roles and Features** window appears.
![](https://main.qcloudimg.com/raw/1d941b3c877a420513e494971a834f37.png)
3. Click **Next**. The **Choose Installation Type** page appears.
4. Select **Role-based or Feature-based Installation**, and click **Next**. The **Choose Target Server** page appears.
5. Keep the default settings, and click **Next**, as shown in the figure below. The **Choose Server Role** page appears.
![](https://main.qcloudimg.com/raw/41f775ccbcd8e984b72bc096efa668d4.png)
6. Select **Web Server (IIS)**, and click **Add Feature** in the displayed window, as shown in the figure below:
![](https://main.qcloudimg.com/raw/f23fe1b8415c0f75c54309b652781aa4.png)
7. Click **Next** three times. The **Choose Role Service** page appears.
8. Select **FTP Service** and **FTP Extension**, and click **Next**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1fa84c69d96c16f2ea0f10e51b0607bb.png)
9. Click **Install** to start installing the FTP service.
10. After installation is completed, click **Close**.
<span id="user"></span>
### Step 3: create an FTP username and password
> The following steps create an FTP account with password authentication. If you plan to use anonymous access only, skip this section.
>
1. In the “Server Manager” window, select **Tools** -> **My Computer** in the navigation bar in the upper right corner. The **My Computer** window appears.
2. Select **System Tools** -> **Local Users and Groups** -> **Users** in the sidebar to the left.
3. On the right side of the **Users** interface, right-click an empty spot, and select **New User**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/60bad9ff725b8fe4386c2eed9c5ff63a.png)
4. On the “New User” interface, set the user name and password according to the following instructions. Click **Create**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1bc9cb2c2000361f6699c155e25d7630.png)
The main parameters are as follows:
  - User name: name of the user. In this case, `ftpuser`.
  - Password and Confirm password: the password must contain uppercase and lowercase letters and numbers. In this case, `tf7295TFY`.
  - Clear **User must change password in next login**, and select **Password never expires**.
  Select options as you see fit. For this article, we select **Password never expires**.
5. Click **Close** to close the “New User” window. You can see the newly created user `ftpuser` in the list.
	
### Step 4: set shared folder permissions
> In this article, we use `C:\test` as the shared folder. It contains a file called `test.txt`. Create a folder called `test` under `C:\` and a file called `test.txt` under `C:\test`. You can also use any other folder and file.
>
1. Click <img src="https://main.qcloudimg.com/raw/863967bab67b6cd83ce5f0924e1b19c8.png" style="margin:-3px 0px"> to open **This Computer**.
2. Expand the directories under C drive. Select and right-click `test`. Select **Properties**.
3. In the **Properties** window, select **Security** tab.
4. Select `Everyone` and click **Edit**, as shown in the figure below:
If “Group or User Name” does not contain `Everyone`, refer to [Adding Everyone](#add) to add the user.
![](https://main.qcloudimg.com/raw/aec3d0557deef26ca3ff8005da86603f.png)
5. <span id="step5"></span>On the **Permissions** interface, set the permissions for `Everyone` and click **OK**, as shown in the figure below:
In this article, we grant `Everyone` all permissions.
![](https://main.qcloudimg.com/raw/ccdfda072d8a476a08773b7fcf979ec7.png)
6. In the **Properties** window, click **OK** to complete the settings.


### Step 5: add an FTP site
1. In the “Server Manager” window, select **Tools** -> **Internet Information Services (IIS) Manager** in the navigation bar in the upper right corner.
2. In the **Internet Information Services (IIS) Manager** window, expand your server in the left sidebar, right-click **Website**, and select **Add FTP Site**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/3d2c1a2708939cd5a8d7bf3bdf9aa1ff.png)
3. On the “Site Information” interface, enter the following information. Click **Next**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/76761e667657b80bfdd2d2403d64ba3c.png)
    - **FTP site name**: name of your FTP site. In this article, `ftp` is used.
    - **Physical path**: path of the shared folder. Make sure you set the appropriate permissions. In this article, `C:\test` is used.
4. On the **Binding and SSL Settings** interface, enter the following information. Click **Next**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/355c3de0e19d7e1c161c51156bf0965f.png) 
The following is a list of parameters:
     - **Binding**: the default option for IP addresses is **None assigned**; and the default port is port 21, the default FTP port number. You can choose your own port number.
     - **SSL**: select an option. In this article, **No SSL** is selected.
       - **No SSL**: does not support SSL connections.
       - **Allow SSL**: allow the FTP server to connect with clients with or without SSL.
      -  **Require SSL**: SSL encryption is required for communication between the FTP server and clients.
   If you choose **Allow SSL** or **Require SSL**, you can select an existing SSL certificate in “SSL Certificates”, or refer to [creating a server certificate](#ssl) to create an SSL certificate.
5. On the “Identity Authentication and Authorization Information” interface, enter the following information. Click **Next**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/0f3be2c7ba449240cdac3f3c767e668c.png)
 - **Identity authentication**: select an identity authentication method. In this article, **Basic** is used.
    - *Anonymous**: allow users access to the content without authentication.
	 -. **Basic**: require users to provide valid user names and passwords before allowing them to access the content. Under this mode, passwords are transferred without encryption. Therefore, select this authentication mode only when you know that the connection between the clients and FTP server is secure (for example, by using SSL).
 - **Authorize**: choose an option from the access permission drop-down list. In this article, `ftpuser` is used.
	    - **All users**: all users, anonymous or identified, can access the content.
	    - **Anonymous users**: anonymous users can access the content.
	    - **Specified role or user group**: only the specified roles or members of the specified groups can access the content. If you choose this option, you need to specify the roles or user groups.
	    - **Specified user**: only the specified user can access the content. If you choose this option, you need to specify the username.
 - **Permissions**: permissions to the shared content. In this article, **Read** and **Write** are selected.
    - **Read**: allow authorized users to read shared content.
    - **Write**: allow authorized users to write into the directory.
7. Click **Complete**.

### Step 6: configure security group and firewall
1. After the FTP site is created, add an inbound rule that allows traffic to the FTP port, which is 21 for the purpose of this article. For more information, refer to [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
If you selected other ports, you also need to add one inbound rule for each port selected.
2. (Optional) Refer to [Microsoft official documentation](https://docs.microsoft.com/en-us/previous-versions/orphan-topics/ws.11/hh831655(v=ws.11)) on how to configure firewall so that the FTP server is able to accept passive connections from the firewall.

### Step 7: test the FTP site
You can use an FTP client, browser, or the file manager to connect to the FTP server. For the purpose this article, the file manager is used.
1. Configure Internet Explorer
 - If you have added the appropriate firewall rules, open an Internet Explorer window and select **Tools** -> **Internet Options** -> **Advanced**. Clear **Use Passive FTP (used for compatibility between the firewall and DSL modem)** and click **OK**.
 - If you did not add the appropriate firewall rules:
    1. Open an Internet Explorer window on **the FTP server** and select **Tools** -> **Internet Options** -> **Advanced**.  Clear **Use Passive FTP (used for compatibility between the firewall and DSL modem)** and click **OK**.
    2. Open an Internet Explorer window on the **client** and select **Tools** -> **Internet Options** -> **Advanced**. Clear **Use Passive FTP (used for compatibility between the firewall and DSL modem)** and click **OK**.
2. Open the file manager on your PC and type the following address in the address box of the browser and press **Enter**, as shown in the following figure.
```
ftp://CVM_public_IP_address:21
```
![](https://main.qcloudimg.com/raw/d3d5a93170bb990f47ecd9f24c3e89ab.png)
3. The **Login identity** dialog box appears. Enter the user name and password configured in [Creating FTP user name and password](#user).
In this article, the username is `ftpuser`, and the password is `tf7295TFY`.
4. Upload and download files after login.

## Appendix
<span id="add"></span>
### Adding Everyone
1. In the **Properties** window, select the **Security** tab. Click **Edit**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/f3f056e833fc63c97f23eef646ea8a10.png)
2. On the **Properties** dialog box, click **Add**.
3. On the “Choose User or Group” dialog box, click **Advanced**.
4. On the displayed “Choose User or Group” dialog box, click **Search Now**.
5. In the search result, select `Everyone` and click **OK**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/32a9d44822ed4db0e82167d0cfb94835.png)
6. On the “Choose User or Group” dialog box, click **OK**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1245acedba4be051cf234423460a4345.png)
Go to [Step 5](#step5) to set the permissions of user `Everyone`.
<span id="ssl"></span>
### Creating a server certificate
1. Open “Server Manager” and select **Tools** -> **Internet Information Services (IIS) Manager** in the navigation bar in the upper right corner.
2. The **Internet Information Services (IIS) Manager** window appears. Select the server in the left sidebar and double-click **Server Certificates** on the right interface, as shown in the figure below:
![](https://main.qcloudimg.com/raw/8fc9f67a26475b891f4c50d9c670c08c.png)
3. Select **Create Self-Signature Certificate** in the right operation column.
4. The **Create Self-Signature Certificate** window appears, enter a certificate name and the storage class, as shown in the figure below:
In this document, an SSL certificate for personal storage is created.
![](https://main.qcloudimg.com/raw/0db81917b5b1e20af19d4d687d0d7fda.png)
5. Click **OK**.
