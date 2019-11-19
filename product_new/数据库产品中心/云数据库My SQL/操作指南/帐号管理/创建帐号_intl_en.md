## Operation Scenario
Besides the default root account created by the system, you can create other business accounts in the TencentDB for MySQL Console based on your actual business needs.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, select the instance for which to create an account and click the instance name or **Manage** in the **Operation** column to enter the instance management page.
3. Select **Database Management** > **Account Management** and click **Create Account**.
![](https://main.qcloudimg.com/raw/244439e05841ec094ff337ca56f845c1.png)
4. In the pop-up dialog box, enter the account name, server, password, and confirm password and click **OK**.
 - The database account name can contain 1-16 letters, digits, and underscores (_) and must begin with a letter and end with a letter or digit.
 - The server address authorized to the database account can be an IP and contain "%". Multiple severs should be separated by ";", ",", "|", line breaks, or spaces.
 - The password must contain 8-64 characters in at least two of the following character types: letters, digits, and special characters (_+-&amp;=!@#$%^*()).
![](https://main.qcloudimg.com/raw/2971e6440e3766c0a7d483095dd45f40.png)
5. After successful creation, the database account can be managed in the database account list of the current instance.

## Related APIs

| API Name                                                      | Description     |
| ------------------------------------------------------------ | -------- |
| [CreateAccounts](http://intl.cloud.tencent.com/document/product/236/17502) | Creates A TencentDB account |

