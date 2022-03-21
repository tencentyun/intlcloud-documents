
Besides the default root account created by the system, you can create other database accounts in the console as needed.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Account Management** tab and click **Create Account**.
![](https://qcloudimg.tencent-cloud.cn/raw/f2d705696fccb1705b8b79b2b813ebd1.png)
3. In the pop-up window, enter the account name, host, password, and confirm password and click **OK**.
 - **Account Name**: the database account name can contain 1–16 letters, digits, and underscores and must begin with a letter and end with a letter or digit.
 - **Host**: specify a host address to access the database. It can be an IP and contain `%` (indicating not to limit the IP range). Multiple hosts should be separated by line breaks, spaces, semicolons, commas, or vertical bars.
    - Example 1: enter `%` to indicate not to limit the IP range, that is, clients at all IP addresses are allowed to use this account to connect to the database.
    - Example 2: enter `10.5.10.%`, which means that clients whose IP range is within `10.5.10.%` are allowed to use this account to connect to the database.
 - **Password**: the password can contain 8–64 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols `~!@#$%^&*_-+=|\(){}[]:;'<>,.?/`.
4. After successful creation, the database account can be managed in the current account list.


