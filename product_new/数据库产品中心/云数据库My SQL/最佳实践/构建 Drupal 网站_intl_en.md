Drupal is an open-source content management framework written in PHP, which consists of a content management system and a PHP development framework. It can be used to build rich-featured dynamic websites ranging from personal blogs to large communities.
This tutorial describes how to build a Drupal ecommerce website on a CVM instance.
Software environments used here include CentOS v7.2, Drupal v7.56, and PHP v5.4.16.

### Logging in to the CVM Instance
For more information on how to purchase and access CVM instances, see [Getting Started with Linux-based CVM](http://intl.cloud.tencent.com/document/product/213/2936).

### Installing the MariaDB Service
1. MariaDB is supported by CentOS v7 and higher by default, so it is used here. Install the MariaDB service in the CVM instance with `yum`.
```
yum install mariadb-server mariadb -y
```
2. Start the MariaDB service.
```
systemctl start mariadb
```
3. Create a database named drupal for Drupal.
```
mysqladmin -u root -p create drupal
```
Here, "drupal" is the database name used in the Drupal service.
4. Create a user for the database.
```
mysql -u root -p
```
Authorize the user and exit the database after the authorization is successful.
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON drupal.* TO 'username'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
exit
```
Here, "username" and "password" are the database username and password used in the Drupal service, respectively.

### Installing the Apache Service
1. Install Apache in the CVM instance with `yum`.
```
yum install httpd -y
```
2. Start the Apache service.
```
service httpd start
```
3. Test Apache.
>In this step, you should configure an inbound rule with the source being **all** and the port protocol being **TCP:80** in the security group of your CVM instance. For more information on how to configure the security group, see [Security Group](http://intl.cloud.tencent.com/document/product/213/12452).
>
Enter `http://115.xxx.xxx.xxx/` in your local browser (where `115.xxx.xxx.xxx` is the public IP of your CVM instance). If the following page appears, Apahce has started successfully.
![](https://main.qcloudimg.com/raw/c9b20e150bd5330feef6d978b8308629.png)

### Installing PHP 
1. Install PHP and its extensions in the CVM instance with `yum`.
```
yum install php php-dom php-dg php-mysql php-pdo -y
```
2. Create an info.php file in the `/var/www/html` directory of the CVM instance to check whether PHP is successfully installed. Below is the sample code:
```
<?php phpinfo(); ?>
```
3. Restart the Apache service.
```
service httpd restart
```
4. Enter `http://115.xxx.xxx.xxx/info.php` in your local browser (where `115.xxx.xxx.xxx` is the public IP of your CVM instance). If the following page appears, PHP has been installed successfully.
![](https://mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)

### Installing the Drupal Service
1. Download the Drupal installation package.
```
wget http://ftp.drupal.org/files/projects/drupal-7.56.zip
```
2. Decompress the package to the root directory of the website.
```
unzip drupal-7.56.zip 
mv drupal-7.56/* /var/www/html/
```
3. Download the translation kit.
```
cd /var/www/html/
wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/7.x/drupal/drupal-7.56.zh-hans.po
```
4. Modify the owner and group to which the `sites` directory belongs.
```
chown -R apache:apache /var/www/html/sites
```
5. Restart the Apache service.
```
service httpd restart
```
6. Enter `http://115.xxx.xxx.xxx/` in your local browser (where `115.xxx.xxx.xxx` is the public IP of your CVM instance) to go to the installation interface of Drupal, select the version to be installed, and click **Save and continue**.
![](https://main.qcloudimg.com/raw/f52af1bb9822ddefc1989df9a0a95e8c.png)
7. Select the language for installation and click **Save and continue**.
8. Set up the database and enter the database information you configured when **installing the MariaDB service**.
9. Enter the site information.
10. Complete the process of Drupal installation.
11. You can access `http://115.xxx.xxx.xxx/` (where `115.xxx.xxx.xxx` is the public IP of your CVM instance) to customize the website.
