## Operation Scenario
If your CVM and TencentDB for MySQL instances are deployed in the same region, you don't need to apply for a public network address. If they are in different regions or on non-Tencent Cloud systems, you need to enable a public network address to connect to TencentDB for MySQL (not applicable to instances outside Mainland China). This document describes how to enable public network access and log in to your instance.

## Directions

### Enabling public network access
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, select the instance to be modified and click the instance name or **Manage** in the "Operation" column to enter the instance details page.
![](https://main.qcloudimg.com/raw/cd32da2cfe0e7bc51bfe9d41563c4dc8.png)
3. Find **Public Network Address** in the basic information section on the instance details page and click **Enable**.
![](https://main.qcloudimg.com/raw/1ca02f08affa0a9756f041781827d864.png)
4. Click **OK** and the enabling process starts.
![](https://main.qcloudimg.com/raw/a1f1412c229b66b75b4ea2834cb55589.png)
5. After the public network address is enabled successfully, it can be found in the basic info.
6. The public network access can be disabled using the switch. When it is enabled again, the public IP corresponding to the domain name remains the same.

### Logging in to an instance
1. Use the following standard MySQL statement to log in to TencentDB on a server that is connected to the network and has a MySQL client installed. The TencentDB account used for login can be any one as shown in **Account Management**.
```
mysql -h hostname -P port -u username -p
```
>
>- Replace "hostname" with the public IP address of the target instance, replace "port" with the public network port, replace "username" with the username for public network access such as "cdb_outerroot", and enter its password when prompted with "Enter password:".
- The username is for public network access. You are recommended to create a separate account for easier access control.
>
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
2. After logging in to TencentDB, you can use MySQL statements to manage your instance. For more information on MySQL statements, see [MySQL's official documentation](http://dev.mysql.com/doc/).
Below is an example:
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)
