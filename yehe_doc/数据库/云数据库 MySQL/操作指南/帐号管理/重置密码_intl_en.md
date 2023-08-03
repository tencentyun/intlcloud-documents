
## Overview
If you forgot your database account password or need to change it while using TencentDB for MySQL, you can reset it in the console.
>?
>- For TencentDB for MySQL, the password resetting feature has been connected to [CAM](https://intl.cloud.tencent.com/document/product/236/14469); therefore, we recommend that you exercise tighter control over the permission to this API (password resetting) or sensitive resources (i.e., TencentDB for MySQL instances) by granting such permission only to appropriate personnel.
>- For data security, we recommend that you regularly reset the password at least once every three months.


## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select **Database Management** > **Account Management**, find the account for which to reset the password, and click **Reset Password** or select **More** > **Reset Password**.
![](https://qcloudimg.tencent-cloud.cn/raw/b162dc614a92c25db597c45581c8fd50.png)
3. In the pop-up window, enter a new password and confirm the password and click **OK**.
>? The password should be a combination of 8–64 characters containing at least two of the three types: letters, digits, and symbols (_+-&=!@#$%^*()).
> 

## Related APIs

| API Name | Description |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) | Modifies the password of a TencentDB account |
