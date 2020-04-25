## Use Case

With more than 2 million forums based on Discuz!, it is the most sophisticated and predominant internet discussion software in the world. This article describes how to create a forum using Discuz! and deploy the LAMP (Linux, Apache, MariaDB, and PHP) runtime environment it needs.


To set up Discuz! manually, you should be familiar with common Linux commands, such as [Installing Software via YUM in CentOS](https://intl.cloud.tencent.com/document/product/213/2046) and know how to use the software you install and their version compatibility.

## Software
This article uses the following:
- Operating system: CentOS 7.5, a distribution of Linux
- Web server: Apache 2.4.6
- Database: MariaDB 5.5.60
- Hypertext processor: PHP 5.4.16
- Forum software: Discuz! X3.2


## Procedure
### Step 1: Logging in to Linux CVM
[Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use another login method that you are comfortable with.
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)



### Step 2: Setting up LAMP 

Tencent Cloud hosts an image of the CentOS official version installation source, which contains the most recent and stable version of the software. Use Yum to install CentOS.

<span id="InstallNecessarySoftware"></span>
#### Installing and configuring required software
1. Run the following command to install Apache, MariaDB, and PHP:
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server -y
```
2. Run the following commands to start the services:
```
systemctl start httpd
systemctl start mariadb
systemctl start php-fpm
```
3. <span id="step3"></span>Run the following commands to set a password for `root` and configure the database so `root` can access it.
>
>- Run the command before you log in to MariaDB for the first time.
>- Enter the password for `root` and press **Enter**. Your password is not shown on the screen. Enter the password a second time to confirm and complete the configuration as prompted on the screen.
> 
```
mysql_secure_installation
```
4. Run the following command to log in to MariaDB. Use the password you set in [Step 3](#step3) and press **Enter**.
```
mysql -u root -p
``` 
A successful login is shown below:
![](https://main.qcloudimg.com/raw/e22b91cc30bf4155436ab398ee44502a.png)

5. Run the following command to exit MariaDB.
```
exit
```

#### Verifying Your Setup

Follow these steps to make sure the environment is set up properly:
1. Run the following command to create a test file `test.php` in the default root directory "/var/www/html" of Apache:
```
vim /var/www/html/test.php
```
2. Press **i** to switch to edit mode and enter the following:
```
<?php
echo "<title>Test Page</title>";
phpinfo();
?>
```
5. Press **Esc** and input **:wq** to save the file and exit Vim.
3. Open a browser window and use the following URL to access `test.php` to check whether the environment is properly configured.
```
http://CVM_public_IP/test.php 
```
If it is, the following appears:
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)



<span id="InstallDiscuz"></span>
### Step 3: Installing and configuring Discuz!  

#### Downloading Discuz! 
Run the following command to download the installation package.
```
wget http://download.comsenz.com/DiscuzX/3.2/Discuz_X3.2_SC_UTF8.zip
```

#### Preparing for installation
1. Run the following command to decompress the installation package.
```
unzip Discuz_X3.2_SC_UTF8.zip
```
2. Run the following command to copy all files under "upload" to "/var/www/html/".
```
cp -r upload/* /var/www/html/
```
3. Run the following command to give users write permission:
```
chmod -R 777 /var/www/html
```

#### Installing Discuz!
1. Open a browser window and go to the IP address of your Discuz! forum (your CVM public IP address), or you can [bind a domain name](#ConigureDomain) to your IP address.
2. Click **I agree** to start the process. Discuz! checks to see if the environment is properly installed and configured.
3. Click **Next Step** when the check finishes. 
4. Select clean install, and click **Next Step**.
5. Enter information as prompted to create a new database for Discuz!.
>  
>- Use `root` and the password set in [Installing and configuring required software](#InstallNecessarySoftware) to connect to the database and set up a system email address and administrator username, password, and email address.
>- Remember your administrator username and password.
>
6. Click **Next Step** to start installation.
6. After the installation is completed, click **Your forum has been installed successfully. Click here to access.** to access your forum.

<span id="ConfigureDomain"></span>
## Using a Domain Name
Use a domain name that makes your website easier to remember. We recommend you obtain a domain name and set it to point to your Discuz! site. If you are installing Discuz! just to learn the process, you can keep using the IP address. Otherwise, use a domain name.

## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting:
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).
 
