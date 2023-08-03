
## Overview
In addition to the default root account created by the system, you can also create other database accounts in the TencentDB for MySQL console as needed.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Database Management**> **Account Management** and click **Create Account**.
![](https://qcloudimg.tencent-cloud.cn/raw/76068498b5b5161fcfed90abf39274f3.png)
3. In the pop-up window, enter the account name, host, and password, confirm the password, and click **OK**.
 - **Account Name**:
    - In MySQL 5.5 and 5.6, the database account name can contain 1–16 letters, digits, or underscores. It must begin with a letter and end with a letter or digit.
    - In MySQL 5.7 and 8.0, the database account name can contain 1–32 letters, digits, or underscores. It must begin with a letter and end with a letter or digit.
 - **Host**: Specify a host address to access the database. It can be an IP and contain `%` (indicating no limit on the IP range). Multiple hosts should be separated by line break, space, semicolon, comma, or vertical bar.
    - Example 1: Enter `%` to indicate no limit on the IP range, that is, clients at all IP addresses are allowed to use this account to connect to the database.
    - Example 2: Enter `10.5.10.%`to indicate that clients with an IP range within `10.5.10.%` are allowed to use this account to connect to the database.
 - **Password**: The password must contain 8–64 characters in at least two of the following character types: letters, digits, and special symbols `\_+-&amp;=!@#$%^\*()`. You can also set the password complexity to improve the database security as instructed in [Setting Password Complexity](https://intl.cloud.tencent.com/document/product/236/49197).
 - **Maximum Connections**: The number of connections for this account, which must be no more than 10,240. If you don't enter a value, no limit will be imposed (subject to the maximum number of connections).
4. After successful creation, the database account can be managed in the database account list of the current instance.

## Related APIs

| API Name                                                      | Description     |
| ------------------------------------------------------------ | -------- |
| [CreateAccounts](https://intl.cloud.tencent.com/document/product/236/17502) | Creates a TencentDB account |


