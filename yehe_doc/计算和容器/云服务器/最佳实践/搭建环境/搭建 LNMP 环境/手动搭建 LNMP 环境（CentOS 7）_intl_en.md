## Overview
The LNMP environment is a website server architecture consisting of Nginx, MySQL or MariaDB, and PHP running on Linux. This document describes how to manually set up the LNMP environment on a Tencent Cloud CVM.

To manually set up the LNMP environment, you should familiarize yourself with common Linux commands such as [installing software via YUM in CentOS](https://intl.cloud.tencent.com/document/product/213/2046), and understand the usage and version compatibility of the software to be installed.
## Software
The following software is used to build the LNMP environment.
- Linux: Linux operating system. This document uses CentOS 7.6 as an example.
- Nginx: web server. This document uses Nginx 1.17.7 as an example.
- MariaDB: database. This document uses MariaDB 10.4.8 as an example.
- PHP: scripting language. This document uses PHP 7.2.22 as an example.


## Prerequisites
You have purchased a Linux CVM.


## Directions

### Step 1: log in to a Linux instance
See [Logging in to Linux Instance Using WebShell (Recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:

- [Logging in to Linux Instance via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502).
- [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501).

### Step 2: install Nginx
1. Run the following command to create a file named `nginx.repo` under `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Press **i** to switch to edit mode and enter the following content:
```
[nginx] 
name = nginx repo 
baseurl = https://nginx.org/packages/mainline/centos/7/$basearch/ 
gpgcheck = 0 
enabled = 1
```
3. Press **Esc** and enter **:wq** to save and close the file.
4. Run the following command to install Nginx.
```
yum install -y nginx
```
5. Run the following command to open `nginx.conf`.
```
vim /etc/nginx/nginx.conf
```
6. Press **i** to switch to edit mode and modify the `nginx.conf` file.
7. Find `server{...}` and replace the content inside the curly brackets with the following. This is to cancel the listening of the IPv6 address and configure Nginx to realize linkage with PHP.
>? Press `Ctrl+F` for page down and `Ctrl+B` for page up.
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
If you cannot find `server{...}` in the `nginx.conf` file, add the `server{...}` content above to the top of `include /etc/nginx/conf.d/*conf;`, as shown below:
![](https://main.qcloudimg.com/raw/901a3957ccd992c2fb345287271c4bef.png)
7. Press **Esc** and enter **:wq** to save and close the file.
8. Run the following command to start Nginx.
```
systemctl start nginx
```
9. Run the following command to enable Nginx autostart.
```
systemctl enable nginx 
```
10. Enter the following URL in your local browser and verify whether the Nginx service is working properly.
```
http://[Public IP address of the CVM instance]
```
If the following appears, Nginx has been successfully installed and configured.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Step 3: install a database
1. Run the following command to check whether MariaDB has been installed in the system. 
```
rpm -qa | grep -i mariadb
```
 - If the following appears, MariaDB is already installed.
![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
To avoid conflicts between different versions, run the following command to remove the installed MariaDB.
```
yum -y remove [Package name]
```
 - If the returned result is empty, MariaDB is not installed. In this case, proceed to the next step.
2. Execute the following command to create the `MariaDB.repo` file under `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. Press **i** to switch to edit mode and enter the following content to add MariaDB.
>? 
>- Different operating systems require different versions of MariaDB. Download [MariaDB](https://downloads.mariadb.org) that is compatible with your operating system.
>- If your CVM has [private network access](https://intl.cloud.tencent.com/document/product/213/5225), change `mirrors.cloud.tencent.com` to the private network address `mirrors.tencentyun.com`. In this way, your public network traffic will not be affected and the access is faster.
>
```
# MariaDB 10.4 CentOS repository list - created 2019-11-05 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = https://mirrors.cloud.tencent.com/mariadb/yum/10.4/centos7-amd64
gpgkey=https://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
4. Press **Esc** and enter **:wq** to save and close the file.
5. Run the following command to install MariaDB. The installation may take quite a while. 
```
yum -y install MariaDB-client MariaDB-server
```
6. Run the following command to start the MariaDB service.
```
systemctl start mariadb
```
7. Run the following command to enable MariaDB autostart.
```
systemctl enable mariadb
```
8. Run the following command to verify that MariaDB is successfully installed.
```
mysql
```
If the following appears, MariaDB has been successfully installed.
![](https://main.qcloudimg.com/raw/bfe9a604457f6de09933206c21fde13b.png)
9. Run the following command to exit MariaDB.
```
\q
```


### Step 4: install and configure PHP
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
4. Run the following command to enable PHP-FPM autostart.
```
systemctl enable php-fpm
```

## Verifying the Environment Configuration
Follow these steps to verify that the LNMP environment has been built successfully.
1. Run the following command to create a test file.
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Run the following command to restart the Nginx service.
```
systemctl restart nginx
```
3. Enter the following URL in a local browser to check whether the environment configuration is successful.
```
http://[Public IP address of the CVM instance]
```
If the following appears, the environment has been successfully configured.
![](https://main.qcloudimg.com/raw/640812413941a61efe29d7faa546ad80.png)


## Relevant Operations
After the LNMP environment is built, you can [manually build a WordPress website](https://intl.cloud.tencent.com/document/product/213/8044) to familiarize yourself with CVM and its features.

## FAQs
If you encounter a problem when using CVM, refer to the following documents for troubleshooting as needed:
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).
