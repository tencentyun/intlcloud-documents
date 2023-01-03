Besides the default account created by the system, you can create other database accounts in the console as needed.

## Directions
1. Log in to the [ TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, select the **Account Management** tab and click **Create Account**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RIui019_13.png)
3, In the **Create Account** window, set the following information, and click **OK**.
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/T2Ar086_14.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Account Name</td>
<td>The database account name can contain 1-16 letters, digits, and underscores (_). It must begin with a letter and end with a letter or digit.</td></tr>
<tr>
<td>Host</td>
<td>Specify a host address to access the database. It can be an IP and contain `%` (indicating no limit on the IP range). Multiple hosts should be separated by line break, space, semicolon, comma, or vertical bar.</code><ul><li>Example 1: Enter `%` to indicate no limit on the IP range, that is, clients at all IP addresses are allowed to use this account to access the database. <br></li><li>Example 2: Enter `10.5.10.%`to indicate that clients with an IP range within `10.5.10.%` are allowed to use this account to connect to the database.</li></ul></td></tr>
<tr>
<td>Set Password</td>
<td>The password can contain 8–64 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols <img src="https://qcloudimg.tencent-cloud.cn/raw/1c7509f6c3fefb127a4547bd31b98442.png" alt=""></td></tr>
<tr>
<td>Confirm Password</td>
<td>Enter the same account password again</td></tr>
<tr>
<td>Connections</td>
<td>Enter the maximum number of connections for the account. Valid range: 1-10240. If you don't enter a value, the maximum number of connections will be 10240. </td></tr>
<tr>
<td>Remarks</td>
<td>Remarks can contain up to 255 characters.</td></tr>
</tbody></table>
4. After the database account is created successfully, you can manage it in the database account list with the operations, such as permission modification, password reset, and account setting modification.

