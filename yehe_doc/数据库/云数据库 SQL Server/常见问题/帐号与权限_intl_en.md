### How do I manage the account of a TencentDB for SQL Server instance?
We recommend you manage accounts in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. Click the ID of the target instance to enter the instance management page. On the **Account Management** tab, you can [create](https://intl.cloud.tencent.com/document/product/238/7521) and [delete](https://intl.cloud.tencent.com/document/product/238/35794) accounts and [modify account permissions](https://intl.cloud.tencent.com/document/product/238/35795).

### How do I manage TencentDB for SQL Server databases?
We recommend you manage databases in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. You can click the ID of the target instance to enter the instance management page. On the **Database Management** tab, you can perform the following operations: [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780), [Deleting Database](https://intl.cloud.tencent.com/document/product/238/35781), and [Setting Database Permissions](https://intl.cloud.tencent.com/document/product/238/47425).

### How do I create an account in TencentDB for SQL Server?
We recommend you create an account in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Creating Account](https://intl.cloud.tencent.com/document/product/238/7521).

### How do I delete an account in TencentDB for SQL Server?
We recommend you delete an account in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Deleting Account](https://intl.cloud.tencent.com/document/product/238/35794).

### How do I modify account permissions in TencentDB for SQL Server?
We recommend you modify account permissions in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Modifying Account Permissions](https://intl.cloud.tencent.com/document/product/238/35795).

[](id:CJSJK1)
### How do I create a database in TencentDB for SQL Server?
We recommend you create a database in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780).

### How do I delete a database in TencentDB for SQL Server?
We recommend you delete a database in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Deleting Database](https://intl.cloud.tencent.com/document/product/238/35781).

### How do I modify database permissions in TencentDB for SQL Server?
We recommend you modify database permissions in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) rather than on the SSMS client. For more information, see [Setting Database Permissions](https://intl.cloud.tencent.com/document/product/238/47425).

### What should I do if the system prompts "Login failed. The login is from an untrusted domain and cannot be used with Windows authentication" when I try to manage databases with SSMS?
Change the authentication method to **SQL Server Authentication**.

### Does TencentDB for SQL Server support assigning the sysadmin role to users?
- Dual-Server High Availability/Cluster Editions: For intrusion prevention considerations, the sysadmin role cannot be assigned to users by default. If your business requires this role, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. If you use SSMS to manage databases, the system may prompt that you must have the sysadmin role to perform the operation.
- Basic Edition: You can use an admin account to assign the sysadmin role to users.

### How do I create an account with SA permissions in TencentDB for SQL Server?
TencentDB for SQL Server doesn't support creating accounts with sysadmin permissions by default. On Dual-Server High Availability/Cluster Editions, if your business requires the sysadmin role, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. On Basic Edition, you can use the admin account to grant permissions in the console.

[](id:XTZHLJ)
### Can I connect to TencentDB for SQL Server with a Windows system account?
You cannot connect to a TencentDB for SQL Server non-Basic Edition instance with a Windows system account. To connect to a Basic Edition instance with such account, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### What should I do if I forgot the login password of TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and click the ID of the target instance to enter the instance management page. On the **Account Management** tab, select **More** > **Reset Password** in the **Operation** column to reset the password. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/238/35796).

### How do I reset the password of TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and click the ID of the target instance to enter the instance management page. On the **Account Management** tab, select **More** > **Reset Password** in the **Operation** column to reset the password. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/238/35796).

### Why can't I create databases/tables?
Your login account may be a business account without database/table creation permissions. In this case, grant the account the required permissions in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). For more information, see [Setting Database Permissions](https://intl.cloud.tencent.com/document/product/238/47425).

### Why do I lack permissions to modify database parameters such as `blocked process threshold(s)`?
You might be using a sub-account without parameter modification permissions. You can use the root account or grant the sub-account permissions as instructed in [Overview](https://intl.cloud.tencent.com/document/product/238/34583).

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
### How do I sync account permissions on Dual-Server High Availability/Cluster Edition primary and replica instances to read-only instances?
Accounts created in a Dual-Server High Availability/Cluster Edition primary instance will be automatically synced to read-only instances. The Cluster Edition uses the Always On mode for sync, while the Dual-Server High Availability Edition uses the publish/subscribe mode for sync. Accounts created in the primary instance in the console will be synced to read-only instances in real time. After the sync is completed, you can use the created login username or modify the password permission in read-only instances.

### Can I manage database accounts at a finer granularity (such as source address and access table)?
You can use commands for authorization at a finer granularity after connecting to a database.

### Which account permissions are granted by default in TencentDB for SQL Server?
The following account permissions are granted in TencentDB for SQL Server by default:
Server-level roles:
- Securityadmin: Manages login and the `CREATE DATABASE` permission and views the audit information.
- Processadmin: Manages SQL Server processes.
- Dbcreator: Creates and modifies databases.

Database-level roles:
- db_owner: Performs all operations on a database.
- db_datareader: Views the data in all user tables in a database.
