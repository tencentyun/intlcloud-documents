
You can create an account, set account permissions, and change the account password in the TencentDB for MongoDB console to manage database access permissions more easily. 

## Background
- TencentDB for MongoDB has two default users: `rwuser` and `mongouser`. TencentDB for MongoDB 3.2 supports both of them by default, while 3.6, 4.0, and 4.2 only support the `mongouser` user by default.
  - Only **rwuser** is authenticated with MONGODB-CR.
  - Both **mongouser** and users created in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) are authenticated with SCRAM-SHA-1.
- You can set multiple accounts and grant each of them different database read/write permissions for database access at a finer granularity and higher data security.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support database account management.

## Notes
- After you create an account and grant it the access permission, it will take effect in 2 minutes after the system performs the backend configuration.
We recommend you reset the database password periodically at least once every three months.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
### Viewing account information
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Database Management** > **Account Management** page to view the information of all accounts of the current database.

### Creating account
1. On the **Account Management** page, click **Create Account**.
2. On the **Create Account** tab in the **Set Permissions** pop-up window, configure the account information according to the table below and click **OK**.
<table>
<thead><tr><th>Parameter</th><th>Required</th><th>Description</th><th>Value Range/Valid Values</th><th>Sample Value</th></tr></thead>
<tbody>
<tr>
<td>Account Name</td>
<td>Yes</td>
<td>Set the name of the new account.</td>
<td>Account name requirements:<ul><li>It can contain 1–32 characters.</li><li>It can contain letters, digits, underscores, and hyphens.</li></ul></td>
<td>test</td></tr>
<tr>
<td>Account Password</td>
<td>Yes</td>
<td>Set the password of the new account.</td>
<td>Password requirements: <ul><li>It can contain 8–32 characters.</li><li>It must contain at least two of the following types of characters: letters, digits, and special symbols `!@#%^*()_`.</li></ul></td>
<td>test@123</td></tr>
<tr>
<td>Confirm Password</td>
<td>Yes</td>
<td>Confirm the password of the new account.</td>
<td>Password requirements: <ul><li>It can contain 8–32 characters.</li><li>It must contain at least two of the following types of characters: letters, digits, and special symbols `!@#%^*()_`.</li></ul></td>
<td>test@123</td></tr>
<tr>
<td>Remarks</td>
<td>No</td>
<td>Remarks</td>
<td>Any characters</td>
<td>test</td></tr>
<tr>
<td>mongouser Password</td>
<td>Yes</td>
<td>Enter the password of the `mongouser` user.</td>
<td>`mongouser` password requirements: <ul><li>It must contain 8-32 characters. </li><li>It supports uppercase letters, lowercase letters, and digits. </li><li>It supports the following symbols: !@#%^*()_ </li><li>It cannot all be letters or digits.</li></ul></td>
<td>test@123</td></tr>
</tbody></table>
3. On the **Set Permissions** page, set the database access permissions for this account.
<table>
<thead><tr><th>Parameter</th><th>Description</th><th>Value Range/Valid Values</th></tr></thead>
<tbody>
<tr>
<td>Global Permission</td>
<td>It is used to set the global permission to access all databases for this account.</td>
<td><ul><li>No permission: no data read/write permission.</li><li>Read-Only: only data read permission.</li><li>Read/Write: data read/write permission.</li></ul></td></tr>
<tr>
<td>Instance Details</td>
<td>It is used to set the permission to access a specific database for this account.</td>
<td><ul><li>Inherit global data: global permission is used.</li><li>No permission: no data read/write permission.</li><li>Read-Only: only data read permission.</li><li>Read/Write: data read/write permission.</li></ul></td></tr>
</tbody></table>
4. (Optional) Click **Create Database**, and a new database will be added to the database list. Enter the name of the new database in the input box, click **OK** after the input box, and set the access permission of this database.
>?The created new database is not a real database but is only used to preset the access permission of this database.
5. Click **OK**, wait 2 minutes for the system configuration to take effect, and then you can use this account to access databases.

### Modifying account permission
1. In the account list on the **Account Management** tab, find the target account.
2. Click **View/Set** in the **Operation** column.
3. In the **Set Permissions** pop-up window, modify the account permission.
4. Click **OK**.

### Changing account password
1. In the account list on the **Account Management** tab, find the target account.
2. Click **Reset Password** in the **Operation** column.
3. In the **Reset Password** pop-up window, enter the **New Password** and **Confirm Password**.
   The password requirements are as follows:
   - It can contain 8–32 characters.
   - It must contain at least two of the following types of characters: letters, digits, and special symbols `!@#%^\*()_`.
4. Click **OK**.

## Relevant Operations
### Viewing account URI
1. In the account list on the **Account Management** tab, find the target account.
2. Click **Connection URI** in the **Operation** column.
3. In the **Connection help** pop-up window, view the information of the connection URI of the account.
For more information on instance connection, see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).
4. Click **OK**.

### Deleting account
1. In the account list on the **Account Management** tab, find the target account.
2. Click **Delete** in the **Operation** column.
3. In the **Delete User** pop-up window, confirm the information of the account to be deleted.
4. Click **OK**.

## Related APIs
| API | Description |
| ----------------------- | ------------------------------------------------------------ |
| ResetDBInstancePassword | [Changes the password of instance user](https://intl.cloud.tencent.com/document/product/240/37924) |

