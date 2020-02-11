## Operation Scenario
The LNMP environment is a website server architecture made up of Nginx, MySQL or MariaDB, and PHP in Linux system. This document describes how to manually build an LNMP environment on a Tencent Cloud Virtual Machine (CVM).

To manually build an LNMP environment, you need to be familiar with Linux commands (see [Installing software via YUM in CentOS environment](https://intl.cloud.tencent.com/document/product/213/2046) for some examples), usage and version compatibility of the software to be installed. 

## Software Versions
In this example, software versions used to build the LNMP environment are as follows:
- Linux: Linux operating system. In this example, CentOS 7.6 is used.
- Nginx: Web server. In this example, Nginx 1.17.5 is used.
- MariaDB: Database. In this example, MariaDB 10.4.8 is used.
- PHP: Scripting language. In this example, PHP 7.2.22 is used.


## Prerequisites
You have purchased a Linux CVM. If you have not yet, see [Getting started with Linux CVMs](http://intl.cloud.tencent.com/document/product/213/2936).


## Directions

### Step 1: Logging in to a Linux instance
- [Log in to a Linux instance in standard login mode (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods as needed:
- [Log in to a Linux instance by using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux instance through SSH](https://intl.cloud.tencent.com/document/product/213/32501).

### Step 2: Installing Nginx
1. Run the following command to create a file named `nginx.repo` under `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Press **i** to switch to the editing mode and enter the following.
```
[nginx] 
name = nginx repo 
baseurl = https://nginx.org/packages/mainline/centos/7/$basearch/ 
gpgcheck = 0 
enabled = 1
```
3. Press **Esc**, enter **:wq**, save the file and return.
4. Run the following command to install Nginx.
```
yum install -y nginx
```
5. Run the following command to open the `nginx.conf` file.
```
vim /etc/nginx/nginx.conf
```
6. Press **i** to switch to the editing mode, and edit the `nginx.conf` file.
The monitoring of IPv6 addresses will be canceled and Nginx will be configured to interact with PHP.
>Search for `#gzip on;` in the `nginx.conf` file, and enter the following in a new line.
>
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
7. Press **Esc**, enter **:wq**, save the file and return.
8. Run the following command to start Nginx.
```
systemctl start nginx
```
9. Run the following command to configure the automatic startup of Nginx.
```
systemctl enable nginx 
```
10. In a local browser, visit the following URL to verify that the Nginx service is working properly.
```
http://[Public IP address of the CVM instance]
```
If the following appears, Nginx has been successfully installed and configured.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Step 3: Installing Database
1. Run the following command to check whether MariaDB has been installed in the system. 
```
rpm -qa | grep -i mariadb
```
 - If the following results are returned, MariaDB already exists.
![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
To avoid conflicts between different versions, run the following command to remove the installed MariaDB.
```
yum -y remove [Package name]
```
 - If the returned result is empty, MariaDB is not installed. In this case, proceed to the next step.
2. Run the following command to create the `MariaDB.repo`  file under `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. Press **i** to switch to the editing mode and enter the following.
```
# MariaDB 10.4 CentOS repository list - created 2019-11-05 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
>For installation information about other operating system versions, visit the [MariaDB official website](https://downloads.mariadb.org).
4. Press **Esc**, enter **:wq**, save the file and return.
5. Run the following command to install MariaDB.
```
yum -y install MariaDB-client MariaDB-server
```
6. Run the following command to start the MariaDB service.
```
systemctl start mariadb
```
7. Run the following command to configure the automatic startup of MariaDB.
```
systemctl enable mariadb
```
8. Run the following command to verify that MariaDB is successfully installed.
```
mysql
```
If the following result appears, MariaDB has been successfully installed.
![](https://main.qcloudimg.com/raw/bfe9a604457f6de09933206c21fde13b.png)
9. Run the following command to exit MariaDB.
```
\q
```


### Step 4: Installing and configuring PHP
1. Run the following commands to update the software source of PHP in Yum.
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-7.noarch.rpm
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```
2. Run the following command to install the packages required for PHP 7.2.
```
yum -y install mod_php72w.x86_64 php72w-cli.x86_64 php72w-common.x86_64 php72w-mysqlnd php72w-fpm.x86_64
```
3. Run the following command to start the PHP-FPM service.
```
systemctl start php-fpm
```
4. Run the following command to configure the automatic startup of PHP-FPM service.
```
systemctl enable php-fpm
```

## Verifying the environment configuration
After finishing the environment configuration, complete the following steps to verify that the LNMP environment has been built successfully.
1. Run the following command to create a test file.
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Run the following command to restart the Nginx service.
```
systemctl restart nginx
```
3. In a local browser, visit the following URL to check whether the environment configuration is successful.
```
http://[Public IP address of the CVM instance]
```
If the following results appear, the environment configuration is successful.
![](https://main.qcloudimg.com/raw/640812413941a61efe29d7faa546ad80.png)


## Related Operations
After the LNMP environment is built, you can [manually construct a WordPress website](https://intl.cloud.tencent.com/document/product/213/8044) to gain a better understanding of CVM features.

## FAQs
If you encounter a problem when using CVM, refer to the following documents for troubleshooting as needed:
- For issues about CVM login, see [Password login and SSH key login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and remote access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues about CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and security groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues about CVM disks, see [System and data disks](https://intl.cloud.tencent.com/document/product/213/17351).




