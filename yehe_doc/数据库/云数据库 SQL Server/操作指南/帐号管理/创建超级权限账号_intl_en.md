This document describes how to create an admin account for a TencentDB for SQL Server instance in the console.

## Admin account description
The System Admin (SA) role is the most privileged role in SQL Server. It can perform any operations in SQL Server without passing any security checks.
**TencentDB for SQL Server single-node (formerly Basic Edition) instances allow you to create an admin account with the SA privilege**, so you can use the account to quickly adapt offline software and move it to the cloud.

<dx-alert infotype="alarm" title="">
- Once an admin account is created for an instance, the sysadmin privilege is enabled, and the product SLA will no longer be guaranteed for the instance.
- You can create only one SA account for each instance.
</dx-alert>

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). Click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select **Account Management** > **Create Account** and enter relevant information in the pop-up window. After confirming that everything is correct, click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HaeX934_1.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Account Name</td>
<td>Account Name: It can contain 1–50 letters, digits, or underscores and must start with a letter. <dx-alert infotype="explain" title="">
The account name cannot contain the following keywords or symbols: `sysadmin`, `sp_addsrvrolemember`, `master.`, `mssql`, `##`, `[ | ]`, `,`, `.`, `;`, `( | )`, `--`.
</dx-alert></td></tr>
<tr>
<td>Account Type</td>
<td>Select **Admin Account**.<blockquote class="rno-document-tips rno-document-tips-alarm">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">Warning</div>        <div class="rno-document-tip-desc"><p>As the admin account has the highest-level management permissions, the instance SLA will not be guaranteed after this account is enabled.</p></div>    </div></blockquote></td></tr>
<tr>
<td>Database</td>
<td>The admin account has the owner permissions of all databases by default.</td></tr>
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
