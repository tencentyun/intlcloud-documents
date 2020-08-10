After creating a TencentDB for MySQL instance, you need to initialize it before you can enable it.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), select the target region, select an instance in "Uninitialized" status in the instance list, and click **Initialize** in the "Operation" column.
![](https://main.qcloudimg.com/raw/945a4e69bef68eb706a520d4cbac13cf.png)
2. In the initialization dialog box that pops up, configure the parameters related to initialization, and click **OK**.
 - **Supported Character Set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is LATIN1, i.e., ISO-8859-1 encoding format. After initializing the instance, you can also change the character set on the instance details page in the console.
 - **Table Name Case Sensitivity**: set whether the table name is case-sensitive, which is yes by default.
 - **Custom Port**: the database access port, which is 3306 by default.
 - **Set Password of Root Account**: the username of the newly created TencentDB for MySQL instance is `root` by default. Set a password for this `root` account.
 - **Confirm Password**: enter the password again.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.


## Subsequent Steps
You can connect to TencentDB for MySQL over both the private and public networks from a Windows or Linux CVM instance. For more information, please see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3130).

