## Use Case
WordPress is a blog platform written in PHP. This article describes how to install WordPress on CentOS 7.6.

To set up WordPress, you should be familiar with common Linux commands, such as [Installing Software via YUM in CentOS](https://intl.cloud.tencent.com/document/product/213/2046) and know how to use the software involved and their version compatibility.

## Software
These are the software involved:
- Operating system: CentOS 7.6, a distribution of Linux
- Web server: Nginx 1.17.5
- Database: MariaDB 10.4.8
- Hypertext processor: PHP 7.2.22
- Blog platform: WordPress 5.0.4

## Procedure 
### Step 1: Logging in to Linux CVM
[Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use another login method that you are comfortable with.
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux Instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)



### Step 2: Setting up LNMP manually
LNMP is a common web service architecture. The name is an acronym of its components: Linux, Nginx, MariaDB, and PHP. Refer to [Manually Building an LNMP Environment (CentOS 7)](https://intl.cloud.tencent.com/document/product/213/32733) for instructions.


### Step 3: Creating a database for WordPress<span id="database"></span>
>User authentication methods may vary according to different MariaDB versions. For more information, refer to the MariaDB official site.
>
1. Run the following command to enter MariaDB.
```
mysql
```
2. Run the following command to create a database named `wordpress`.
```
create database wordpress;
```
3. Run the following command to create a new user named `user` and set its password to `123456`.
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Run the following command to grant `user` all permissions to `wordpress`.
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Run the following command to apply all configurations.
```
FLUSH PRIVILEGES;
```
6. Run the following command to exit MariaDB.
```
\q
```

### Step 4: Set up `root` account
1. Run the following command to enter MariaDB.
```
mysql
```
2. Run the following command to set a password for `root`.
>MariaDB 10.4 for CentOS now allows `root` to log in without a password. Run the following command to set a password for `root` and record it in a secure location.
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('your_pasword');
```
3. Run the following command to exit MariaDB.
```
\q
```


### Step 5: Installing and configuring WordPress
#### Downloading WordPress
> You can download the latest version of WordPress from the official WordPress website.
>
1. Run the following command to delete `index.php`. This is used to test PHP-Nginx setup.
```
rm -rf /usr/share/nginx/html/index.php
```
2. Run the following commands to navigate to `/usr/share/nginx/html/` and download and decompress the installation package.
```
cd /usr/share/nginx/html
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


#### Modifying the WordPress configuration file
1. Run the following commands to navigate to the WordPress installation directory and copy and rename `wp-config-sample.php` to `wp-config.php`. Save the original file for backup.
```
cd /usr/share/nginx/html/wordpress
cp wp-config-sample.php wp-config.php
```
2. Run the following command to open the new configuration file.
```
vim wp-config.php
```
3. Press **i** to enter edit mode. Find the following content and make necessary changes according to [Configuring WordPress database](#database).
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
4. Press **Esc** and enter **:wq** to save the file and exit Vim.

### Step 6: Verifying the WordPress Configuration
1. Open a browser window and enter the following to start the process.
```
http://your_CVM_public_IP/wordpress
```
You are redirected to the installation page.
2. Input information as prompted. Click **Install WordPress** to complete the process.
<table>
	<th style="width: 18%;">Item</th>
	<th style="width: 100px;">Description</th>
					<tr>
					<td>
							Site title
					</td>
					<td>
							Name of your WordPress site.
					</td>
			</tr>
				<tr>
					<td>
							Username
					</td>
					<td>
							Account name of the WordPress administrator. For security reasons, use a name other than `admin`.</td></tr>
					</td>
			</tr>
			<tr>
					<td>
							Password
					</td>
					<td>
							Use the default password or set a new one. Use a strong password and do not reuse existing ones. Keep your password safe.
					</td>
			</tr>
				<tr>
					<td>
							Your email address
					</td>
					<td>
							Email address used to receive notifications.
					</td>
			</tr>
	</table>
Now, you can log in to your WordPress and publish blogs.

## Using a Domain Name
Use a domain name that makes your website easier to remember. We recommend you obtain a domain name and set it to point to your WordPress site. If you are installing WordPress just to learn the process, you can skip this step.

## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting.
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).

