## Introduction
The LNMP environment is a website server architecture run on Linux and consisting of Nginx, MySQL or MariaDB, and PHP. This article describes how to set up LNMP on a CVM.

To set up the LNMP environment, you should be familiar with common Linux commands, such as [Installing Software via YUM in CentOS](https://intl.cloud.tencent.com/document/product/213/2046) for some examples), and understand the versions of the installed software.

## Software
The following software are involved:
CentOS is a distribution of the Linux operating system. We use CentOS 6.9 in this article.
Nginx is a web server. We use Nginx 1.17.5 in this article.
MySQL is a database software. We use MySQL 5.1.73.
PHP is a scripting language. We use PHP 7.1.32 in this article.

## Prerequisites

You need a Linux CVM. If you have not purchased one yet, see [Getting Started with Linux CVMs](http://intl.cloud.tencent.com/document/product/213/2936).


## Directions
### Step 1: Logging in to a Linux instance
[Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501).

### Step 2: Installing Nginx
1. Run the following command to create a file named `nginx.repo` under `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Press **i** to enter edit mode and input the following.
```
[nginx]
name = nginx repo
baseurl=https://nginx.org/packages/mainline/centos/6/$basearch/
gpgcheck=0
enabled=1
```
5. Press **Esc** and input **:wq** to save the file and go back.
4. Run the following command to install Nginx.
```
yum install -y nginx
```
5. Run the following command to open `nginx.conf`.
```
vim /etc/nginx/nginx.conf
```
6. Press **i** to switch to edit mode.
7. Find `server{...}` and replace the content inside the curly brackets with the following:
   This cancels the monitoring of IPv6 addresses and configures Nginx to interact with PHP.
> If you cannot find `server{...}` in `nginx.conf`, add the following above `include /etc/nginx/conf.d/*conf;`
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
8. Press **Esc** and input **:wq** to save the file and go back.
9. Run the following command to start Nginx.
```
service nginx start
```
10. Run the following command to set Nginx to start automatically when the system starts.
```bash
chkconfig --add nginx
```
```
chkconfig  nginx on
```
11. In a local browser, visit the following URL to verify that the Nginx service is working properly.
```
http://[Public IP address of the CVM instance]
```
If the following appears, Nginx has been successfully installed and configured.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Step 3: Installing MySQL
1. Run the following command to check if MySQL is already installed.
```
rpm -qa | grep -i mysql
```
 - If the following appears, MySQL is already installed.
![](https://main.qcloudimg.com/raw/74e544638637d39209cc1e474083d11d.png)
To avoid conflict between different versions, run the following command to remove the existing MySQL.
```
yum -y remove [Package name]
``` 
 - If nothing is returned, MySQL is not installed. In this case, proceed to the next step.
2. Run the following command to install MySQL.
```
yum install -y mysql-devel.x86_64 mysql-server.x86_64 mysql-libs.x86_64
```
3. Run the following command to start MySQL.
```
service mysqld start 
```
4. Run the following command to set MySQL to start automatically when the system boots up.
```bash
chkconfig --add mysqld
```
```
chkconfig mysqld  on 
```
5. Run the following command to verify MySQL installation.
```
mysql
```
If the following appears, MySQL has been successfully installed.
![](https://main.qcloudimg.com/raw/9c9347ad0264ddad5e98c8dd48adcc6a.png)
6. Run the following command to exit MySQL.
```
\q
```

### Step 4: Installing and configuring PHP
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
4. Run the following command to set the PHP-FPM service to start automatically.
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
3. In a local browser, visit the following URL to check whether the environment configuration is successful.
```
http://[Public IP address of the CVM instance]
```
If the following results appear, the environment configuration is successful.
![](https://main.qcloudimg.com/raw/64af927320f2121ae4daf15cf2eaba39.png)



## Related Operations

After the LNMP environment is built, you can [start a WordPress website](https://intl.cloud.tencent.com/document/product/213/8044).

## FAQ

If you encounter a problem when using CVM, refer to the following documents for troubleshooting based on your actual situation.

- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).



