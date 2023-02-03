## Overview
If you forgot your database account password or need to modify it while using TencentDB for MariaDB, you can reset it in the console.

>? We recommended that you regularly reset the password at least once every three months for the sake of data security.

## Directions
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Account Management** tab, find the account for which to reset the password, and select **More** > **Reset Password**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/bjYK945_11.png)
3. In the pop-up window, enter the **New Password** and **Confirm Password** and click **OK**.
>? To avoid the risks caused by creating, modifying, and deleting account information, we recommend that you configure [access management] (https://intl.cloud.tencent.com/document/product/237/35441), and reset the password with caution.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/M7Xa115_12.png)

## Related APIs

| API Name | Description |
| ------------------------------------------------------------ | ------------ |
| [ResetAccountPassword](https://intl.cloud.tencent.com/document/product/237/16168) | Resets account password |

