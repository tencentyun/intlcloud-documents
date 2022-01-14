After creating a TencentDB for MySQL instance, you need to initialize it before you can enable it.

## Directions
1. Log in to [MySQL Console](https://console.cloud.tencent.com/cdb) and select a region. In the instance list, locate the desired "Uninitialized" instance, and click **Initialize** in "Operation" column.
![](https://main.qcloudimg.com/raw/945a4e69bef68eb706a520d4cbac13cf.png)
2. In the initialization dialog box that pops up, configure the parameters, and click **OK**.
 - **Supported character set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is UTF8. After initializing the instance, you can also change the character set on the instance details page in the console. For more information, please see [Notes on character set](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Case-sensitivity of the table name**: whether the table name is case sensitive. It is case sensitive by default.
 - **Custom port**: the database access port, which is 3306 by default.
 - **Root account password**: the default user name for the new MySQL database is "root". You can set the password of the root account.
 - **Confirm password**: enter the password again.
3. In the initialization dialog box that pops up, click **OK**.

4. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.


## Next Steps
For public network you don't have to access from CVM. For more information, please see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).

