TDSQL-C for MySQL supports instance-level dedicated IP address, which allows you to connect to the instance through the IP address of a read-write instance or read-only instance in a cluster. This document describes how to connect to an instance in a cluster from a Linux CVM instance via private or public network.

## Prerequisites[](id:QTTJ)
You have created a database cluster account. For more information, see [Creating Account](https://www.tencentcloud.com/document/product/1098/44612).

## Step1: Query the private and public IP address of the instance to be connected.
1. Log in to the [TDSQL-C MySQL console](https://console.cloud.tencent.com/cynosdb/mysql/ap-beijing/cluster/cynosdbmysql-fo7dcbse/detail).
2. On the cluster list page, proceed based on the actually used view mode: 
<dx-tabs>
::: Tab view
1. Click the target cluster in the cluster list on the left to enter the cluster management page.
2. On the **Cluster Details** tab, find the target instance, and view its private and public network IP address under **Network**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fNte738_1.png)
:::
::: List view
1. Find the target cluster in the cluster list and click the **Cluster ID** or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select the read-write or read-only instance on the instance list page, and you can view the instance private and public network IP address under **Private/Public Network Address**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Q36Q803_2.png)
:::
</dx-tabs>

## Step 2: Connect to the target instance in a cluster
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
      - hostname: Replace it with the private network address of the target TDSQL-C for MySQL cluster as instructed in [Step 1](#SLIPDZ).
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
      - hostname: Replace it with the public network address of the target TDSQL-C for MySQL instance in a cluster as instructed in [Step 1](#SLIPDZ). If the public network address has not been enabled, enable it as instructed in [Enabling/Disabling Public Network Address](https://www.tencentcloud.com/document/product/1098/51982).
      - port: Replace it with the public network port number.
      - username: Replace it with the account name for public network connection. We recommend that you create a separate account in the console for easier connection control.
    2. Enter the password corresponding to the account name for public network connection after `Enter password:` is prompted. If you forgot the password, reset it as instructed in [Resetting Password](https://www.tencentcloud.com/document/product/1098/44611).
    In this example, `hostname` is 59281c4exxx.myqcloud.com and public network port is 15311.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. Under the `MySQL [(none)]>` prompt, you can send a SQL statement to the TDSQL-C for MySQL server for execution. For specific command lines, see [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Below takes `show databases;` as an example:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/MTd3827_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1686191193171.png)

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
Then, on the CVM instance details page, select **Security Group** > **Edit Rule** and open the corresponding port. For detailed directions, see [Adding Security Group Rules](https://www.tencentcloud.com/document/product/213/34272).

#### What settings may cause a cluster connection failure?
Check whether the CVM instance and the TDSQL-C for MySQL cluster are in the same VPC in the same region under the same Tencent Cloud account. If any of these three prerequisites is not meet, the cluster cannot be connected.
