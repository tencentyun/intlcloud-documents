## Issue
When you try to connect to a TencentDB for MySQL instance, the system prompts `ERROR 1045 (28000): Access denied for user 'XXX'@'XXX'`.
![](https://main.qcloudimg.com/raw/3283ffcec33f4bdf02aa6ed8cf48ea48.png)

## Possible Causes
1. The username is incorrect.
2. The host name is incorrect.
3. The password is incorrect.

## Solutions
Check whether the username, host, and password are correct.

## Troubleshooting
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click the ID of the target instance in the instance list to enter the instance management page.
2. On the instance management page, select **Database Management** > **Account Management** and check whether the account name and host name match.
>?If the account name and host name do not match, you can proceed as follows:
>- Method 1: Check whether the host has another account name, and if so, use that account name and the corresponding password for login.
>- Method 2: Add the IP address of the current host under the current account name. To clone the account, click **Clone Account** in the **Operation** column of the account, change the **Host** parameter value to the IP address of the host you need to log in to in the **Clone Account** pop-up window, and click **OK**.
>
![](https://main.qcloudimg.com/raw/93d14fbcea9f28269dfb8c0b79c38a22.png)
3. Try again and make sure that the entered password is correct. If you forgot the password, you can find the account for which to reset the password and select **More** > **Reset Password**.
![](https://main.qcloudimg.com/raw/2b7c31670524bc00fa05cfd5181fc018.png)

