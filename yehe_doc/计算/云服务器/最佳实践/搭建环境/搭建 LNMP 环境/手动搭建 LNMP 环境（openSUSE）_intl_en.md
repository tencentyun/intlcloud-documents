## Introduction
LNMP refers to a common web server architecture consisting of Nginx, MySQL or MariaDB, and PHP running on Linux. This article describes how to deploy LNMP on a Tencent Cloud Virtual Machine (CVM).
You need to install several software packages on Linux. If you do not know how to perform software installation on Linux, refer to [this article](https://intl.cloud.tencent.com/document/product/213/2047).

## Software
This article uses the following software to build the LNMP environment:
- OS: openSUSE 42.3
- Web server: Nginx 1.14.2
- Database: MySQL 5.6.43
- Hypertext processor: PHP 7.0.7

##  Prerequisites
You have purchased a Linux CVM. If you have not yet, see [Getting started with Linux CVMs](http://intl.cloud.tencent.com/document/product/213/2936).

## Directions
### Step 1: Logging in to a Linux instance
- [Log in to a Linux instance in standard login mode (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods as needed:
- [Log in to a Linux instance by using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux instance through SSH](https://intl.cloud.tencent.com/document/product/213/32501).

### Step 2: Adding image source
1. Log in to your CVM.
2. Run the following commands to add image source:
```
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/oss suseOss
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/non-oss suseNonOss
```
3. Run the following command to update the source you just added.
```
zypper ref
```

### Step 3: Installing and configuring Nginx
1. Run the following command to install Nginx.
``` 
zypper install -y nginx
```
2. Run the following command to start the Ngnix server and set it to auto start when the CVM starts up.
```
systemctl start nginx
systemctl enable nginx
```
3. Run the following to edit the Nginx configuration file.
```
Vi /etc/nginx/nginx.conf
```
4 Press **i** to toggle edit mode.
5. Find **server{...}** and replace it with the following content:
```
server {
	listen       80;
	server_name  localhost;
	#access_log  /var/log/nginx/log/host.access.log  main;
	location / {
			root   /srv/www/htdocs/;
			index index.php index.html index.htm;
	}
	#error_page  404              /404.html;
	#redirect server error pages to the static page /50x.html
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
			root   /srv/www/htdocs/;
	}
	#pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ .php$ {
			root           /srv/www/htdocs/;
			fastcgi_pass   127.0.0.1:9000;
			fastcgi_index  index.php;
			fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
			include        fastcgi_params;
	}
}
```
7. When you finish, press **Esc** to exit edit mode. Then enter **:wq** to save the file and exit Vi.
8. Run the following command to restart the Nginx service.
```
systemctl restart nginx
```
9. Run the following command to create an index page called `index.html`.
```
vi /srv/www/htdocs/index.html
```
10. Press **i** to switch to edit mode and **Enter** the following.
```html
<p> hello world!</p>
```
11. After you finish, press **Esc** to exit edit mode. Then enter **:wq** to save the file and exit Vi.
12. Access the public IP of your CVM on the browser to check if your Nginx is running properly.
If the following appears, Nginx has been successfully installed and configured.
![](https://main.qcloudimg.com/raw/df09d1fe6baed50cebd89ef7402db4b2.png)

## Step 4: Installing and configuring MySQL
1. Run the following command to install MySQL.
```
zypper install -y mysql-community-server mysql-community-server-tools
```
2. Run the following command to start the MySQL service and set it to auto start when your CVM starts up.
```
systemctl start mysql 
systemctl enable mysql
```
3. Run the following command to log in to MySQL.
> When you login for the first time, MySQL will ask you to setup a password. If you do not wish to do so, press **Enter** to skip the step.
>
```
mysql -u root -p
```
If the following appears, you have successfully logged in.
![](https://main.qcloudimg.com/raw/1e9daf876fb08c70674789865688f695.png)
4. Run the following command to change the root password.
```
update mysql.user set password = PASSWORD('NEW_PASSWORD') where user='root';
```
5. Run the following command to apply the configuration:
```
flush privileges;
```
6. Run the following command to exit MySQL.
```
\q
```

### Step 5: Installing PHP
Run the following command to install PHP:
```
zypper install -y php7 php7-fpm php7-mysql
```

### Step 6: Configuring Nginx with PHP-FPM
1. Run the following commands to navigate to `/etc/php7/fpm` and rename `php-fpm.conf.default` to `php-fpm.conf`.
```
cd /etc/php7/fpm
cp php-fpm.conf.default php-fpm.conf
``` 
2. Run the following commands to navigate to `/etc/php7/fpm/php-fpm.d` and rename `www.conf.default` to `www.conf`.
```
cd /etc/php7/fpm/php-fpm.d
cp www.conf.default www.conf
```
3. Run the following commands to start PHP-FPM and set it to auto start when your CVM starts up.
```
systemctl start php-fpm
systemctl enable php-fpm
```

## Verifying Your Setup
1. Run the following command to create a file named index.php.
```
Vi /srv/www/htdocs/index.php
```
2. Press **i** to switch to edit mode and enter the following:
```
<?php
	echo "hello new world!";
?>
```
3. Press **Esc** to exit edit mode. Then enter **:wq** to save the file and exit.
4. Access the public IP of your CVM on the browser.
If the following appears, then your LNMP setup has been installed and configured successfully.
![](https://main.qcloudimg.com/raw/0adc6168e7407931c597228520b35413.png)

## See Also
After the LNMP environment is built, you can use it to [set up a WordPress website](https://intl.cloud.tencent.com/document/product/213/8044) to familiarize yourself with your CVM and what it can do.

## FAQ
If you encounter issues when using CVM, refer to the following documents for troubleshooting:
For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
For issues regarding the CVM’s network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).



