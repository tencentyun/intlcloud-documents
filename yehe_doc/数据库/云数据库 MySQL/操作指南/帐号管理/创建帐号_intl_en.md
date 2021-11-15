
## Overview
Besides the default root account created by the system, you can create other database accounts in the TencentDB for MySQL console based on your actual business needs.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance name/ID or **Manage** in the **Operation** column and enter the instance management page.
2. Select **Manage Database** > **Manage Account** and click **Create**.
![](https://main.qcloudimg.com/raw/244439e05841ec094ff337ca56f845c1.png)
3. In the pop-up dialog box, enter the account name, server, password, and confirm password and click **OK**.
 - **Account Name**: the database account name can contain 1-16 letters, digits, and underscores (_) and must begin with a letter and end with a letter or digit.
 - **Server**: the host address can be an IP and contain `%` (indicating not to limit the IP range). Multiple hosts should be separated by line breaks, spaces, semicolons, commas, or vertical bars.
    - Example 1: enter `%` to indicate not to limit the IP range, that is, clients at all IP addresses are allowed to use this account to access the database.
    - Example 2: enter `10.5.10.%`, which means that clients whose IP range is within `10.5.10.%` are allowed to use this account to access the database.
 - **Set Password**: the password must contain 8-64 characters in at least two of the following character types: letters, digits, and special characters (_+-&amp;=!@#$%^*()).
![](https://main.qcloudimg.com/raw/2971e6440e3766c0a7d483095dd45f40.png)
4. After successful creation, the database account can be managed in the database account list of the current instance.

## Related APIs

| API Name                                                      | Description     |
| ------------------------------------------------------------ | -------- |
| [CreateAccounts](https://intl.cloud.tencent.com/document/product/236/17502) | Creates a TencentDB account |


