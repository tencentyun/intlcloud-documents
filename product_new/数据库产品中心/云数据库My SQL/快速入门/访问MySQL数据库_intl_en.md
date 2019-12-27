## Access Methods
TencentDB for MySQL can be accessed in three methods:
- **Private network access**: A CVM instance can be used to access the private network address that is automatically assigned to a TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should reside in the same region, be under the same account, and use the same type of networks (both in the basic network or in the same [VPC](http://intl.cloud.tencent.com/document/product/215/535)).
- **Public network access**: TencentDB for MySQL can be accessed using a public network address.


>- For public network access, the database instance's public IP needs to be enabled, which may expose your database service to attacks or intrusions on the public network. Therefore, it is recommended to log in to the database over the private network. 
>- Public network access to TencentDB is suitable for development or auxiliary management of databases but not for formal business access, as potentially uncontrollable factors may lead to unavailability of the public network access, such as DDoS attacks and bursts of high-traffic access.
- **Peering connection**: For more information on private network access between CVM and TencentDB instances which reside in different regions, are under different accounts, or use different types of networks. For more information on billing, see [Billing Overview of Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000/18833).


## Access to a TencentDB for MySQL Instance
### Enabling the Public Network Access Address (Optional)
>To use the public network access, you need to enable the public network address of your TencentDB instance.
>
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, select the instance to be modified and click the instance name or **Manage** in the "Operation" column to enter the instance details page.
3. Find **Public Network Address** in the basic information section on the instance details page and click **Enable**.
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
4. Click **OK** and the enabling process starts.
![](https://main.qcloudimg.com/raw/b07b27c59f1e6944115148a93baea4a4.png)
5. After the public network address is enabled successfully, it can be found in the basic information.
6. The public network access can be disabled using the switch. When it is enabled again, the public IP corresponding to the domain name remains the same.

### Login on Windows
1. Log in to a Windows-based CVM instance that resides in the same region as the TencentDB for MySQL instance and is accessible.
For more information on how to log in to a CVM instance, see <a href="https://intl.cloud.tencent.com/document/product/213/2764" target="_blank">Getting Started with Windows-based CVM</a> or <a href="https://intl.cloud.tencent.com/document/product/213/2936" target="_blank">Getting Started with Linux-based CVM</a>. Network accessibility means that both the CVM instance and the TencentDB instance are in the basic network or in the same VPC.
1. Download a standard SQL client. MySQL Workbench is recommended for Windows. Visit https://dev.mysql.com/downloads/workbench/ on the CVM instance and download the appropriate installer based on your system version.
![](https://main.qcloudimg.com/raw/f82d66f0470813c6b972a7d0125043e1.png)
2. **Login**, **Sign Up**, and **No, thanks, just start my download.** will appear on the page. Select **No, thanks, just start my download.** to download quickly.
![](https://mc.qcloudimg.com/static/img/7169ce063b1b41c58c48089bc2a61441/image.png)
3. Install MySQL Workbench on this CVM instance. **Microsoft .NET Framework v4.5 and Visual C ++ Redistributable for Visual Studio 2015 are required for the installation.** If needed, you can click "Download Prerequisites" in the MySQL Workbench installation wizard to install them.
![](https://mc.qcloudimg.com/static/img/bcf08cec72e8ea9c490cb30ae79f0da4/image.png)
4. Open MySQL Workbench, select **Database** > **Connect to Database**, enter your TencentDB for MySQL instance's private (or public) network address, username, and password and click **OK** to log in.
 - Hostname: Enter the private (or public) network address which can be viewed on the instance details page in the TencentDB for MySQL Console.
 - Port: Private (or public) network port.
 - Username: The username is "root" by default. For public network access, you are recommended to create a separate account for easier access control.
 - Password: Password of the username.
![](https://main.qcloudimg.com/raw/9c9e5dcc8a2bb9fa15fa4d98a18308f1.png)
5. After successful login, the following page will appear, where you can view the modes and objects of the MySQL database, create tables, and perform operations such as data insertion and query.
![](https://main.qcloudimg.com/raw/8f02e50fcc9c5c8dff33bcd2a83e3522.png)

### Login on Linux 
1. Log in to a Linux-based CVM instance that resides in the same region as the TencentDB for MySQL instance and is accessible.
For more information on how to log in to a CVM instance, see <a href="https://intl.cloud.tencent.com/document/product/213/2764" target="_blank">Getting Started with Windows-based CVM</a> or <a href="https://intl.cloud.tencent.com/document/product/213/2936" target="_blank">Getting Started with Linux-based CVM</a>. Network accessibility means that both the CVM instance and the TencentDB instance are in the basic network or in the same VPC.
In the following example, the CVM instance runs on CentOS 7.2_64. You can use Yum, the package manager built in CentOS, to download and install the MySQL client from the Tencent Cloud image source.
Install the MySQL client by running the following command:
```
yum install mysql
```
If "Complete!" is displayed, it means the MySQL client is installed successfully.
![](https://main.qcloudimg.com/raw/907e047fed90f6cf68752fb386382927.png)
2. Perform the following operations based on the selected access method:
 - For private network access, run the following command to log in to the TencentDB for MySQL instance.
```
mysql -h hostname -u username -p
```
>
>- Replace "hostname" with the private (or public) network address of the target instance, replace "username" with the default username "root", and enter its password when prompted with "Enter password:".
>- If "MySQL [(none)]" is displayed, it means that you have logged in to MySQL successfully.
>
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
 - For public network access, run the following command to log in to the TencentDB for MySQL instance.
```
mysql -h hostname -P port -u username -p
```
>
>
>- Replace "hostname" with the public IP address of the target instance, replace "port" with the public network port, replace "username" with the username for public network access such as "cdb_outerroot", and enter its password when prompted with "Enter password:".
- The username is for public network access. You are recommended to create a separate account for easier access control.
>- In this example, hostname is 59281c4exxx.myqcloud.com and public network port is 15311.
>
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
3. Under the prompt "MySQL \[(none)]>", you can send an SQL statement to the MySQL server for execution. For specific command lines, see [here](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Take `show databases;` for example as below:
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)


