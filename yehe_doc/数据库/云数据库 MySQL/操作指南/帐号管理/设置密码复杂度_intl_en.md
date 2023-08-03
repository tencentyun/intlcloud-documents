TencentDB for MySQL allows you to set the password complexity to improve the strength of database access passwords and optimize the database security.

## Prerequisites
- The database version is:
 - MySQL 5.6, with minor version 20201231 or later.
 - MySQL 5.7, with minor version 20201231 or later.
 - MySQL 8.0, with minor version 20201230 or later.

- The instance must be on a two-node/three-node architecture.

## Use Limits
For any password set during account creation or reset in the TencentDB for MySQL console, it must at least meet the following initial account password requirements:
- It can contain 8 to 64 characters
- It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols.
- Special characters are `_+-&=!@#$%^*()`.

## Enabling Password Complexity
>?After the password complexity feature is enabled, any password set during account creation or reset must follow the password complexity policy.

### Enabling when creating an instance on the purchase page
1. Log in to the [TencentDB for MySQL purchase page](https://buy.intl.cloud.tencent.com/cdb).
2. Configure parameters as needed. Select **Enable** after the **Password Complexity** parameter.
![](https://qcloudimg.tencent-cloud.cn/raw/d8954b4267f8b9c75b3f33834c8a8ad5.png)
3. Set the following parameters.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Min Number of Uppercase or Lowercase Letters</td>
<td>You can select a number between 1 (default value) and 16.</td></tr>
<tr>
<td>Min Number of Digitals</td>
<td>You can select a number between 1 (default value) and 16.</td></tr>
<tr>
<td>Min Number of Symbols</td>
<td>You can select a number between 1 (default value) and 16.</td></tr>
<tr>
<td>Min Number of Password Characters</td>
<td>You can select a number between 8 (default value) and 64. The minimum value must be greater than the sum of the above three parameters.</td></tr>
</tbody></table>

### Enabling for existing instances in the console
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Database Management**> **Account Management** and click **Password Complexity** (disabled by default).
![](https://qcloudimg.tencent-cloud.cn/raw/ae8c348798736f38a4ea1069e29c7b5f.png)
3. Select **Enable** in the **Password Complexity** pop-up window, set the following parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/f4407c8d310de235c596f541f087d747.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Min Number of Uppercase or Lowercase Letters</td>
<td>You can select a number between 1 (default value) and 16.</td></tr>
<tr>
<td>Min Number of Digitals</td>
<td>You can select a number between 1 (default value) and 16.</td></tr>
<tr>
<td>Min Number of Symbols</td>
<td>You can select a number between 1 (default value) and 16.</td></tr>
<tr>
<td>Min Number of Password Characters</td>
<td>You can select a number between 8 (default value) and 64. The minimum value must be greater than the sum of the above three parameters.</td></tr>
</tbody></table>

## Disabling Password Complexity
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Database Management**> **Account Management** and click **Password Complexity**.
![](https://qcloudimg.tencent-cloud.cn/raw/ae613393746da572d25e4bc90e940895.png)
3. Select **Disable** in the **Password Complexity** pop-up window and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/06c7f71ceaacb063768ac6c83ab78b76.png)

## Relevant Documentation
- [Creating Account](https://intl.cloud.tencent.com/document/product/236/31900)
- [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901)
