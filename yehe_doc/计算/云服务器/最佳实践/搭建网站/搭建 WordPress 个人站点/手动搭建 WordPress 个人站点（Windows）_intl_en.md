## Overview
WordPress is a blog platform written in PHP. This article describes how to install WordPress on Windows Server 2012.

<dx-alert infotype="notice" title="">
It's recommended that you can configure a personal blog by using a Tencent Cloud marketplace image. It may take a long time to set up the Discuz! forum manually.
</dx-alert>



## Software
Although PHP version 5.6.20 and later and MySQL version 5.0 and later support WordPress, we recommend using PHP 7.3 and MySQL 5.6 or later versions for security reasons.

The following software is involved in building WordPress:
- Windows: this document uses Windows Server 2012 R2 Datacenter 64-bit as an example.
- Web server: IIS. This document uses IIS 8.5 as an example.
- MySQL 8.0.19 is used for database.
- PHP is a scripting language. This article uses PHP 7.1.30.
- WordPress is a blog platform. We use WordPress 5.9 in this article.


## Directions

### Step 1. Log in to the CVM
[Log in to the Windows instance using RDP (recommended)](https://intl.cloud.tencent.com/zh/document/product/213/5435).
You can also use other login methods that you are more comfortable with: [log in to a Windows CVM instance using a remote desktop](https://intl.cloud.tencent.com/document/product/213/32498).

### Step 2. Setting up WIMP
See [Manually Building a WIPM Environment](https://intl.cloud.tencent.com/zh/document/product/213/33143).
1. Install IIS.
2. Deploy PHP 5.6.20 and later versions.
3. Install MySQL 5.6 and later versions.

### Step 3. Installing and configuring WordPress

<dx-alert infotype="explain" title="">
You can download the latest WordPress version from the official WordPress website.
</dx-alert>



1. Download WordPress and decompress it into a directory on the CVM.
For example, you can decompress it into `C:\wordpress`.
2. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"> >  <img src="https://main.qcloudimg.com/raw/ca83b4e70e201fe9ff98dc1f2b207cee.png" style="margin: -3px 0px;"> >  **MySQL 5.6 Command Line Client** to open the MySQL command line client.
3. Run the following commands on the MySQL command line client to create a database for WordPress.
For example, create a database named `wordpress`.
```
create database wordpress;
```
4. Find `wp-config-sample.php` under `C:\wordpress` and rename it to `wp-config.php`.
5. Open the `wp-config.php` file with a text editor, and modify the relevant configuration information according to [Step 3: Installing and configuring WordPress](https://intl.cloud.tencent.com/document/product/213/10190) as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5900f1b371a512f7c058783caeccc719.png)
6. Save `wp-config.php`.
7. Click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: -3px 0px;"> to open **Server Manager**.
8. On the left sidebar, select **IIS**. Click the name of the server in the **Server** column to the right. Select **Internet Information Services (IIS) Manager**. The **Internet Information Services (IIS) Manager** window appears.
9. In the **Internet Information Service (IIS) Manager** window, expand your server on the left sidebar and click your **website**. The website management page appears, as shown below:
10. Delete **websites** bound to port 80.
You can change the port to another unused port, such as 8080.
11. In the **Actions** column on the right, click **Add Website**.
12. In the pop-up window, enter the following information and click **OK**.
    - **Website name**: name of the website, such as `wordpress`.
    - **Application pool**: select **DefaultAppPool**.
    - **Physical path**: the directory that contains WordPress, such as `C:\wordpress`.
13. Find `php.ini` under the directory that contains PHP. Open it with a text editor and make the following changes:
    1. Changes are different for different PHP versions.
       - For PHP 5.x, find `extension=php_mysql.dll` and delete the `;` at the beginning.
       - For PHP 7.x, find `extension=php_mysqli.dll` or `extension=mysqli` and delete the `;` at the beginning.
    2. Find `extension_dir= "ext"` and delete the `;` at the beginning.
14. Save the `php.ini` file.

### Step 4. Verifying the WordPress Configuration

1. Open a browser window on your local machine and visit `http://localhost/wp-admin/install.php`. The WordPress installation page appears.
2. Enter the installation information as described in the following table based on the WordPress installation wizard and click **Install WordPress**.
<table>
	<tr><th width="16%">Required Information</th><th>Description</th></tr>
	<tr><td>Website Name</td><td>Name of the WordPress site.</td></tr>
	<tr><td>Username</td><td>Account name of the WordPress administrator. For security reasons, use a name other than `admin`.</td></tr>
	<tr><td>Password</td><td>Use a strong password, different than your current password. Store it in a secure location.</td></tr>
	<tr><td>Email</td><td>Email address used to receive notifications</td></tr>
</table>
Now, you can log in to your WordPress website and post blogs.

## FAQs
If you encounter a problem when using CVM, refer to the following documents for troubleshooting:
- CVM login: [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- CVM network: [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- CVM disks: [System and Data Disks](https://intl.cloud.tencent.com/zh/document/product/213/17351).

