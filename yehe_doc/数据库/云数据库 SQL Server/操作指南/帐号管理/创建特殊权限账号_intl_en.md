This document describes how to create a designated account for a TencentDB for SQL Server instance in the console.

## Designated account description
You can create one or multiple designated accounts for a TencentDB for SQL Server single-node (formerly Basic Edition) or two-node (formerly High Availability/Cluster Edition) instance. Note the following for designated accounts:
A designated account can only view and own the specified database.
For example, if account B is created in instance A and designated to have the owner permission of database `db1`, then when logging in to instance A with designated account B, you can only view database `db1`, but you can perform all operations on it.
- A designated account can be authorized to multiple databases, but a database can be authorized to only one designated account.
This means that a designated account can have the owner permissions of multiple databases, but a database with owner permission granted to a designated account cannot be authorized to other designated accounts.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). Click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select **Account Management** > **Create Account** and enter relevant information in the pop-up window. After confirming that everything is correct, click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Twuv079_13.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Account Name</td>
<td>Account Name: It can contain 1–50 letters, digits, or underscores and must start with a letter. <dx-alert infotype="explain" title="">
The account name cannot contain the following keywords or symbols: `sysadmin`, `sp_addsrvrolemember`, `master.`, `mssql`, `##`, `[ | ]`, `,`, `.`, `;`, `( | )`, `--`.
</dx-alert></td></tr>
<tr>
<td>Account Type</td>
<td>Select **Designated Account**.<blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">Note</div>        <div class="rno-document-tip-desc"><p>The designated account can only view and own the specified database.</p></div>    </div></blockquote></td></tr>
<tr>
<td>Database</td>
<td>Select target databases in the **Unauthorized Database** list. The selected databases and permissions are displayed under **Authorized Database** on the right, and the selected databases can be unselected. </td></tr>
<tr>
<td>New Password</td>
<td>The password must contain 8–32 characters in at least two of the following types: letters, digits, and symbols `_+-&amp;=!@#$%^*()[]`.</td></tr>
<tr>
<td>Confirm Password</td>
<td>Enter the password again.</td></tr>
<tr>
<td>Remarks</td>
<td>Optional. It can contain up to 256 characters.</td></tr>
</tbody></table>
