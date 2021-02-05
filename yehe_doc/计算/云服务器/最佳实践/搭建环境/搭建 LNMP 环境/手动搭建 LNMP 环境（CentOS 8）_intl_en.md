## Overview
The LNMP environment is a website server architecture consisting of Nginx, MySQL or MariaDB, and PHP running on Linux. This document describes how to manually set up the LNMP environment on a Tencent Cloud CVM.

To manually set up the LNMP environment, you should familiarize yourself with common Linux commands and understand the usage and version compatibility of the software to be installed.

## Software
The following software is used to build the LNMP environment.
CentOS is a distribution of the Linux operating system. This document uses CentOS 8.0 as an example.
Nginx is a web server. This document uses Nginx 1.18.0 as an example.
MySQL is a database software. This document uses MySQL 8.0.21 as an example.
PHP is a scripting language. This document uses PHP 7.4.11 as an example.

## Prerequisites
A Linux CVM is required to set up a LNMP environment. If you have not purchased a Linux CVM yet, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).

## Directions
### Step 1: log in to a Linux instance
See [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
- [Log in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
- [Log in to Linux Instances via a SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)

### Step 2: install and configure Nginx
1. Run the following command to install Nginx.
>?This document takes installing Nginx 1.18.0 as an example. You can view [Nginx installation package](http://nginx.org/packages/centos/8/x86_64/RPMS/?spm=a2c4g.11186623.2.31.557423bfYPMd6u) to obtain more versions that are compatible with CentOS 8.
>
```
dnf -y install http://nginx.org/packages/centos/8/x86_64/RPMS/nginx-1.18.0-1.el8.ngx.x86_64.rpm
```
2. Run the following command to view the Nginx version.
```
nginx -v
```
If the following result is returned, it indicates that Nginx has been successfully installed.
```
nginx version: nginx/1.18.0
```
3. Run the following command to check the Nginx configuration file path.
```
cat /etc/nginx/nginx.conf
```
The `/etc/nginx/conf.d/*.conf` under the `include` configuration item indicates the default path of the Nginx configuration file.
4. Run the following commands in sequence to back up the configuration file under the default path.
```
cd /etc/nginx/conf.d
```
```
cp default.conf default.conf.bak
```
5. Run the following command to open the `default.conf` file.
```
vim default.conf
```

6. Press **i** to switch to the edit mode to modify the `default.conf` file.
  1. Add “index.php” to `index` under `location`, as shown below:
![](https://main.qcloudimg.com/raw/32df0b8ba82278cd96cf86152738677e.png)
  2. Delete the prefixed `#` of `location ~  \\.php$` and modify the following configuration items:
    - Change `root` to your website root directory. This document uses `/usr/share/nginx/html;` as an example.
    - Change `fastcgi_pass` to `unix:/run/php-fpm/www.sock;`. This configuration should be the same as `listen` in the `/etc/php-fpm.d/www.conf` file, because Nginx is associated with PHP-FPM through UNIX sockets.
    - Replace `/scripts$fastcgi_script_name;` after `fastcgi_param  SCRIPT_FILENAME` with `$document_root$fastcgi_script_name;`.
    The result should be as follows:
![](https://main.qcloudimg.com/raw/2e4bff09d70399881bfbf995390a58d3.png) 
7. Press **Esc** and enter **:wq** to save and close the file.
8. Run the following commands in sequence to enable Ngnix autostart.
```
systemctl start nginx
```
```
systemctl enable nginx
```

### Step 3: install and configure MySQL
1. Run the following command to install MySQL.
```
dnf -y install @mysql
```
2. Run the following command to view the MySQL version.
```
mysql -V
```
If the following result is returned, it indicates that MySQL has been successfully installed.
```
mysql  Ver 8.0.21 for Linux on x86_64 (Source distribution)
```
3. Run the following commands in consequence to enable MySQL autostart.
```
systemctl enable --now mysqld
```
```
systemctl status mysqld
```
4. Run the following command to complete security configurations and set password for MySQL
```
mysql_secure_installation
```
Perform the following steps:
  1. Enter `y` and press **Enter** to start configurations.
  2. Choose a password policy. A strong password policy is recommended. Enter `2` and press **Enter**.
    - 0: indicates a loose policy.
    - 1: indicates a medium policy.
    - 2: indicates a strict policy.
  3. Set the password for MySQL and press **Enter**. The password you entered will not be displayed by default.
  4. Re-enter your password, press **Enter** and enter `y` to confirm the password.
  5. Enter `y` and press **Enter** to remove anonymous users.
  6. Configure whether to disable the remote connection to MySQL:
    - Yes: enter `y` and press **Enter**.
    - No: enter `n` and press **Enter**.
  7. Enter `y` and press **Enter** to delete the test library and access permission to it.
  8. Enter `y` and press **Enter** to reload the authorization table.

### Step 4: install and configure PHP
1. Run the following commands in sequence to add and update EPEL repository.
```
dnf -y install epel-release
```
```
dnf update epel-release
```
2. Run the following commands in sequence to delete the cached unnecessary software package and update the software repository.
```
dnf clean all
```
```
dnf makecache
```
3. Run the following command to install the REMI repository.
>?Skip this step if you install PHP of version other than 7.4.11.
>
```
dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
```
4. Run the following command to start the PHP 7.4 component.
```
dnf module install php:remi-7.4
```
5. Run the following command to install the required PHP components.
```
dnf install php php-curl php-dom php-exif php-fileinfo php-fpm php-gd php-hash php-json php-mbstring php-mysqli php-openssl php-pcre php-xml libsodium
```
6. Run the following command to view the PHP version.
```
php -v
```
If the following result is returned, it indicates that PHP has been successfully installed.
```
PHP 7.4.11 (cli) (built: Sep 29 2020 10:17:06) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.11, Copyright (c), by Zend Technologies
```
7. Run the following command to open the `www.conf` file.
```
vi /etc/php-fpm.d/www.conf
```
8. Press **i** to switch to the edit mode and modify the `www.conf ` file.
9. Change `user = apache` to `user = nginx` and `group = apache` to `group = nginx`, as shown below.
![](https://main.qcloudimg.com/raw/ceb9c202ebe56c9bd9265e86c0ad2333.png)
10. Press **Esc** and enter **:wq** to save and close the file.
4. Run the following commands in sequence to start PHP-FPM and enable PHP-FPM autostart.
```
systemctl start php-fpm
```
```
systemctl enable php-fpm
```

## Verifying the Environment Configuration
1. Run the following command to create a test file.
>? This document uses `/usr/share/nginx/html` that you configured for your website root directory in Nginx as an example.
>
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Enter the following URL in your browser and verify whether the environment has been successfully configured. For more information about how to obtain the public IP address of the instance, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
```
http://Public IP address of the CVM instance/index.php
```
If the following appears, the environment has been successfully configured.
![](https://main.qcloudimg.com/raw/182c0f73df20d66216a9b73d571b2093.png)

## Relevant Operations
After the LNMP environment is built, you can [manually build a WordPress website](https://intl.cloud.tencent.com/document/product/213/8044) to familiarize yourself with CVM and its features.

## FAQs

If you encounter a problem when using CVM, refer to the following documents for troubleshooting as needed:

- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).

