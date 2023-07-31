LAMP (Linux + Apache + MySQL/MariaDB + Perl/PHP/Python) is a set of open-source software programs often used to set up dynamic websites or servers. These independent programs are usually used together and increasingly compatible with one another to form a powerful web application platform.
This tutorial guides you through the following process: starting a TencentDB instance and configuring a LAMP application with a CVM instance to connect to the highly available environment of the TencentDB instance.
The database can be separated from the environment lifecycle after you run the TencentDB instance. This allows you to connect the same database from multiple servers for simplified database operation and maintenance, so that you no longer need to worry about database installation, deployment, version update, and troubleshooting, etc.

>The TencentDB and CVM instances used in the tutorial reside in the same region. If this is not the case, see [Connecting to MySQL Instance](https://www.tencentcloud.com/document/product/236/37788)

### Initializing the TencentDB Instance
For more information on how to purchase and initialize TencentDB instances, see [Purchase Methods](https://intl.cloud.tencent.com/document/product/236/5160) and [Creating MySQL Instance](https://www.tencentcloud.com/document/product/236/37785).

### Logging in to the CVM Instance
For more information on how to purchase and access CVM instances, see [Getting Started with Linux-based CVM](http://intl.cloud.tencent.com/document/product/213/2936). CentOS is used in this tutorial.

### Installing the MySQL Client
1. Install the MySQL client to the CVM instance with `yum`.
```
yum install mysql -y
```
![](https://mc.qcloudimg.com/static/img/8b952d6d7d767413a6558e82df092d44/image.png)
2. Connect to the TencentDB instance after the installation is completed.
```
mysql -h hostname -u username -p
```
![](https://mc.qcloudimg.com/static/img/297856a53959582220b9bba6f06ce9f6/image.png)
Here, "hostname" is the private IP of the TencentDB instance and "username" is the username of your database.
3. After the connection is successful, you can close the instance and proceed to the next step.
```
quit;
```

### Installing the Apache Service
1. Install Apache in the CVM instance with `yum`.
```
yum install httpd -y
```
![](https://mc.qcloudimg.com/static/img/dc142f813e8e8474a5994e2e841828f2/image.png)
2. Start the Apache service.
```
service httpd start
```
3. Test Apache.
>In this step, you should configure an inbound rule with the source being **all** and the port protocol being **TCP:80** in the security group of your CVM instance. For more information on how to configure the security group, see [Security Group](http://intl.cloud.tencent.com/document/product/213/12452).
>
Enter `http://xxx.xxx.xxx.xxx/` in your local browser (where `xxx.xxx.xxx.xxx` is the public IP of your CVM instance). If the following page appears, Apahce has started successfully.
![](https://main.qcloudimg.com/raw/80941070a1a309ba484527473c915221.png)

### Installing PHP 
1. Install PHP in the CVM instance with `yum`.
```
yum install php -y
```
![](https://mc.qcloudimg.com/static/img/61a0864ddbb70e65c63ad5093e8165d4/image.png)

### Creating a Project to Test the LAMP Environment
1. Create an info.php file in the `/var/www/html` directory of the CVM instance. Below is the sample code:
```
<?php phpinfo(); ?>
```
2. Restart the Apache service.
```
service httpd restart
```
3. Enter `http://xxx.xxx.xxx.xxx/info.php` in your local browser (where `xxx.xxx.xxx.xxx` is the public IP of your CVM instance). If the following page appears, the LAMP service has been deployed successfully.
![](https://mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)
