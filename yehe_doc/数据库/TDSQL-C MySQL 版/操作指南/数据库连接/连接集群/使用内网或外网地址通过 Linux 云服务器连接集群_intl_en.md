This document describes how to connect to a cluster at a private network or public network address from a Linux CVM instance.

## Prerequisites[](id:QTTJ)
You have created a database cluster account as instructed in [Creating Account](https://www.tencentcloud.com/document/product/1098/44612).

## Directions
1. Log in to the Linux CVM instance. For more information, see [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/1098/52632).
2. Taking a CVM instance on CentOS 7.2 (64-bit) as an example, run the following command to install the MySQL client.
```
yum install mysql
```
If `Complete!` is displayed, the MySQL client is installed successfully.
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)

3. Perform the corresponding operation based on the connection method:
 - **Private network connection:**
    1. Run the following command to log in to the TDSQL-C for MySQL cluster.
```
mysql -h hostname -P port -u username -p
```
      - hostname: Replace it with the private network address of the target TDSQL-C for MySQL cluster, which can be viewed on the cluster details page in the [console](https://console.cloud.tencent.com/cynosdb).
      - port: Replace it with the private network port number.
    	- username: Replace it with the name of the account created in [Prerequisites](#QTTJ), which is the default account name `root` here for example.
For example, if the private network address is `10.0.168.14:5308` and the account name is `root`, enter the following connection command: `mysql -h 10.0.168.14 -P 5308 -u root -p`.
    2. Enter the password corresponding to the account in the above command after `Enter password:` is prompted. If you forgot the password, you can reset it as instructed in [Resetting Password](https://www.tencentcloud.com/document/product/1098/44611).
        If `MySQL [(none)]>` is displayed, you have logged in to TDSQL-C for MySQL successfully.
      ![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)

   - **Public network connection:**

    1. Run the following command to log in to the TDSQL-C for MySQL cluster.
```
mysql -h hostname -P port -u username -p
```
      - hostname: Replace it with the public network address of the target TDSQL-C for MySQL cluster, which can be viewed together with the port on the cluster details page in the [console](https://console.cloud.tencent.com/cynosdb). If the public network address has not been enabled, enable it as instructed in [Enabling/Disabling Public Network Address](https://www.tencentcloud.com/document/product/1098/51982).
      - port: Replace it with the public network port number.
      - username: Replace it with the account name for public network connection. We recommend you create a separate account in the console for easier connection control.
    2. Enter the password corresponding to the account name for public network connection after `Enter password:` is prompted. If you forgot the password, reset it as instructed in [Resetting Password](https://www.tencentcloud.com/document/product/1098/44611).
    In this example, `hostname` is 59281c4exxx.myqcloud.com and public network port is 15311.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. Under the `MySQL [(none)]>` prompt, you can send a SQL statement to the TDSQL-C for MySQL server for execution. For specific command lines, see [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).

## FAQs
#### How do I find the account name or reset the password to log in to the cluster?
You can view the account name you created for cluster connection under **Account Management** on the cluster management page in the TDSQL-C for MySQL console. If you forgot the password, perform the **Reset Password** operation to change the password.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VTEZ284_22.png)

#### Do I need to configure a security group for the TDSQL-C for MySQL cluster when connecting to it over the private or public network?
Yes. For detailed directions, see [Creating and Managing TencentDB Security Groups](https://www.tencentcloud.com/document/product/1098/52007). Note that if the public network access is enabled for connection over the public network, the private network port needs to be opened in the configured security group rule.

#### What should I do if I can't log in to the Linux CVM instance because the security group rules of the instance don't match properly?
If the security group rules of the Linux CVM instance don't match properly (for example, the corresponding port is not opened), and you can't log in to the instance, you can use the [Security Group (Port) Verification Tool](https://console.cloud.tencent.com/vpc/helper) to check the connectivity of the security group.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5QCA495_23.png)
You can locate the possible causes of the login failure through quick check.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IcLQ390_24.png)
Then, on the CVM instance details page, select **Security Group** > **Edit Rule** and open the corresponding port. For detailed directions, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

#### What settings may cause a cluster connection failure?
Check whether the CVM instance and the TDSQL-C for MySQL cluster are in the same VPC in the same region under the same Tencent Cloud account. If any of these three prerequisites is not meet, the cluster cannot be connected.

