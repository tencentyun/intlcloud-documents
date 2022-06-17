## Overview
The LNMP environment is a website server architecture consisting of Nginx, MySQL or MariaDB, and PHP running on Linux. This document describes how to manually set up the LNMP environment on a Tencent Cloud CVM.

To manually set up the LNMP environment, you should familiarize yourself with common Linux commands such as [installing software via YUM in CentOS](https://intl.cloud.tencent.com/document/product/213/2046), and understand the usage and version compatibility of the software to be installed.

>! It’s recommended that you can configure the LNMP environment through the image environment of Tencent Cloud marketplace, and it may take a long time to set up the LNMP environment manually.


## Software
The following software is used to build the LNMP environment.
CentOS is a distribution of the Linux operating system. This document uses CentOS 6.9 as an example.
Nginx is a web server. This document uses Nginx 1.17.5 as an example.
MySQL is a database software. This document uses MySQL 5.1.73 as an example.
PHP is a scripting language. This document uses PHP 7.1.32 as an example.

## Prerequisite

Setting up a LNMP environment requires a Linux CVM. If you have not purchased one yet, see [Getting Started with Linux CVMs](https://intl.cloud.tencent.com/zh/document/product/213/10517).


## Directions
### Step 1: log in to a Linux instance
[Log in to the Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use any of the following login methods you are comfortable with:
- [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
- [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)

### Step 2: install Nginx
1. Run the following command to create a file named `nginx.repo` under `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Press **i** to switch to the editing mode and enter the following.
```
[nginx]
name=nginx repo
baseurl=https://nginx.org/packages/mainline/centos/6/$basearch/
gpgcheck=0
enabled=1
```
3. Click **Esc** and enter **:wq** to save and close the file.
4. Run the following command to install Nginx.
```
yum install -y nginx
```
5. Run the following command to open the `default.conf` file.
```
vim /etc/nginx/conf.d/default.conf
```
6. Press **i** to switch to the edit mode to modify the `default.conf` file.
7. Find `server{...}` and replace the content inside the curly brackets with the following. This is to cancel the listening of the IPv6 address and configure Nginx to realize linkage with PHP.
```
server {
	listen       80;
	root   /usr/share/nginx/html;
	server_name  localhost;
	#charset koi8-r;
	#access_log  /var/log/nginx/log/host.access.log  main;
	#
	location / {
		  index index.php index.html index.htm;
	}
	#error_page  404              /404.html;
	#redirect server error pages to the static page /50x.html
	#
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
	  root   /usr/share/nginx/html;
	}
	#pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
	#
	location ~ .php$ {
	  fastcgi_pass   127.0.0.1:9000;
	  fastcgi_index  index.php;
	  fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
	  include        fastcgi_params;
	}
}
```
8. Press **Esc** and enter **:wq**. Save and close the file.
9. Run the following command to start Nginx.
```
service nginx start
```
10. Run the following commands to automatically launch Nginx at startup.
```bash
chkconfig --add nginx
```
```
chkconfig  nginx on
```
11. Enter the following URL in your local browser and verify whether the Nginx service is working properly.
```
http://[Public IP address of the CVM instance]
```
If the following appears, Nginx has been successfully installed and configured.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Step 3: install a database
1. Run the following command to check whether MySQL has been already installed.
```
rpm -qa | grep -i mysql
```
 - If the following appears, MySQL has already been installed.
![](https://main.qcloudimg.com/raw/74e544638637d39209cc1e474083d11d.png)
To avoid conflicts between different versions, run the following command to remove the existing MySQL.
```
yum -y remove [Package name]
```
 - If nothing is returned, MySQL has not been installed. In this case, proceed to the next step.
2. Run the following command to install MySQL.
```
yum install -y mysql-devel.x86_64 mysql-server.x86_64 mysql-libs.x86_64
```
3. Run the following command to start MySQL.
```
service mysqld start 
```
4. Run the following commands to automatically launch MySQL at startup.
```bash
chkconfig --add mysqld
```
```
chkconfig mysqld  on 
```
5. Run the following command to verify whether MySQL has been successfully installed.
```
mysql
```
If the following appears, MariaDB has been successfully installed.
![](https://main.qcloudimg.com/raw/9c9347ad0264ddad5e98c8dd48adcc6a.png)
6. Run the following command to exit MySQL.
```
\q
```

### Step 4: install and configure PHP
1. Run the following commands to update the software source of PHP in Yum.
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-6.noarch.rpm
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
```
2. Run the following command to install the packages required for PHP 7.1.32.
```
yum -y install mod_php71w.x86_64 php71w-cli.x86_64 php71w-common.x86_64 php71w-mysqlnd php71w-fpm.x86_64
```
3. Run the following command to start the PHP-FPM service.
```
service php-fpm start
```
4. Run the following commands to automatically launch PHP-FPM at startup.
```bash
chkconfig --add php-fpm  
```
```
chkconfig php-fpm on
```


## Verifying the Environment Configuration
1. Run the following command to create a test file.
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Run the following command to restart Nginx.
```
service nginx restart
```
3. In a local browser, visit the following URL to check whether the environment has been successfully configured.
```
http://[Public IP address of the CVM instance]
```
If the following appears, the environment has been successfully configured.
![](https://main.qcloudimg.com/raw/64af927320f2121ae4daf15cf2eaba39.png)



## Related Operations

After the LNMP environment is built, you can [manually build a WordPress website](https://intl.cloud.tencent.com/document/product/213/8044) to familiarize yourself with CVM and its features.

## FAQs

If you encounter a problem when using CVM, refer to the following documents for troubleshooting:

- CVM login: [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- CVM network: [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- CVM disks: [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).
