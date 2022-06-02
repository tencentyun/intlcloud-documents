
## Connection Methods
You can connect to a TDSQL for MySQL instance in the following ways:
- **Private network connection**: A CVM instance can be used to connect to the private network address of a TDSQL for MySQL instance. This method utilizes the high-speed private network of Tencent Cloud and features low delay.
 - The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region, or both in the classic network.
 - The private network address is provided by TencentDB by default and can be viewed in the instance list or on the instance details page in the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql).
>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over the private network through [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003).
>
- **Public network connection**: If you cannot access the private network, you can connect to your TDSQL for MySQL instance at its public network address. The public network address needs to be [manually enabled](#waiwang). It can be viewed on the instance details page in the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) and can be disabled if no longer needed.
 - Enabling the public network address will expose your database services to the public network, which may lead to database intrusions or attacks. We recommend you use the private network to connect to the database.
 - Public network connection to TencentDB is suitable for development or auxiliary management of databases but not for business access in the production environment, as potentially uncontrollable factors may lead to unavailability of the public network connection, such as DDoS attacks and bursts of high-traffic access.
 - Currently, public network access can be enabled in Guangzhou, Shanghai, Hong Kong (China), Shanghai Finance, Beijing, Shenzhen Finance, and Chengdu regions.

## Prerequisites
### Creating account
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Account Management** tab and click **Create Account**.
![](https://main.qcloudimg.com/raw/148943eb024c9d3871b3c5d509de2e20.png)
3. In the pop-up window, enter the account name, host, password, etc. After confirming that everything is correct, click **Confirm and Go Next**.
The host name is actually the network egress address. If needed, you can enter % to indicate that this instance is accessible to every IP.
4. In the **Modify Permissions** pop-up window, grant permissions as needed and click **Modify**. To discard the changes, click **Cancel Modification**.
The navigation bar on the left provides a graphical interface fully compatible with MySQL management. Permissions can be managed at the column level.
![](https://main.qcloudimg.com/raw/4a6bdfb7e48222945440db418e7f6de1.png)
5. Return to the account list, click **Modify Permissions** to modify user permissions, click **Clone Account** to completely copy the current account permissions to create a new account, or click **More** to reset the password or delete the account.
![](https://main.qcloudimg.com/raw/fe697afd0c76d921ce7961f4c57a9017.png)

### [Enabling public network address (optional)](id:waiwang)
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql), click an instance ID in the instance list to enter the instance details page, and click **Enable** next to **Public Network Address** in the **Basic Info** section.
![](https://main.qcloudimg.com/raw/71a29582f85cbda585ed586341f9b351.png)
2. After successful enablement, you can view the public network address and port number next to **Public Network Address**. TDSQL for MySQL assigns a unique pair of public IP and port to each instance.


After creating an account and obtaining the private/public network address, you can connect to TDSQL for MySQL through third-party tools and program drivers.
- On Windows, connection methods of command line, client, and JDBC driver are taken as examples.
- On Linux, connection method of command line is taken as an example.

## Connecting from Windows Device
### Connecting with Windows command lines
1. Open the Windows command line tool, and enter the following commands under the correct path of mysql.
```
mysql -h private/public network address -P port number -u username  -p
Enter password: **********
```
2. If the following information is displayed, the database is connected successfully, and you can use it.
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
```

### Connecting with Windows client
1. Download a standard SQL client such as MySQL Workbench and SQLyog. SQLyog is taken as an example here.
2. Open SQLyog, select **File** > **New Connection**, enter the host address, port, username, and password, and click **Connect**.
 - **MySQL Host Address**: Enter the private/public network address of the instance obtained earlier.
 - **Username**: Enter the account name created earlier.
 - **Password**: Enter the password of the account. If you forgot the password, reset it in the [console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql).
 - **Port**: Enter the port number of the instance obtained earlier.
3. After the connection is successful, you can perform other operations on the database.


### Connecting with Windows JDBC driver
TDSQL for MySQL supports connecting with program drivers. This document uses Java JDBC Driver for MySQL (Connector/J) as an example.

1. [Download](https://dev.mysql.com/downloads/connector/j/5.0.html) a JDBC jar package from the MySQL official website, and import it to the library referenced in Java.
2. Run the following code to call JDBC:
```
public static final String url = "private/public network address";
public static final String name = "com.mysql.jdbc.Driver"; // Call JDBC
public static final String user = "username";
public static final String password = "password";
//JDBC
Class.forName("com.mysql.jdbc.Driver"); 
Connection conn=DriverManager.getConnection("url, user, password");
//
conn.close();
```
3. After the connection is successful, you can perform other operations on the database.

## Connecting from Linux Device
### Connecting with Linux command lines
This document takes a CVM instance on CentOS 7.2 64-bit as an example. For more information on CVM instance purchase, see [Purchasing Channels](https://intl.cloud.tencent.com/document/product/213/506).
1. Log in to the Linux CVM instance, enter `yum install mysql`, and download and install the MySQL client from Tencent Cloud's image source with CentOS package management software Yum.
![](https://main.qcloudimg.com/raw/fe1470a47fd3311460a7cfd24f70a88a.png)
2. When `complete` is displayed on the command line, the MySQL client is successfully installed.
3. Enter `mysql -h private/public network address -P port -u username -p` to connect to TDSQL for MySQL. Then, you can perform sharding.
Below uses `show databases;` as an example:
![](https://main.qcloudimg.com/raw/c094ba46f8a3d321ad4a199d88d9d3e6.png)

