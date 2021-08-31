## Scenario
Drupal is a free and open-source content management framework written in PHP and distributed under the GNU General Public License. Drupal provides a back-end framework for at least 2.3% of all websites worldwide – ranging from personal blogs to corporate sites. This article describes how to setup Drupal manually on a CVM. 

To manually setup a Drupal-based personal website, you need to be familiar with Linux commands, such as [using YUM to install software on CentOS](https://intl.cloud.tencent.com/document/product/213/2046). You should also be familiar with software usage and compatibility.

## Software
This article describes how to install the following software
- Linux operating system. This article uses CentOS 7.6.
- Apache is a web server software. This article uses Apache 2.4.6.
- MariaDB is a database management system. This article uses MariaDB 10.4.8.
- PHP is a scripting language. This article uses PHP 7.0.33.
- Drupal is a content management framework. This article uses Drupal 8.1.1.


## Prerequisites
You need a Linux CVM. If you have not purchased one yet, see [this article](http://intl.cloud.tencent.com/document/product/213/2936) for information on how to get started with a Linux CVM.


## Directions
### Step 1 Logging in to a Linux instance
[Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Step 2 Setting up LAMP
After logging in, set up LAMP so you can run Drupal. Refer to [this article](https://intl.cloud.tencent.com/document/product/213/34813) for details.

### Step 3 Downloading and installing Drupal
1. Run the following commands to download the Drupal install package to the root directory of your website.
```
cd /var/www/html/
```
```
wget wget http://ftp.drupal.org/files/projects/drupal-8.1.1.zip
```
2. Run the following commands to decompress the install package and rename the directory.
```
unzip drupal-8.1.1.zip 
```
```
mv drupal-8.1.1/ drupal/
```

### Step 4 Configuring Drupal 
1. Run the following command to open the Apache configuration file.
```
vi /etc/httpd/conf/httpd.conf
```
2. Press **i** to enter edit mode. Find `AllowOverride None` in `Directory "/var/www/html"></Directory>` and replace it with the following:
```
AllowOverride All
```
The result is shown below:
![](https://main.qcloudimg.com/raw/c68f918f22d9c29607d59fe1847eff69.png)
3. Press **Esc** to exit edit mode and enter **:wq** to save the file and return.
4. Run the following command to change the access permission of the root directory of the website for the user `apache`.
```
chown -R apache:apache /var/www/html
```
5. Run the following command to reboot Apache service.
```
systemctl restart httpd
```

#### Configure a database for Drupal<span id="database"></span>
>Instructions for configuring MariaDB user credentials may vary depending on different versions. Consult [official MariaDB website](https://downloads.mariadb.org/) for details.
>
1. Run the following command to enter MariaDB.
```
mysql
```
2. Run the following command to create a database named `drupal`.
```
CREATE DATABASE drupal;
```
3. Run the following command to create a new user `user` and set its password to `123456`.
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Run the following command and grand `user` all privileges to `drupal`.
```
GRANT ALL PRIVILEGES ON drupal.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Run the following command to apply all configurations.
```
FLUSH PRIVILEGES;
```
6. Run the following command to exit MariaDB.
```
\q
```

#### Configure `root`
1.  Run the following command to enter MariaDB.
```
mysql
```
2. Run the following command to set a password for `root`.
>MariaDB 10.4 for CentOS now allows `root` account to log in without password. Run the following command to set a password for `root` and record it in a secure location.
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('your_pasword');
```
3. Run the following command to exit MariaDB.
```
\q
```

### Step 5 Installing and configuring Drupal
1. Open a browser window on your local machine and visit the following address to install Drupal.
```
http://CVM_Public_IP/drupal
```
2. Select the language of your preference and click **Save and continue**
3. Select **Standard installation** and click **Save and continue**
4. Input relevant database information configured in [Configuring a database for Drupal](#database). Click **Save and continue**
>Drupal installation now checks to see if all installation criteria are met. If so, installation starts. If not, error messages appear. Resolve them before continuing.
>

5. The configuration page loads automatically after installation is completed. Input information and click **Save and continue**
>Record your maintenance username and password.
>

6. The homepage of your Drupal loads automatically. Use the maintenance username and password to log in
You have now successfully set up your Drupal website. Customize your experience as you see fit.

## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting based on your actual situation.
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).
