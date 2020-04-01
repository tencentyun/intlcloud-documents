TencentDB for MySQL can be accessed in the following ways:
- **Private network access**: a CVM instance can be used to access the private network address that is automatically assigned to a TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account and reside in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or reside in the basic network.
>CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over the private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).
- **Public network access**: TencentDB for MySQL can be accessed using a public network address.
>
>- For public network access, the database instance's public IP needs to be enabled, which may expose your database service to attacks or intrusions on the public network. Therefore, it is recommended to log in to the database over the private network. 
>- Public network access to TencentDB is suitable for development or auxiliary management of databases but not for formal business access, as potentially uncontrollable factors may lead to unavailability of the public network access, such as DDoS attacks and bursts of high-traffic access.
>- Public network access can only be enabled for instances in Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Seoul, Tokyo, and Silicon Valley regions.


The following describes how to log in to a TencentDB for MySQL instance from Windows and Linux CVM instance over the private and public networks.
## Accessing from Windows CVM
1. Log in to a Windows CVM instance. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Configuring Windows CVM</a>.
2. Download a standard SQL client.
>MySQL Workbench is recommended. Visit https://dev.mysql.com/downloads/workbench/ and download an appropriate installer based on your system version.
>
![](https://main.qcloudimg.com/raw/25e78e6614b2967e8c70140b8849a6d6.png)
3. **Login**, **Sign Up**, and **No, thanks, just start my download.** will appear on the page. Select **No, thanks, just start my download.** to download quickly.
![](https://main.qcloudimg.com/raw/f98f84df777a8f8927bec3375781f517.png)
4. Install MySQL Workbench on this CVM instance.
>
>- Microsoft .NET Framework 4.5 and Visual C ++ Redistributable for Visual Studio 2015 are required for the installation.
>- If needed, you can click "Download Prerequisites" in the MySQL Workbench installation wizard to enter the corresponding page to download and install them. Then, install MySQL Workbench.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. Open MySQL Workbench, select **Database** > **Connect to Database**, enter your TencentDB for MySQL instance's private (or public) network address, username, and password and click **OK** to log in.
 - Hostname: enter the private (or public) network address which can be viewed together with the ports on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). For the public network address, please check whether it has been enabled as instructed in [Enabling Public Network Address](#waiwang).
 - Port: private (or public) network port.
 - Username: the username is "root" by default. For public network access, you are recommended to [create a separate account](https://intl.cloud.tencent.com/document/product/236/31900) for easier access control.
 - Password: the password corresponding to `Username`. If you forgot the password, please reset it as instructed in [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
![](https://main.qcloudimg.com/raw/8f2aeea985388e545ccf5da8fec908b7.png)
6. After successful login, the following page will appear, where you can view the modes and objects of the MySQL database, create tables, and perform operations such as data insertion and query.
![](https://main.qcloudimg.com/raw/9ec2f9393a3652727acbb8dfc41ad5b7.png)

## Accessing from Linux CVM
1. Log in to a Linux CVM instance. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/10517" target="_blank">Configuring Linux CVM</a>.
2. Taking a CVM instance on CentOS 7.2 64-bit as an example, install the MySQL client by running the following command:
```
yum install mysql
```
If `Complete!` is displayed, it means the MySQL client is installed successfully.
![](https://main.qcloudimg.com/raw/907e047fed90f6cf68752fb386382927.png)
3. Perform the corresponding operation based on the access method:
 - **Private network access:**
    1. Run the following command to log in to the TencentDB for MySQL instance.
```
mysql -h hostname -u username -p
```
      - hostname: replace it with the private network address of the target TencentDB for MySQL instance, which can be viewed on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
		- username: replace it with the default username `root`.
    2. Enter the password corresponding to the `root` account of the TencentDB for MySQL instance after the prompt `Enter password:` is displayed. If you forgot the password, please reset it as instructed in [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
    If `MySQL [(none)]>` is displayed, it means that you have logged in to MySQL successfully.
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **Public network access:**
    1. Run the following command to log in to the TencentDB for MySQL instance.
```
mysql -h hostname -P port -u username -p
```
      - hostname: replace it with the public network address of the target TencentDB for MySQL instance, which can be viewed together with the port on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). If the public network address has not been enabled, please enable it as instructed in [Enabling Public Network Address](#waiwang).
      - port: replace it with the public network port number.
      - username: replace it with the public network access username for public network access. You are recommended to [create a separate account](https://intl.cloud.tencent.com/document/product/236/31900) for easier access control.
    2. Enter the password corresponding to the public network access username after the prompt `Enter password:` is displayed. If you forgot the password, please reset it as instructed in [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
    In this example, `hostname` is 59281c4exxx.myqcloud.com and public network port is 15311.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. Under the prompt `MySQL \[(none)]>`, you can send an SQL statement to the MySQL server for execution. For specific command lines, please see [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Take `show databases;` for example as below:
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)



<span id = "waiwang"></span>
## Appendix. Enabling Public Network Access
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance details page.
3. Find **Public Network Address** in the basic information section on the instance details page and click **Enable**.
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
4. Click **OK** and the enabling process starts.
5. After the public network address is enabled successfully, it can be found in the basic info.
6. The public network access can be disabled using the switch. When it is enabled again, the public IP corresponding to the domain name remains the same.
