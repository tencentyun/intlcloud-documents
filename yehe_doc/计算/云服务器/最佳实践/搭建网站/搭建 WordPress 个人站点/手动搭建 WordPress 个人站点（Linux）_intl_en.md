## Overview
WordPress is a blog platform developed using PHP. This document describes how to manually build WordPress on a CentOS 7.6 Tencent Cloud CVM.

To build WordPress, you must be familiar with common Linux commands, such as [Installing Software via YUM (CentOS)](https://intl.cloud.tencent.com/document/product/213/2046) and know how to use the software involved and their version compatibility.

<dx-alert infotype="notice" title="">
It's recommended that you can configure a personal blog by using a Tencent Cloud marketplace image. It may take a long time to set up WordPress manually.
</dx-alert>



## Software
The following software is involved in building WordPress:
- Linux: Linux operating system. This document uses CentOS 7.6 as an example.
- Nginx: web server. This document uses Nginx 1.17.5 as an example.
- MariaDB: database. This document uses MariaDB 10.4.8 as an example.
- PHP: scripting language. This document uses PHP 7.2.22 as an example.
- WordPress: blog platform. This document uses WordPress 5.0.4 as an example.

## Directions 
### Step 1. Logging in to the CVM
[Log in to Linux instance (Web Shell)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use any of the following login methods you are comfortable with:
- [Logging in to Linux Instances (Remote Login)](https://intl.cloud.tencent.com/document/product/213/32502)
- [Logging in to Linux Instance (SSH Key)](https://intl.cloud.tencent.com/document/product/213/32501)



### Step 2: Manually building the LNMP environment
LNMP, an acronym for Linux, Nginx, MariaDB, and PHP, is one of the most common runtime environments for web servers. After you create and log in to a CVM instance, you can build the LNMP environment by referring to [Manual Setup of LNMP (CentOS 7)](https://intl.cloud.tencent.com/document/product/213/32733).


### Step 3: Configuring the database[](id:database)


<dx-alert infotype="notice" title="">
The user authentication method varies depending on the MariaDB version. For details, visit the MariaDB official website.
</dx-alert>


1. Run the following command to enter MariaDB:
```shellsession
mysql
```
2. Run the following command to create a MariaDB database, named `wordpress` in this example:
```shellsession
CREATE DATABASE wordpress;
```
3. Run the following command to create a user, `user` with the password `123456` in this example:
```shellsession
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Run the following command to grant `user` all permissions to the `wordpress` database:
```shellsession
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Run the following command to set a password for `root`.
<dx-alert infotype="explain" title="">
MariaDB 10.4 for CentOS allows the `root` account to log in without a password. Run the following command to set a password for `root` and record it so you can remember it.
</dx-alert>
```shellsession
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('Enter your password');
```
6. Run the following command to apply all configurations.
```shellsession
FLUSH PRIVILEGES;
```
7. Run the following command to exit MariaDB.
```shellsession
\q
```


### Step 4: Installing and configuring WordPress
#### Downloading WordPress


<dx-alert infotype="explain" title="">
You can download the latest WordPress version from the official WordPress website.
</dx-alert>


1. Run the following command to delete the `index.php` file that is used to test PHP-Nginx configuration from the root directory of the website:
```shellsession
rm -rf /usr/share/nginx/html/index.php
```
2. Run the following commands to navigate to the `/usr/share/nginx/html/` directory and download and decompress the WordPress installation package:
```shellsession
cd /usr/share/nginx/html
```
```shellsession
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
```
```shellsession
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


#### Modifying the WordPress configuration file
1. Run the following commands to navigate to the WordPress installation directory, copy the content in the `wp-config-sample.php` file to the `wp-config.php` file, and save the original configuration file for backup:
```shellsession
cd /usr/share/nginx/html/wordpress
```
```shellsession
cp wp-config-sample.php wp-config.php
```
2. Run the following command to open and edit the new configuration file:
```shellsession
vim wp-config.php
```
3. Press **i** to enter the editing mode. Find the MySQL part in the file and change related configuration to content in [Configuring the WordPress database](#database).
```shellsession
	// ** MySQL settings - You can get this info from your web host ** //
	/** The name of the database for WordPress */
	define('DB_NAME', 'wordpress');
	
	/** MySQL database username */
	define('DB_USER', 'user');
	
	/** MySQL database password */
	define('DB_PASSWORD', '123456');
	
	/** MySQL hostname */
	define('DB_HOST', 'localhost');
```
4. After the modification is complete, press **Esc** and enter **:wq** to save the file and go back.

### Step 5: Verifying WordPress installation
1. In the address box of the browser, type `http://domain name or the public IP address of the CVM instance/wordpress folder`, for example:
```shellsession
http://192.xxx.xxx.xx/wordpress
```
Press **Enter** to switch to the WordPress installation page and configure WordPress.
2. Enter the installation information as described in the following table based on the WordPress installation wizard and click **Install WordPress**.
<table>
	<th style="width: 18%;">Required Information</th>
	<th style="width: 25%;">Description</th>
					<tr>
					<td>
							Website title
					</td>
					<td>
							WordPress website name
					</td>
			</tr>
				<tr>
					<td>
							User Name
					</td>
					<td>
							WordPress administrator name. For security purposes, use a name other than admin because admin can be easily cracked.
					</td>
			</tr>
			<tr>
					<td>
							Password
					</td>
					<td>
							Use the default strong password or a custom password. Do not use existing passwords and ensure that the password is saved in a secure place.
					</td>
			</tr>
				<tr>
					<td>
							Email address
					</td>
					<td>
							Email address used to receive notifications
					</td>
			</tr>
	</table>
Now, you can log in to your WordPress website and post blogs.

## Related Operations
You can set a domain name for your WordPress website. In this way, users can use the domain name instead of a complex IP address to visit your website. If you build a website just to learn the process, you can use an IP address. However, this method is not recommended.


## FAQs
If you encounter a problem when using CVM, refer to the following documents for troubleshooting:
- CVM login: [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- CVM network: [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- CVM disks: [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).



