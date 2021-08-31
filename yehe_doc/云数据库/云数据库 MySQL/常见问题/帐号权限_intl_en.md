### How do I authorize a MySQL client installed on a server to access TencentDB for MySQL instances?
You can go to [MySQL Console](https://console.cloud.tencent.com/cdb) to modify the address of the server where your MySQL client is installed to control its access. 
  
### What should I do if I cannot log in to the data management console (DMC)?
1. You might be using the wrong database account. Please log in to [MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name and go to **Database Management** > **Manage Account**, locate the account, and click **More** > **Modify Host** in the "Operation" column. Set **New Host** to "%" or the address of the server where your MySQL client is installed to grant the account access permissions.
![](https://main.qcloudimg.com/raw/2e0f60d3237e8e244b51dd7e164de315.png)  

You can also use root account to log in to DMC.

2. If you are using the right account, your password may be incorrect. Please enter a correct password or [reset your password](https://intl.cloud.tencent.com/document/product/236/31901).


### What should I do if I cannot create any database or table?
You might be using a database account that is not authorized to create databases or tables. Please log in to [MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name and go to **Database Management** > **Manage Account**, locate the account, and click **Modify Permissions** in the "Operation" column to grant permissions as shown below.  
![](https://main.qcloudimg.com/raw/b33188cf3aba103b415c0ecc38fb0168.png)

### What should I do if I have no permissions to modify database parameters such as `sql_mode`?
You might be using a sub-account without parameter modification permissions. You can use the root account or grant the sub-account permissions as instructed in [Access Management](https://intl.cloud.tencent.com/document/product/236/14469).

### How do I grant a sub-account permissions to modify TencentDB for MySQL instances?
To grant a user permissions to create and manage TencentDB instances, you can implement the `QcloudCDBFullAccess` policy for the user as instructed in [Full read/write permission policy for TencentDB](https://intl.cloud.tencent.com/document/product/236/14468).


