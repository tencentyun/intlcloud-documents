## Operation Scenarios
If you forgot your database account password or need to change it while using TencentDB for MySQL, you can reset it in the console.
>
>- For TencentDB for MySQL, the password resetting function has been connected to [CAM](https://intl.cloud.tencent.com/document/product/236/14469); therefore, you are recommended to exercise tighter control over the permission to the password resetting API or sensitive resources of TencentDB for MySQL instances by granting such permission only to appropriate personnel.
>- For data security, you are recommended to regularly reset the password at least once every three months.


## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, select the instance for which to reset the password and click the instance name or **Manage** in the **Operation** column to enter the instance management page.
3. Select **Manage Database** > **Manage Account**, find the account for which to reset the password, and select **More** > **Reset Password**.
![](https://main.qcloudimg.com/raw/f8ff03d7b57ab9c96231f98920704441.png)
4. In the pop-up dialog box, enter and confirm the new password and then click **OK**.
> The database password should contain 8–64 characters in at least two of the following character types: letters, digits, and special symbols (_+-&=!@#$%^*()).
> 
![](https://main.qcloudimg.com/raw/8a2a4d08a1d14cfbcbb683f804bfeb78.png)

## Related APIs

| API Name | Description |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) | Modifies the password of a TencentDB account |
