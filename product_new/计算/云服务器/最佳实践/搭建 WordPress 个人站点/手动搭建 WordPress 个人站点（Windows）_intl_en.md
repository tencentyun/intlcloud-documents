## Introduction
WordPress is a blog platform written in PHP. This article describes how to install WordPress on Windows Server 2012.
 
## Software
Although PHP version 5.6.20 and later and MySQL version 5.0 and later support WordPress, we recommend using PHP 7.3 and MySQL 5.6 or later versions for security reasons.

These are the software involved:
- Windows operating system. We use Windows Server 2012 in this article.
- IIS is a web server. We use ISS 8.5 in this article.
- MySQL is a database software. We use MySQL 5.6.46 in this article.
- PHP is a scripting language. We use PHP 7.3.12 in this article.
- WordPress is a blog platform. We use WordPress 5.3 in this article.


## Directions

### Step 1: Logging in to Windows CVM
- [Log in to a Windows CVM Using an RDP File (Recommended)](http://intl.cloud.tencent.com/document/product/213/5435)
- [Log in to a Windows CVM Using a Remote Desktop](https://intl.cloud.tencent.com/document/product/213/32498)

### Step 2: Setting up WIMP
Refer to [Manually Building a WIPM Environment](https://intl.cloud.tencent.com/document/product/213/2755) for instructions on how to:
1. Install IIS.
2. Deploy PHP 5.6.20 and later versions.
3. Install MySQL 5.6 and later versions.

### Step 3: Installing and configuring WordPress
> You can download the latest version of WordPress from the official WordPress website.
>

1. Download WordPress and decompress it into a directory on the CVM.
For example, you can decompress it into `C:\wordpress`.
2. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;">. Input **cmd** in **Run** and press **Enter** to open a command line window.
3. Run the following commands in the command line window to create a database for WordPress.
For example, create a database named `wordpress`.
```
create database wordpress;
```
4. Find `wp-config-sample.php` under `C:\wordpress` and rename it to `wp-config.php`.
5. Use a text editor to open `wp-config.php` and edit the configuration information as detailed in [Step 4: Installing MySQL](#Step04).
6. Save `wp-config.php`.
7. Click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**.
8. In the navigation panel to the left, select **IIS**. Click the name of the server in the **Server** column to the right. Select **Internet Information Services (IIS) Manager**. The **Internet Information Services (IIS) Manager** window appears.
9. In the **Internet Information Service (IIS) Manager** window, expand your server in the left navigation panel and click your website. The website management page appears.
10. Delete websites bound to port 80.
You can change the port to another unused port, such as 8080.
11. Click **Add Website**.
12. Input necessary information as shown below and click **OK**.

 - Website name: name of the website, such as `wordpress`.
 - Application pool: select **DefaultAppPool**.
 - Physical path: the directory that contains WordPress, such as `C:\wordpress`.
13. Find `php.ini` under the directory that contains PHP. Open it with a text editor and make the following changes:
 1. Changes are different for different PHP versions.
     - For PHP 5.x, find `extension=php_mysql.dll` and delete the `;` at the beginning.
     - For PHP 7.x, find `extension=php_mysqli.dll` and delete the `;` at the beginning.
 2. Find `extension_dir= “ext”` and delete the `;` at the beginning.
14 Save `php.ini`.

### Step 4: Verifying the WordPress Configuration

1. Open a browser window on your local machine and visit `http://localhost/wp-admin/install.php`. The WordPress installation page appears.
2. Input information as the installation wizard guides you through the process. Click **Install WordPress** to complete the process.
<table>
	<tr><th>Information </th><th>Description</th></tr>
	<tr><td>Website Name</td><td>Name of the WordPress site.</td></tr>
	<tr><td>Username</td><td>Account name of the WordPress administrator. For security reasons, use a name other than `admin`.</td></tr>
	<tr><td>Password</td><td>Use a strong password, different than your current password. Store it in a secure location.</td></tr>
	<tr><td>Email</td><td>Email address used to receive notifications</td></tr>
</table>
Now, you can log in to your WordPress blog website and publish blogs.

## Relevant Operations

Use a domain name that makes your website easier to remember. We recommend you obtain a domain name and set it to point to your WordPress site.

Domain names that point to a server inside Mainland China must obtain ICP filing from the MIIP. Tencent Cloud provide ICP filing support for free. The process usually takes 20 days.

## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting based on your actual situation.
- For issues about CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues about the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues about CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).

