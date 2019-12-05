## Preparations
### Creating an account
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), select the desired instance, and click the instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select the **Manage Account** tab and click **Create Account**.
![](https://main.qcloudimg.com/raw/148943eb024c9d3871b3c5d509de2e20.png)
3. In the pop-up dialog box, enter the account name, host, password, and remarks and click **OK** after confirming that everything is correct.
The host name is actually the network egress address. If needed, you can enter % to indicate that every IP can be accessible.
![](https://main.qcloudimg.com/raw/9eed6bea2c606347767f6821e3dc2eb5.png)
4. In the permission modification dialog box, after granting permissions as needed, click "Save Settings" to complete the permission granting. If you want to set permissions later, click "Set Later".
The navigation bar on the left provides a graphical interface fully compatible with MySQL management. Permissions can be managed at the column level.
![](https://main.qcloudimg.com/raw/4a6bdfb7e48222945440db418e7f6de1.png)
5. Return to the account list. Click **Modify Permission** to modify the user permissions, click **Clone Account** to completely copy the current account permissions and create a new account, or click **More** to reset the password or delete the account.
![](https://main.qcloudimg.com/raw/f72d3815f500b0c5a4e7e8d699ec793f.png)

### Obtaining the public network address
1. Enter the instance details page and click **Enable** in the public network address bar in the basic info section.
![](https://main.qcloudimg.com/raw/71a29582f85cbda585ed586341f9b351.png)
2. After this, the public network address and port number can be obtained. TDSQL provides a unique IP and port for access and use.

## Connection Steps
After creating an account and obtaining its public network address, you can connect to TDSQL through third-party tools and program drivers.
- On Windows, connection methods of command line, client, and JDBC driver are taken as examples.
- On Linux, connection method of command line is taken as an example.

### Connecting via Windows command line
1. Open the Windows command line and enter the following command in the correct path to MySQL.
```
mysql -h public network address -P port number -u username  -p
Enter password: **********
```
2. After the relevant code is entered correctly, the following message will be displayed, indicating that the database is successfully connected to. Then, you can perform operations on the database.
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
```
		
### Connecting via Windows client
1. Download a standard SQL client such as MySQL Workbench and SQLyog. SQLyog is taken as an example here.
2. Open SQLyog, select **File** > **New Connection**, enter the corresponding host address, port, username, and password, and click **Connect**.
 - MySQL host address: Enter the public network address obtained earlier.
 - Username: Enter the name of the account created earlier.
 - Password: Enter the account password.
 - Port: Enter the port corresponding to the public network address.
![](https://main.qcloudimg.com/raw/56645ca6d1c5fe7803e05f7643b833ae.png)
3. The following screen will appear after successful connection, where you can perform operations on the database.
![](https://main.qcloudimg.com/raw/1f492c179e2f604afc02a775d58a2d9c.png)

### Connecting via Windows JDBC driver
TDSQL supports connecting via program drivers. This document uses Java JDBC Driver for MySQL (Connector/J) as an example to describe how to connect to TDSQL.

1. Download the .jar package of JDBC from [MySQL's official website](https://dev.mysql.com/downloads/connector/j/5.0.html) and import it into the library referenced by Java.
2. The code to call JDBC is as follows:
```
		public static final String url = "public network address";
		public static final String name = "com.mysql.jdbc.Driver"; // Called JDBC successfully
		public static final String user = "username";
		public static final String password = "password";
		//JDBC
		Class.forName("com.mysql.jdbc.Driver"); 
				Connection conn=DriverManager.getConnection("url, user, password");
		//
		conn.close();
```
3. After successful connection, you can perform operations on the database.
>Because TDSQL needs to mark the shardkey when sharding and inserting data, these operations cannot be called with JDBC.

### Connecting via Linux command line
This document takes CentOS 7.2 64-bit on a CVM instance as an example. For CVM instance purchase, see [Purchase Method](https://intl.cloud.tencent.com/document/product/213/506).
1. Log in to Linux and enter the command `yum install mysql` to download and install a MySQL client from a Tencent Cloud image source with Yum, CentOS' built-in package manager.
![](https://main.qcloudimg.com/raw/fe1470a47fd3311460a7cfd24f70a88a.png)
2. When `complete` is displayed on the command line, the MySQL client is successfully installed.
3. Enter the command `mysql -h public network address -P port -u username -p` to connect to TDSQL. Then, you can perform sharding.
`show databases;` is taken as an example below:
![](https://main.qcloudimg.com/raw/c094ba46f8a3d321ad4a199d88d9d3e6.png)

