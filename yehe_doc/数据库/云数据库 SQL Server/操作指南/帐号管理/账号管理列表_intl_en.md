This document describes the fields in the account list.

## Database account
After you create a TencentDB for SQL Server instance, you can create different database accounts to allocate and manage databases based on your business needs.

## Viewing the account list
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. In the instance list, click **Manage** in the **Operation** column of the target instance to enter the **Instance Details** page.
3. Click **Account Management** to enter the **Account Management** tab.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/a6Aj811_11.png)

## Tools
| Tool | Description |
|---------|---------|
| Search box | Click ![](https://qcloudimg.tencent-cloud.cn/raw/4e9962a6b05796851af7e63f3bea18dc.png) to filter accounts. You can fuzzy search for accounts by account name. |
| Refresh | Click ![](https://qcloudimg.tencent-cloud.cn/raw/309481e9077b12e66da812127caa683a.png) to refresh the list. |

## Fields in the account list

| Field | Description |
|---------|---------|
| Account Name | The name of the account created for the instance. |
| Account Type | The types of accounts created in the instance. The types of accounts supported by different instance architectures are as follows: <br>**Two-node**<li>Privileged account: Instance admin account, which has the owner permissions of all databases by default. <li>Standard account: Non-admin account, which can be granted the read/write, read-only, or owner permissions of a specific database. <li>Designated account: It can only view and own the specified database. A designated account can be authorized to multiple databases, but a database can be authorized to only one designated account. <br>**Single-node**<li>Admin account: Instance admin account, which has the highest-level sysadmin permission and the owner permissions of all databases. <strong>After the admin account is enabled, the product SLA will no longer be guaranteed.</strong><li>Privileged account: Instance admin account, which has the owner permissions of all databases by default. <li>Standard account: Non-admin account, which can be granted the read/write, read-only, or owner permissions of a specific database. <li>Designated account: It can only view and own the specified database. A designated account can be authorized to multiple databases, but a database can be authorized to only one designated account. |
| Status | The status of the account. |
| Account Creation Time | The time when the account was created, which can be sorted in ascending or descending order. |
| Account Update Time | The time when the account was last updated, which can be sorted in ascending or descending order. |
| Password Update Time | The time when the account password was last reset, which can be sorted in ascending or descending order. |
| Database | The databases that the account is authorized to access. |
| Remarks | The remarks of the account. |
| Operation | <li>Set Permissions: Set the read/write or read-only permission of the specified database for the account. <li>Reset Password: Reset the password of the account. <li>Delete Account: Delete the account. |

>?For each operation in the account list, you can select multiple accounts and click the corresponding batch operation button above the list for batch management.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/HciT537_15.png)

## More
- [Creating Account](https://www.tencentcloud.com/document/product/238/7521)
- [Modifying Account Permissions](https://intl.cloud.tencent.com/document/product/238/35795)
- [Resetting Instance Password](https://www.tencentcloud.com/document/product/238/35796)
- [Deleting Account](https://intl.cloud.tencent.com/document/product/238/35794)

  
