You can create an account for connection to a TencentDB for MariaDB instance. This document describes how to create an account in the TencentDB for MariaDB Console and modify account permissions.
Currently, accounts cannot be created or modified through command line `insert into mysql.user`, `grant`, or `drop`.

## Creating an Account
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql) and click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select the **Account Management** tab and click **Create Account**.
3. In the pop-up dialog box, enter the account name, host, password, and remarks and click **OK** after confirming that everything is correct.
 - **Host**: it supports IP, IP range, and %. % means all the IP addresses within a range. For example, to support all host IPs from 10.10.10.1 to 10.10.10.254, enter `10.10.10.%`.
 **Read-only Account**: if you check this option, the account can only use read-only requests (SELECT).
>You need to set permissions separately for different host IPs under the same account. You can use the **clone account** feature in account management to quickly clone similar accounts and set their permissions.
>
![](https://main.qcloudimg.com/raw/4d258a894b25f00d04359234add787fc.png)

## Setting Permissions
1. On the account management page, click **Modify Permission** in the "Operation" column.
![](https://main.qcloudimg.com/raw/d99d1c24ead8d610a8fd50cc723e3793.png)
2. In the pop-up dialog box, grant permissions based on your needs and click **Save Configuration**.
The permissions in TencentDB for MariaDB are defined at the object level and include 19 common database permissions. You can set permissions for objects such as tables, views, functions, and triggers.
>You need to create a database first before you can set object-level permissions.
>
![](https://main.qcloudimg.com/raw/694d08a5d3c1c491f1b263122400845f.png)

