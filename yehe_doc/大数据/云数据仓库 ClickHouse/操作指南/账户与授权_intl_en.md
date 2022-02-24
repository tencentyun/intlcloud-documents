## Feature Overview
When there is a large number of database tables in a cluster, you can use various features such as account management (account creation and password management) and account authorization (permission modification and deletion) for refined data permission management.

## Account Management
1. Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), click a **Cluster ID/Name** in the cluster list to enter the cluster details page, and switch to the **Account Management** tab.
 ![](https://qcloudimg.tencent-cloud.cn/raw/43de011143bffa6e347231c765e462c7.png)
2. On the **Account Management** tab, you can add and delete cluster system accounts and change passwords. Click **Account Management** to enter the **Account Management** page, where **Add account** is selected for **Database Account** by default. Set the account type, password, and description as prompted and click **OK** to create a database account. You can also change passwords and delete accounts by switching accounts.
 ![](https://qcloudimg.tencent-cloud.cn/raw/825125b1667df568d49e64dfcb74f3f5.png)
>?
>- Account name rule: it can contain 2–16 lowercase letters, digits, and underscores and must start with a letter and end with a letter or digit.
>- Password rule: it must contain 8–30 (preferably more than 12) characters in at least three of the following types: lowercase letters, uppercase letters, digits, and special characters `()!@#$%^&\*|?><` and cannot start with `/`.
>
3. To delete an account, you must first unbind all its authorizations.

## Account Authorization
1. Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), click a **Cluster ID/Name** in the cluster list to enter the cluster details page, and switch to the **Account Management** tab. Click **Account Authorization** to authorize the account (binding V-cluster and granting permissions of databases and tables):
![](https://qcloudimg.tencent-cloud.cn/raw/c69ada62b8540bd095c02ccb459a566d.png)
>?
>- **Access Scope**: you can grant the permissions of all or certain databases and tables.
>- **General Permissions**: the query permission is granted by default. You can also grant the setting and insertion permissions as needed (**setting permissions**: column/index/partition modification, column data modification and deletion, and view/dictionary deletion; **insertion permissions**: column data insertion and view/dictionary creation).
>- **High-Risk Permissions**: you can grant table creation/clearing/deletion and database creation/deletion permissions as needed.
>
2. You can view account authorization records in the authorization list. To modify or revoke permissions, click the corresponding buttons in the **Operation** column.
 ![](https://qcloudimg.tencent-cloud.cn/raw/c811a2662e274cd26bc391bdce6d7240.png)
3. Click **Modify Permissions** to edit the current account's scope of V-cluster database/table permissions, general permissions, and high-risk permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/dbe0f3b85142a17aab56b7eaeb0919cb.png)

## Notes
1. Operations on the account management page involve only SQL accounts but not XML accounts.
2. You can grant one account the permissions of multiple databases/tables in the V-cluster. Each operation generates an authorization record.
3. After authorization, you need to modify the password of the default passwordless XML account to avoid potential security risks.

