## Overview
If you forgot your database account password or need to change it while using TencentDB for MySQL, you can reset it in the console.
>?
>- For TencentDB for MySQL, the password resetting feature has been connected to [CAM](https://intl.cloud.tencent.com/document/product/236/14469); therefore, we recommend you exercise tighter control over the permission to the password resetting API or sensitive resources of TencentDB for MySQL instances by granting such permission only to appropriate personnel.
>- For data security, we recommend you regularly reset the password at least once every three months.


## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Database Management** > **Account Management**, find the account for which to reset the password, and click **Reset Password** or select **More** > **Reset Password**.
![](https://qcloudimg.tencent-cloud.cn/raw/b162dc614a92c25db597c45581c8fd50.png)
3. In the pop-up window, enter the **New Password** and **Confirm Password** and click **OK**.
>?The password must contain 8–64 characters in at least two of the following character types: letters, digits, and symbols `\_+-&=!@#$%^\*()`.
> 

## Related APIs

| API Name | Description |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) | Modifies the password of TencentDB account |
