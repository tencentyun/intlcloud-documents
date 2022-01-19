After a TencentDB for MySQL instance is created, it is in the **Uninitialized** status and needs to be initialized before it can be used.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the target region, select an instance in **Uninitialized** status in the instance list, and click **Initialize** in the **Operation** column.
2. In the initialization pop-up window, configure the initialization parameters and click **OK**.
 - **Character Set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is UTF8. After initializing the instance, you can change the character set on the instance details page in the console. For more information, see [Use Limits > Notes on character set](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Table Name Case Sensitivity**: whether the table name is case sensitive. The default value is yes.
 - **Custom Port**: the database access port, which is 3306 by default.
 - **Set Password of Root Account**: set the password of the root account (the default user name for a new MySQL database is "root").
 - **Confirm Password**: enter the password again.
3. In the initialization pop-up window, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/cd8d4f83c43cc23b23c50c2e85773473.png)
4. Return to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.

## Subsequent Operations
You can access the TencentDB for MySQL instance over both private and public networks from a Windows or Linux CVM instance. For more information, see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).
