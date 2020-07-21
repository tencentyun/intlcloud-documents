This document describes how to connect to a TDSQL instance in various methods in details.
Two types of connection methods are as follows:
- **Private network access**: a CVM instance can be used to access the private network address of a TencentDB instance. This method relies on the high-speed private network of Tencent Cloud and features low delay.
  - The CVM and TencentDB instances must be under the same account and in the same VPC in the same region, or both in the classic network.
- **Public network access**: if you cannot connect to the private network, you can access your TDSQL instance over a public network address.
  - Enabling the public network address will expose your database services to the public network, which may lead to database intrusions or attacks. We recommend that you use the private network to access the database.
  - Public network access to TencentDB is suitable for development or auxiliary database management but not for actual business access, because uncontrollable factors may cause public network access to be unavailable, such as DDoS attacks and sudden surges in access traffic.


## Preparations
### Creating an account
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select the **Manage Account** tab and click **Create**.
![](https://main.qcloudimg.com/raw/148943eb024c9d3871b3c5d509de2e20.png)
3. In the pop-up dialog box, enter the account name, host, password, and remarks. After confirming that everything is correct, click **OK**.
The host name is actually the network egress address. If needed, you can enter % to indicate that every IP can be accessible.
4. In the permission modification dialog box, after assigning permissions based on needs, click **Save Settings** to complete the permission assignment. If you need to set permissions later, click "Set Later".
The navigation bar on the left provides a graphical interface fully compatible with MySQL management. Permissions can be managed at the column level.
![](https://main.qcloudimg.com/raw/4a6bdfb7e48222945440db418e7f6de1.png)
5. Return to the account list, click **Modify Permissions** to modify user permissions, click "Clone Account" to completely copy the current account permissions to create a new account. Click **More** to reset the password and delete the account.
![](https://main.qcloudimg.com/raw/f72d3815f500b0c5a4e7e8d699ec793f.png)

### Obtaining the public network address
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), click an instance name to enter the instance details page. In the "Public address" section on the basic info tab, click **Enable**.
![](https://main.qcloudimg.com/raw/71a29582f85cbda585ed586341f9b351.png)
2. After this, the public network address and port number can be obtained. TDSQL provides a unique IP and port for access and use.

## Connection Steps
After creating an account and obtaining its public/private network address, you can connect to TDSQL through third-party tools and program drivers.
- On Windows, connection methods of command line, client, and JDBC driver are taken as examples.
- On Linux, connection method of command line is taken as an example.

### Windows command line connection
1. Open the Windows command line tool, and enter the following commands under the correct path of mysql.
```
mysql -h public network address -P port number -u user name  -p
Enter password: **********
```
2. After the relevant code is entered correctly, the following information will be displayed. After the database is connected successfully, you can operate the database in the next step.
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
```
		
### Windows client connection
1. Download a standard SQL client such as MySQL Workbench and SQLyog. Here we take SQLyog as an example.
2. Open SQLyog, select **File** > **New Connection**, enter CVM address, port, user name and password, and click **Connect**.
 - My SQL CVM address: enter the public network address obtained earlier.
 - Username: enter the name of the account created earlier.
 - Password: enter the account password.
 - Port: enter the port corresponding to the public network address.

### Windows JDBC driver connection
TDSQL supports connecting via program drivers. This document uses Java JDBC Driver for MySQL (Connector/J) as an example to describe how to connect to TDSQL.

1. First [download](https://dev.mysql.com/downloads/connector/j/5.0.html) a JDBC jar package from the MySQL official website, and import it to the library referenced in JAVA.
2. Run the following code to call JDBC:
```
		public static final String url = "Public network address";
		public static final String name = "com.mysql.jdbc.Driver"; // Call JDBC
		public static final String user = "username";
		public static final String password = "password";
		//JDBC
		Class.forName("com.mysql.jdbc.Driver"); 
				Connection conn=DriverManager.getConnection("url, user, password");
		//
		conn.close();
```
3. After the connection is successful, you can perform other operations on the database in the next step.
>?Because TDSQL needs to mark the shardkey when sharding and inserting data, these operations cannot be called with JDBC.

### Linux command line connection
This document takes CentOS 7.2 64-bit on a CVM instance as an example. For more information on CVM instance purchase, please see [Purchasing Channels](https://intl.cloud.tencent.com/document/product/213/506).
1. Log in to Linux, enter the `yum install mysql` command, and download and install MySQL client in Tencent Cloud's image source with CentOS's own package management software Yum.
![](https://main.qcloudimg.com/raw/fe1470a47fd3311460a7cfd24f70a88a.png)
2. When `complete` is displayed on the command line, the MySQL client is successfully installed.
3. Enter the command `mysql -h public network address -P port -u username -p` to connect to TDSQL. Then, you can perform sharding.
Below uses `show databases;` as an example:
![](https://main.qcloudimg.com/raw/c094ba46f8a3d321ad4a199d88d9d3e6.png)

