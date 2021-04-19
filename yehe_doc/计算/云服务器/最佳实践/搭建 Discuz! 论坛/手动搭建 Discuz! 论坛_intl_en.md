## Overview

Used by over 2 million websites, Discuz! is the world’s most sophisticated and predominant forum software. This document describes how to create a website using Discuz! on Tencent Cloud CVM instance and deploy the LAMP (Linux, Apache, MariaDB, and PHP) runtime environment it needs.


To manually set up a Discuz! site, you should be familiar with common Linux commands (See [Installing Software via YUM under CentOS Environment](https://intl.cloud.tencent.com/document/product/213/2046), and understand the usage and version compatibility of the software to be installed.
## Software
The following software is used to build a Discuz! website.
- Linux: Linux operating system. This document uses CentOS 7.6 as an example.
- Apache: Web server software. This document uses Apache 2.4.15 as an example.
- MariaDB: database. This document uses MariaDB 5.5.60 as an example.
- PHP: scripting language. This document uses PHP 5.4.16 as an example.
- Discuz!: forum software. This document uses Discuz! X3.4 as an example.


## Directions
### Step 1: log in to the CVM
See [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:

- [Log in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)



### Step 2: set up the LAMP environment 

Tencent Cloud hosts a software repository containing CentOS official releases, which provides the most recent and stable version. Use Yum to quickly install CentOS.

<span id="InstallNecessarySoftware"></span>
#### Installing and configuring required software
1. Run the following command to install Apache, MariaDB, PHP and Git:
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server git -y
```
2. Run the following commands in sequence to start the services.
```
systemctl start httpd
```
```
systemctl start mariadb
```
```
systemctl start php-fpm
```
3. <span id="step3"></span>Run the following command to set a password for `root` user and complete other basic configurations, so the root user can access the database.
>!
>- Run the following command to set the password before your first login to MariaDB.
>- When you see the prompt to enter root password, press Enter set the password. Your password will not be displayed by default. Complete other basic configurations as prompted.
> 
```
mysql_secure_installation
```
4. Run the following command to log in to MariaDB. Enter the password you set in [step 3](#step3) and press **Enter**.
```
mysql -u root -p
```
A successful login is shown below:
![](https://main.qcloudimg.com/raw/18c54971e141db38c3f483161fefe251.png)

5. Run the following command to exit MariaDB.
```
\q
```

#### Verifying the environment configuration

Check whether the environment is set up properly as instructed below:
1. Run the following command to create a test file `test.php` in the default root directory `/var/www/html` of Apache:
```
vim /var/www/html/test.php
```
2. Press **i** to switch to edit mode and enter the following content:
```
<?php
echo "<title>Test Page</title>";
phpinfo()
?>
```
3. Press **Esc** and enter **:wq** to save and close the file.
4. Enter the following URL in a browser to access `test.php` to check whether the environment is properly configured.
```
http://[Public IP address of the CVM]/test.php 
```
If everything goes well, the following appears.
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)



<span id="InstallDiscuz"></span>
### Step 3: install and configure Discuz!  

#### Downloading Discuz! 
Run the following command to download the installation package.
```
git clone https://gitee.com/Discuz/DiscuzX.git
```

#### Preparing for installation
1. Run the following command to access the installation directory.
```
cd DiscuzX
```
2. Run the following command to copy all files under "upload" to "/var/www/html/".
```
cp -r upload/* /var/www/html/
```
3. Run the following command to grant users the write permission.
```
chmod -R 777 /var/www/html
```

#### Installing Discuz!
1. Enter the IP address of your Discuz! site (the public IP address of your CVM instance) in the address box, or you can [bind an available domain name](#ConfigureDomain) to your IP address.
2. Click **I agree** and go to the environment check page.
3. Check the items and click **Next Step**.
4. Select **Clean Install**, and click **Next Step**.
5. Enter information as prompted to create a new database for Discuz!.
>!  
>- Use `root` and the password set in [Installing and configuring required software](#InstallNecessarySoftware) to connect to the database and set up a system email address and administrator username, password, and email address.
>- Remember your administrator username and password.
>
6. Click **Next Step** to start installation.
7. After the installation, click **Your forum has been installed successfully. Click here to access.** to access your forum.

<span id="ConfigureDomain"></span>
## Using a Domain Name
Using a domain name instead of an IP can help users remember your website easier.

## FAQs
Check the following documentation for problems of using CVM: 
- CVM login: [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278)
- CVM network: [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502)
- CVM disks: [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351)



