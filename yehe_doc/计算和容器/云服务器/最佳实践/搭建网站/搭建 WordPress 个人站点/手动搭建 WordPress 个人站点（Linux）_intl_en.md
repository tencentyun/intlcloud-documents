## Scenario
WordPress is a blog platform developed in PHP. This document describes how to manually build a private WordPress site on a Tencent Cloud CVM with CentOS 7.6.

To build a WordPress site, you must be familiar with common Linux commands, such as those for [installing software through YUM in the CentOS environment](https://intl.cloud.tencent.com/document/product/213/2046). In addition, you need to know how to use the involved software programs and their version compatibility details.

## Software
The following software programs are used to build the WordPress site:
- Linux: Linux operating system. This document uses CentOS 7.6 as an example.
- Nginx: web server. This document uses Nginx 1.17.5 as an example.
- MariaDB: database. This document uses MariaDB 10.4.8 as an example.
- PHP: scripting language. This document uses PHP 7.2.22 as an example.
- WordPress: blog platform. This document uses WordPress 5.0.4 as an example.

## Directions 
### Step 1: Log in to the CVM
[Log in to a Linux instance by using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use either of the following login methods that you are comfortable with.
- [Logging into a Linux Instance by Using Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
- [Logging into a Linux Instance by Using the SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)



### Step 2: Manually build an LNMP environment
LNMP is the acronym for Linux, Nginx, MariaDB, and PHP. It is one of the most common runtime environments for web servers. After creating and logging in to a CVM instance, you can build an LNMP environment by referring to [Manually Building an LNMP Environment (CentOS 7)](https://intl.cloud.tencent.com/document/product/213/32733).

<span id="database"></span>
### Step 3: Configure the WordPress database
>The user authentication method varies depending on the MariaDB version. For details, visit the MariaDB official website.
>
1. Run the following command to enter MariaDB:
```
mysql
```
2. Run the following command to create a MariaDB database, such as `wordpress` in this example:
```
CREATE DATABASE wordpress;
```
3. Run the following command to create a user and specify a password, such as the `user` user with the password `123456` in this example:
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Run the following command to grant `user` all permissions to the `wordpress` database:
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Run the following command for all configurations to take effect:
```
FLUSH PRIVILEGES;
```
6. Run the following command to exit MariaDB:
```
\q
```

### Step 4: Configure a `root` account
1. Run the following command to enter MariaDB:
```
mysql
```
2. Run the following command to set a password for `root`:
> MariaDB 10.4 for CentOS allows the `root` account to log in without a password. Run the following command to set a password for `root` and save it in a safe place:
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('Enter your password');
```
3. Run the following command to exit MariaDB:
```
\q
```


### Step 5: Install and configure WordPress
#### Downloading WordPress
> You can download the latest version of WordPress from the official WordPress website.
>
1. Run the following command to delete the `index.php` file that is used to test PHP-Nginx configuration from the root directory of the website:
```
rm -rf /usr/share/nginx/html/index.php
```
2. Run the following commands to navigate to the `/usr/share/nginx/html/` directory and download and decompress the WordPress installation package:
```
cd /usr/share/nginx/html
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


#### Modifying the WordPress configuration file
1. Run the following commands to navigate to the WordPress installation directory, copy the content of the `wp-config-sample.php` file to the `wp-config.php` file, and save the original configuration file for backup:
```
cd /usr/share/nginx/html/wordpress
cp wp-config-sample.php wp-config.php
```
2. Run the following command to open and edit the new configuration file:
```
vim wp-config.php
```
3. Press **i** to enter the editing mode. Find the MySQL section in the file and modify the settings as described in [Configuring the WordPress database](#database).
```
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
4. After finishing the modification, press **Esc** and enter **:wq**. Then, save the changes and close the file.

### Step 6: Verify WordPress installation
1. In the address box of the browser, enter `http://<Domain name or public IP address of the CVM instance>/<WordPress folder>`, for example:
```
http://192.xxx.xxx.xx/wordpress
```
Press **Enter** to go to the WordPress installation page and configure WordPress.

2. Complete the following installation information as instructed in the WordPress installation wizard. Then, click **Install WordPress**.
<table>
	<th style="width: 18%;">Required information</th>
	<th style="width: 25%;">Description</th>
					<tr>
					<td>
							Site title
					</td>
					<td>
							WordPress site name
					</td>
			</tr>
				<tr>
					<td>
							Username
					</td>
					<td>
							WordPress administrator name. For security purposes, use a name other than admin, which is prone to be cracked.
					</td>
			</tr>
			<tr>
					<td>
							Password
					</td>
					<td>
							Use the default strong password or a custom password. Do not use previous passwords and save the password in a secure place.
					</td>
			</tr>
				<tr>
					<td>
							Email address
					</td>
					<td>
							Email address for receiving notifications
					</td>
			</tr>
	</table>
Now, you can log in to your WordPress site and post blogs.

## Relevant Operations
You can set a domain name for your WordPress site. In this way, users can use the domain name instead of a complex IP address to visit your site. If you are building the site for learning purposes, you can set an IP address for the site. However, this practice is not recommended for other cases.

## FAQs
If you encounter issues when using a CVM, refer to the following documents for troubleshooting based on your actual situation.
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).

