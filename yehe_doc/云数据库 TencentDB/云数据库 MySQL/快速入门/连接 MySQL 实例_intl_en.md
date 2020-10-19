TencentDB for MySQL can be connected to in the following two methods:

- **Private network connection**: a CVM instance can be used to connect to the private network address of a TencentDB instance. This method relies on the high-speed private network of Tencent Cloud and features low delay.
 - The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region, or both in the classic network.
 - The private network address is provided by the system by default and can be viewed in the instance list or on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).

- **Public network connection**: if you cannot access the private network, you can connect to your TencentDB for MySQL instance at its public network address. The public network address needs to be [manually enabled](#waiwang). It can be viewed on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and can be disabled if no longer needed.
 - The public network address can be enabled only for instances in the Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Seoul, Tokyo, and Silicon Valley regions.
 - Enabling the public network address will expose your database services to the public network, which may lead to database intrusions or attacks. We recommend you use the private network to connect to the database. 
 - Public network connection to TencentDB is suitable for development or auxiliary database management but not for actual business connection, because uncontrollable factors may cause public network connection to be unavailable, such as DDoS attacks and sudden surges in access traffic.


The following describes how to log in to a TencentDB for MySQL instance from Windows and Linux CVM instance over the private and public networks.
## Accessing from Windows CVM Instance
1. Log in to a Windows CVM instance. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Configuring Windows CVM</a>.
2. Download a standard SQL client.
>?We recommend you download MySQL Workbench. Visit https://dev.mysql.com/downloads/workbench/ and download an appropriate installer based on your system.
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. **Login**, **Sign Up**, and **No, thanks, just start my download.** will appear on the page. Select **No, thanks, just start my download.** for quick download.
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. Install MySQL Workbench on this CVM instance.
>?
>- Microsoft .NET Framework 4.5 and Visual C++ Redistributable for Visual Studio 2015 are required for the installation.
>- You can click **Download Prerequisites** in the MySQL Workbench installation wizard to enter the corresponding page to download and install them. Then, install MySQL Workbench.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. Open MySQL Workbench, select **Database** > **Connect to Database**, enter your TencentDB for MySQL instance's private (or public) network address, username, and password, and click **OK** to log in.
 - Hostname: enter the private (or public) network address, which can be viewed with the port on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). For public network address, check whether it has been enabled as instructed in [Enabling Public Network Address](#waiwang).
 - Port: private (or public) network port.
 - Username: the username is `root` by default. For public network connection, we recommend you [create a separate account](https://intl.cloud.tencent.com/document/product/236/31900) for easier connection control.
 - Password: the password corresponding to `Username`. If you forgot the password, reset it as instructed in [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
![](https://main.qcloudimg.com/raw/946b50fb05de11d7c68c2262ac4fe933.png)
6. After successful login, the following page will appear, where you can view the modes and objects of the MySQL database, create tables, and perform operations such as data insertion and query.
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## Accessing from Linux CVM Instance
1. Log in to a Linux CVM instance. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/236/31901" target="_blank">Configuring Linux CVM</a>.
2. Taking a CVM instance on CentOS 7.2 (64-bit) as an example, run the following command to install the MySQL client:
```
yum install mysql
```
If `Complete!` is displayed, the MySQL client is installed successfully.
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)
3. Perform the corresponding operation based on the connection method:
 - **Private network connection:**
    1. Run the following command to log in to the TencentDB for MySQL instance:
```
mysql -h hostname -u username -p
```
      - hostname: replace it with the private network address of the target TencentDB for MySQL instance, which can be viewed on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
    	- username: replace it with the default username `root`.
    2. Enter the password corresponding to the `root` account of the TencentDB for MySQL instance after `Enter password:` is prompted. If you forgot the password, please reset it as instructed in [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
    If `MySQL [(none)]>` is displayed, you have logged in to MySQL successfully.
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **Public network connection:**

    1. Run the following command to log in to the TencentDB for MySQL instance:
```
mysql -h hostname -P port -u username -p
```
      - hostname: replace it with the public network address of the target TencentDB for MySQL instance, which can be viewed together with the port on the instance details page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). If the public network address has not been enabled, please enable it as instructed in [Enabling Public Network Address](#waiwang).
      - port: replace it with the public network port number.
      - username: replace it with the public network connection username. We recommend you [create a separate account](https://intl.cloud.tencent.com/document/product/236/31901) for easier connection control.
    2. Enter the password corresponding to the public network connection username after `Enter password:` is prompted. If you forgot the password, reset it as instructed in [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
    In this example, `hostname` is 59281c4exxx.myqcloud.com and public network port is 15311.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. Under the `MySQL \[(none)]>` prompt, you can send an SQL statement to the MySQL server for execution. For specific command lines, please see [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Below takes `show databases;` as an example:
![](//mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)


<span id = "waiwang"></span>
## Appendix 1. Enabling Public Network Connection Address
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance details page.
2. Find **Public Network Address** in the basic information section on the instance details page and click **Enable**.
>? If the basic info section contains the public network address and port, it indicates that the public network address has been enabled.
>
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
3. Click **OK** to start enabling public network access.
4. Once enabled successfully, the public network address can be found in the basic information section.
>?The public network connection can be disabled using the switch. When it is enabled again, the public network address corresponding to the domain name remains the same.

## Appendix 2. Network Connectivity Verification Method
We recommend you troubleshoot and locate network connectivity problems quickly with the `telnet` command. For more information, please see [telnet Command](https://intl.cloud.tencent.com/document/product/236/31901).

If the verification with telnet found that the network access of the TencentDB instance was good, but an error was reported when you tried to log in to it on the command line in the CVM instance, please see [Connection](https://intl.cloud.tencent.com/document/product/236/37783#sytyzysjk).

## Appendix 3. Troubleshooting Connection Errors
If you encounter connection errors, we recommend you use [One-Click Connectivity Checker](https://intl.cloud.tencent.com/document/product/236/37783#sytyzysjk) to troubleshoot the problem first and then find the corresponding solution in [Troubleshooting Connection Errors](https://intl.cloud.tencent.com/document/product/236/37864) according to the check report.

