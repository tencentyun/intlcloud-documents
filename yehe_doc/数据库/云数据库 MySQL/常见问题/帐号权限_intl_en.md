### How do I authorize a MySQL client installed on a server to access TencentDB for MySQL instances?
You can go to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) to modify the address of the server where your MySQL client is installed to control its access. 

For more information, see [Modifying Host Addresses with Access Permissions](https://intl.cloud.tencent.com/document/product/236/31903).  

### What should I do if I cannot log in to DMC?
1. You might be using the wrong database account. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance name and go to **Database Management** > **Manage Account**, locate the account, and click **More** > **Modify Host** in the **Operation** column. Set **New Host** to "%" or the address of the server where your MySQL client is installed to grant the account access permissions.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/6iPR545_2.png)
For more information, see [Modifying Host Addresses with Access Permissions](https://intl.cloud.tencent.com/document/product/236/31903).  

You can also use root account to log in to DMC.

2. If you are using the right account, your password may be incorrect. Enter a correct password or [reset your password](https://intl.cloud.tencent.com/document/product/236/31901).


### What should I do if I cannot create any database or table?
You might be using a database account that is not authorized to create databases or tables. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance name and go to **Database Management** > **Manage Account**, locate the account, and click **Modify Permissions** in the **Operation** column to grant permissions as shown below.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/tQ3Q678_3.png)

### What should I do if I have no permissions to modify database parameters such as `sql_mode`?
You might be using a sub-account without parameter modification permissions. You can use the root account or grant the sub-account permissions as instructed in [Overview](https://intl.cloud.tencent.com/document/product/236/14469).

### How do I grant a sub-account permissions to modify TencentDB for MySQL instances?
To grant a user permissions to create and manage TencentDB instances, you can implement the `QcloudCDBFullAccess` policy for the user. For more information, see [Console Examples > Full Access Policy for TencentDB](https://intl.cloud.tencent.com/document/product/236/14468).

