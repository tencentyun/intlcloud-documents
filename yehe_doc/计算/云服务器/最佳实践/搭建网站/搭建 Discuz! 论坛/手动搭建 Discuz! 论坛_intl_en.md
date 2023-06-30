## Overview

Used by over 2 million websites, Discuz! is the world’s most sophisticated and predominant forum software. This document describes how to set up a forum website using Discuz! on Tencent Cloud CVM instance and deploy the LAMP (Linux, Apache, MariaDB, and PHP) runtime environment it needs.


To manually set up a Discuz! website, you should be familiar with common Linux commands (see [Installing Software via YUM under CentOS Environment](https://intl.cloud.tencent.com/document/product/213/2046)), and understand the usage and version compatibility of the software to be installed.





## Software
The following software versions are used to build a Discuz! website.
- Linux: Linux operating system. This document uses CentOS 7.6 as an example.
- Apache: Web server software. This document uses Apache 2.4.15 as an example.
- MariaDB: database. This document uses MariaDB 5.5.60 as an example.
- PHP: scripting language. This document uses PHP 5.4.16 as an example.
- Discuz!: forum software. This document uses Discuz! X3.4 as an example.


## Directions
### Step 1: log in to the CVM
[Log in to the Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use any of the following login methods you are comfortable with:
- [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
- [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)



### Step 2: set up the LAMP environment 

Tencent Cloud hosts a software repository containing CentOS official releases, which provides the most stable version available currently. Use Yum to quickly install CentOS.


#### Installing and configuring necessary software[](id:InstallNecessarySoftware)
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
3. [](id:step3)Run the following command to set a password for `root` and complete other basic configurations, so the root user can access the database.
<dx-alert infotype="notice" title="">
- Run the following command to set the password before your first login to MariaDB.
- When you see the prompt to enter the root password, click **Enter** to set the password. Your password will not be displayed by default. Complete other basic configurations as prompted.
</dx-alert>
```
mysql_secure_installation
```
4. Run the following command to log in to MariaDB. Enter the password you set in [step 3](#step3) and click **Enter**.
```
mysql -u root -p
```
A successful login indicates that the configurations are correct, as shown below:
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
2. Click **i** to switch to editing mode and enter the following content:
```
<?php
echo "<title>Test Page</title>";
phpinfo()
?>
```
3. Click **Esc** and enter **:wq** to save and close the file.
4. Enter the following URL in a browser to access `test.php` to check whether the environment is properly configured.
```
http://[Public IP address of the CVM]/test.php 
```
If everything goes well, the following appears.
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)




### Step 3: install and configure Discuz![](id:InstallDiscuz)

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
2. Run the following command to copy all files under "upload" to `/var/www/html/`.
```
cp -r upload/* /var/www/html/
```
3. Run the following command to grant other users the write permission.
```
chmod -R 777 /var/www/html
```

#### Installing Discuz!
1. Enter the IP address of your Discuz! site (the public IP address of your CVM instance) or the domain name obtained from [Related Operations](#ConfigureDomain), and then you can see the Discuz! installation interface.
<dx-alert infotype="explain" title="">
This document only demonstrates the installation steps. If a security warning that the version is too low is reported, we recommend you use an image on a higher version.
</dx-alert>
2. Click **I agree** and go to the environment check page.
3. Check the items and click **Next Step** to go to the runtime environment setting page.
4. Select "Clean Install" and click **Next Step** to go to the database creation page.
5. Enter information as prompted to create a new database for Discuz!.
<dx-alert infotype="notice" title="">
- Use the `root` account and password set in [Installing and configuring required software](#InstallNecessarySoftware) to connect to the database and set up a system email address and admin username, password, and email address.
- Remember your admin username and password.
</dx-alert>
6. Click **Next** to start the installation.
6. After the installation, click **Your forum has been installed successfully. Click here to access.** to access your forum.


## Related Operations[](id:ConfigureDomain)
You can use a domain name that is easy to remember rather than a complicated IP address to make your forum website easier to remember and access. If you set up this website just for the purpose of learning, you can use an IP address for temporary use, which is nevertheless not recommended.


## FAQs
If you encounter a problem when using CVM, refer to the following documents for troubleshooting:
- CVM login: [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- CVM network: [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- CVM disks: [System and Data Disks](https://intl.cloud.tencent.com/zh/document/product/213/17351).



