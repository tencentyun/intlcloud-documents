## Operation Scenarios
If you forgot your database account password or need to change it while using TencentDB for MySQL, you can reset it in the console.
>?
>- For TencentDB for MySQL, the password resetting function has been connected to [CAM](https://intl.cloud.tencent.com/document/product/236/14469); therefore, you are recommended to exercise tighter control over the permission to the password resetting API or sensitive resources of TencentDB for MySQL instances by granting such permission only to appropriate personnel.
>- For data security, you are recommended to regularly reset the password at least once every three months.


## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Database Management** > **Account Management**, find the account for which to reset the password, and select **More** > **Reset Password**.
![](https://qcloudimg.tencent-cloud.cn/raw/cbb345bf5ecd9dfa0e4b117c698db6d8.png)
3. In the pop-up dialog box, enter and confirm the new password and then click **OK**.
>?The database password should contain 8–64 characters in at least two of the following character types: letters, digits, and special symbols (\_+-&=!@#$%^\*()).
> 


## Related APIs

| API Name | Description |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) | Modifies the password of TencentDB account |
