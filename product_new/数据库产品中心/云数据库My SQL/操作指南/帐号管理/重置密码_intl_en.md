## Operation Scenario
This document describes how to reset the instance password in the console.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, select the instance for which to reset the password and click the instance name or **Manage** in the **Operation** column to enter the instance management page.
3. Select **Database Management** > **Account Management**, find the account for which to reset the password, and select **More** > **Reset Password**.
![](https://main.qcloudimg.com/raw/f8ff03d7b57ab9c96231f98920704441.png)
4. In the pop-up dialog box, enter and confirm the new password and then click **OK**.
>
>- For TencentDB for MySQL, the password resetting function has been connected to [CAM](https://intl.cloud.tencent.com/document/product/236/14469); therefore, you are strongly recommended to exercise tighter control over the permission to this API (password resetting) or sensitive resources (i.e., TencentDB for MySQL instances) by granting such permission only to appropriate personnel.
>- It is recommended to reset the database password periodically with an interval of no more than 3 months.
>- The database password should contain 8-64 characters in at least two of the following character types: letters, digits, and special characters (_+-&amp;=!@#$%^*()).
> 
![](https://main.qcloudimg.com/raw/8a2a4d08a1d14cfbcbb683f804bfeb78.png)


## Related APIs

| API Name | Description |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](http://intl.cloud.tencent.com/document/product/236/17497) | Modifies the password of a TencentDB account |

