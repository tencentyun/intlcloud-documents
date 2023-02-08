This document describes how to connect to a cluster at a private network or public network address from a Windows CVM instance.

## Prerequisites
You have created a database cluster account as instructed in [Creating Account](https://www.tencentcloud.com/document/product/1098/44612).

## Directions
1. Log in to a Windows CVM instance. For more information, see [Customizing Windows CVM Configurations](https://www.tencentcloud.com/document/product/1098/52633).
2. Download a standard SQL client.
>?We recommend you download MySQL Workbench. Click [here](https://dev.mysql.com/downloads/workbench/) and download an installer based on your operating system.
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. **Login**, **Sign Up**, and **No thanks, just start my download.** will appear on the page. Select **No thanks, just start my download.** to download quickly.
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. Install MySQL Workbench on this CVM instance.
>?
>- Microsoft .NET Framework 4.5 and Visual C++ Redistributable for Visual Studio 2015 are required for the installation.
>- You can click **Download Prerequisites** in the MySQL Workbench installation wizard to enter the corresponding page to download and install them. Then, install MySQL Workbench.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. Open MySQL Workbench, select **Database** > **Connect to Database**, enter the private (or public) network address, username, and password of your TDSQL-C for MySQL cluster and click **OK** to log in.
![](https://main.qcloudimg.com/raw/9c9e5dcc8a2bb9fa15fa4d98a18308f1.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Hostname</td>
<td>Enter the private (or public) network address of the target database, which can be viewed on the cluster details page in the <a href="https://console.cloud.tencent.com/cynosdb">console</a>. For public network address, check whether it has been enabled as instructed in <a href="https://www.tencentcloud.com/document/product/1098/51982">Enabling/Disabling Public Network Address</a>.</td></tr>
<tr>
<td>Port</td>
<td>Private (or public) network port.</td></tr>
<tr>
<td>Username</td>
<td>Enter the account name configured when creating the database account, which is the default account `root` here for example.</td></tr>
<tr>
<td>Password</td>
<td>Enter the password corresponding to the username. If you forgot the password, reset it in the console.</td></tr>
</tbody></table>
6. After successful login, the following page will appear, where you can view the modes and objects of the database, create tables, and perform operations such as data insertion and query.
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## FAQs
#### How do I find the account name or reset the password to log in to the cluster?
You can view the account name you created for cluster connection under **Account Management** on the cluster management page in the TDSQL-C for MySQL console. If you forgot the password, perform the **Reset Password** operation to change the password.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/na6Q197_30.png)

#### Do I need to configure a security group for the TDSQL-C for MySQL cluster when connecting to it over the private or public network?
Yes. For detailed directions, see [Creating and Managing TencentDB Security Groups](https://www.tencentcloud.com/document/product/1098/52007). Note that if the public network access is enabled for connection over the public network, the private network port needs to be opened in the configured security group rule.

#### What should I do if I can't log in to the Linux CVM instance because the security group rules of the instance don't match properly?
If the security group rules of the Linux CVM instance don't match properly (for example, the corresponding port is not opened), and you can't log in to the instance, you can use the [Security Group (Port) Verification Tool](https://console.cloud.tencent.com/vpc/helper) to check the connectivity of the security group.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NwXh031_31.png)
You can locate the possible causes of the login failure through quick check.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vQRD904_32.png)
Then, on the CVM instance details page, select **Security Group** > **Edit Rule** and open the corresponding port. For detailed directions, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

#### What settings may cause a cluster connection failure?
Check whether the CVM instance and the TDSQL-C for MySQL cluster are in the same VPC in the same region under the same Tencent Cloud account. If any of these three prerequisites is not meet, the cluster cannot be connected.
