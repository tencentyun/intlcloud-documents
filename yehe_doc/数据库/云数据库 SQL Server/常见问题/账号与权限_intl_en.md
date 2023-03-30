### How do I manage the account of a TencentDB for SQL Server instance?
We recommend that you manage accounts in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. Click the ID of the target instance to enter the instance management page. On the **Account Management** tab, you can [create](https://www.tencentcloud.com/document/product/238/7521) and [delete](https://www.tencentcloud.com/document/product/238/35794) accounts and [modify account permissions](https://www.tencentcloud.com/document/product/238/35795).

### How do I manage TencentDB for SQL Server databases?
We recommend that you manage databases in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. You can click the ID of the target instance to enter the instance management page. On the **Database Management** tab, you can perform the following operations: [Creating Database](https://www.tencentcloud.com/document/product/238/35780), [Deleting Database](https://www.tencentcloud.com/document/product/238/35781), and [Setting Database Permissions](https://www.tencentcloud.com/document/product/238/47425).

### How do I create an account in TencentDB for SQL Server?
We recommend that you create an account in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Creating Account](https://www.tencentcloud.com/document/product/238/7521).

### How do I delete an account in TencentDB for SQL Server?
We recommend that you delete an account in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Deleting Account](https://www.tencentcloud.com/document/product/238/35794).

### How do I modify account permissions in TencentDB for SQL Server?
We recommend that you modify account permissions in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Modifying Account Permissions](https://www.tencentcloud.com/document/product/238/35795).

[](id:CJSJK1)
### How do I create a database in TencentDB for SQL Server?
We recommend that you create a database in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Creating Database](https://www.tencentcloud.com/document/product/238/35780).

### How do I delete a database in TencentDB for SQL Server?
We recommend that you delete a database in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Deleting Database](https://www.tencentcloud.com/document/product/238/35781).

### How do I modify database permissions in TencentDB for SQL Server?
We recommend that you modify database permissions in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Setting Database Permissions](https://www.tencentcloud.com/document/product/238/47425).

### When managing a database with Microsoft SQL Server Management, the system prompts "Login failed. The login is from an untrusted domain and cannot be used with Windows authentication." Why?
Change the authentication method to "SQL Server Authentication".

### Does TencentDB for SQL Server support assigning the sysadmin role to users?
- Two-node (formerly High Availability/Cluster Edition) instances: For intrusion prevention considerations, the sysadmin role cannot be assigned to users by default. If your business requires this role, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. If you use SSMS to manage databases, the system may prompt that you must have the sysadmin role to perform the operation.
- Single-node (formerly Basic Edition) instances: The sysadmin role can be provided through the admin account. Note that the admin account has the highest-level sysadmin permission and the owner permissions of all databases. After it is enabled, the product SLA will no longer be guaranteed.

### How do I create an account with SA permissions in TencentDB for SQL Server?
For TencentDB for SQL Server two-node (formerly High Availability/Cluster Edition) instances, if your business requires the sysadmin role, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. For single-node (formerly Basic Edition) instances, the sysadmin role can be provided through the admin account in the console. Note that the admin account has the highest-level sysadmin permission and the owner permissions of all databases. After it is enabled, the product SLA will no longer be guaranteed.

[](id:XTZHLJ)
### Can I connect to TencentDB for SQL Server with a Windows system account?
You cannot connect to a TencentDB for SQL Server non-single-node (formerly Basic Edition) instance with a Windows system account. To connect to a single-node (formerly Basic Edition) instance with such account, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### What should I do if I forgot the login password of TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and click the ID of the target instance to enter the instance management page. On the **Account Management** tab, select **More** > **Reset Password** in the **Operation** column to reset the password. For more information, see [Resetting Password](https://www.tencentcloud.com/document/product/238/35796).

### How do I reset the password of TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and click the ID of the target instance to enter the instance management page. On the **Account Management** tab, select **More** > **Reset Password** in the **Operation** column to reset the password. For more information, see [Resetting Password](https://www.tencentcloud.com/document/product/238/35796).

### What should I do if I cannot create any database or table?
Your login account may be a business account without database/table creation permissions. In this case, grant the account the required permissions in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). For more information, see [Setting Database Permissions](https://www.tencentcloud.com/document/product/238/47425).

### Why do I lack permissions to modify database parameters such as `blocked process threshold(s)`?
You might be using a sub-account without parameter modification permissions. You can use the root account or grant the sub-account permissions as instructed in [CAM Overview](https://intl.cloud.tencent.com/document/product/238/34583).

### Can I have the permission to access and create folders on the server in TencentDB for SQL Server?
Currently, TencentDB for SQL Server doesn't allow you to access and create folders on the instance server.

### Can I view connection details in TencentDB for SQL Server?
You can view connection details after connecting to the instance through SSMS. If you don't have relevant permissions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for escalating your database account permissions.

[](id:CKMSQLB)
### Can I view the slow SQL table in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the target instance ID in the instance list, and [query and download slow query logs](https://intl.cloud.tencent.com/document/product/238/47569) on the slow query log page.
The slow SQL table of TencentDB for SQL Server is not displayed by default. You can view it after connecting to the instance through SSMS. If you don't have relevant permissions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for escalating your database account permissions.

### Can I have the SQL trace permission in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), and you can see that the SQL trace permission is granted to accounts created on the **Account Management** tab by default.
If your account is created manually through the SSMS client, it doesn't support SQL trace by default. You can run the following command to authorize it with the admin account as needed: `GRANT ALTER TRACE TO [$account];`.

### Why does the system prompt that I don't have the permission to enable Profiler in TencentDB for SQL Server?
Accounts created on the **Account Management** tab in the TencentDB for SQL Server console have the Profiler permission by default. However, accounts manually created through SSMS don't have such permission. In this case, you can run the following command to authorize them: `GRANT ALTER TRACE TO [$account];`.

### Can I use accounts created in the primary instance in read-only instances?
Accounts created in the primary instance will be synced to read-only instances but cannot be managed there. They support only read but not write operations in read-only instances.

### Will permissions be synced to replica instances and read-only instances automatically after an account in the primary instance is deleted and created again?
After an account in the TencentDB for SQL Server primary instance is deleted and created again, the permissions and other modifications in the primary instance will be automatically synced to replica instances and read-only instances.

[](id:TBDZDSL)
### How do I sync account permissions on two-node (formerly High Availability/Cluster Edition) primary and replica instances to read-only instances?
Accounts created in a two-node (formerly High Availability/Cluster Edition) primary instance will be automatically synced to read-only instances. 2017/2019 Enterprise two-node instances use the Always On mode for sync, while 2008 R2/2012/2014/2016 Enterprise two-node instances use the publish/subscribe mode for sync. Accounts created in the primary instance in the console will be synced to read-only instances in real time. After the sync is completed, you can use the created login username or modify the password permission in read-only instances.

### Can I manage database accounts at a finer granularity (such as source address and access table)?
You can use commands for authorization at a finer granularity after connecting to a database.

### Which account permissions are granted by default in TencentDB for SQL Server?
The following account permissions are granted in TencentDB for SQL Server by default:
Server-level roles:
- Securityadmin: Manages login and the `CREATE DATABASE` permission and views the audit information.
- Processadmin: Manages SQL Server processes.
- Dbcreator: Creates and modifies databases.

Database-level roles:
- db_owner: Owns the database and performs all database operations.
- db_datareader: Views the data in all user tables in a database.
- db_reader: Reads data in the database.
- db_writer: Writes data to the database.


