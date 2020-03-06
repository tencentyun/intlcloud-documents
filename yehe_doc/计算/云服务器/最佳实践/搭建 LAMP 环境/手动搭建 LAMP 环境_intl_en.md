## Scenario
LAMP is a common web service architecture run on Linux and consisting of Apache, MySQL/MariaDB, and PHP. This article describes how to set up LAMP on a Linux CVM.

You should be familiar with common Linux commands, such as [Installing Software via YUM in a CentOS Environment](https://intl.cloud.tencent.com/document/product/213/2046), and understand the versions of the installed software.

## Software
These are the software involved:
- CentOS is a distribution of the Linux operating system. We will use version 7.6 in this article.
- Apache is a web server software. We will use version 2.4.6 in this article.
- MariaDB is a database management system. We will use version 10.4.8 in this article.
- PHP is a scripting language. We will use version 7.0.33 in this article.

## Prerequisites
You need a Linux CVM. If you have not purchased one yet, see [Getting Started with Linux CVMs](http://intl.cloud.tencent.com/document/product/213/2936).

## Instructions
### Step 1: Logging in to a Linux instance
[Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux Instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Step 2: Installing Apache
1. Run the following command to install Apache.
```
yum install httpd -y
```
2. Run the following commands to start Apache and set it to start automatically when the system starts.
```
systemctl start httpd
```
```
systemctl enable httpd
```
3. Open a browser window and visit the following URL to verify that Apache is working properly.
```
http://[Public IP address of the CVM instance]
```
The following appears if Apache is installed properly:
![](https://main.qcloudimg.com/raw/f9dc3992f4d6e7e94bb63330fd5cadfe.png)


### Step 3: Installing MariaDB
1. Run the following command to check if MariaDB is already installed.
```
rpm -qa | grep -i mariadb
```
 - If the following appears, MariaDB is already installed.
 ![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
If that’s the case, run the following to remove MariaDB to avoid conflicts between different versions.
```
yum -y remove [Package name]
```
 - If nothing is returned, MariaDB is not installed. In this case, proceed to the next step.
2. Run the following command to create a file named `MariaDB.repo` under `/etc/yum.repos.d/`. 
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. Press **i** to switch to edit mode and input the following.
```
# MariaDB 10.4 CentOS repository list - created 2019-11-05 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
>For installation information for other versions, visit the [MariaDB official website](https://downloads.mariadb.org).
>
5. Press **Esc** and input **:wq** to save the file and go back.
6. Run the following command to install MariaDB.
```
yum -y install MariaDB-client MariaDB-server
```
7. Run the following commands to start MariaDB and set it to start automatically when the system starts.
```
systemctl start mariadb
```
```
systemctl enable mariadb
```
8. Run the following command to verify that MariaDB is successfully installed.
```
mysql
```
If the following appears, MariaDB is successfully installed.
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
2. Run the following command to install the packages required for PHP 7.0.33.
```
yum -y install php70w php70w-opcache php70w-mbstring php70w-gd php70w-xml php70w-pear php70w-fpm php70w-mysql php70w-pdo
```
3. Run the following command to edit the Apache configuration file.
```
vi /etc/httpd/conf/httpd.conf
```
4. Press **i** to enter edit mode and make the following changes:
![](https://main.qcloudimg.com/raw/0b478ca5aa21124a531cfd5c8860cb70.png)
![](https://main.qcloudimg.com/raw/aeeb6fff1af9cf71735cae558455ee94.png)
![](https://main.qcloudimg.com/raw/cc840587150c3282c972a6b23e0c1a68.png)
![](https://main.qcloudimg.com/raw/de36e94d0e4791d1d84f141120125456.png)
 1. Find `ServerName www.example.com:80` and start a new line below it. Input the following:
 ```
ServerName localhost:80
```
 2. Find `Require all denied` in `<Directory>` and change it to `Require all granted`.
 3. Find `<IfModule dir_module>` and change the content to `DirectoryIndex index.php index.html`.
 4. Start a new line below `AddType application/x-gzip .gz .tgz` and input the following:
```
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps
```
5. Press **Esc** and input **:wq** to save the file and go back.
6. Run the following command to restart Apache.
```
systemctl restart httpd
```

## Verifying the Environment Configuration
1. Run the following command to create a test file.
```
echo "<?php phpinfo(); ?>" >> /var/www/html/index.php
```
2. Open a browser window on your local machine and visit the following URL to check whether the environment configuration is successful.
```
http://CVM Public IP/index.php
```
If the following appears, the LAMP environment is configured successfully.
![](https://main.qcloudimg.com/raw/64681fb76bad29072de9ddc3250e66d1.png)

## Relevant Operations
After the LAMP environment is built, you can [manually set up Drupal website](https://intl.cloud.tencent.com/document/product/213/34814).


## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting based on your actual situation.
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).

