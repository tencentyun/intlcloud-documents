## Operation Scenario
By modifying the host address authorized by the database account in the TencentDB for MySQL console, you can control the access to the database to improve the access security.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
2. In the instance list, select the instance to be modified and click the instance name or **Manage** in the **Operation** column to enter the instance management page.
3. Select **Database Management** > **Account Management**, find the account for which to modify the host, and select **More** > **Modify Host**.
![](https://qcloudimg.tencent-cloud.cn/raw/ce35c100d385cc7df8f29e6a0b830ada.png)
4. In the pop-up dialog box for modifying host, enter the new host address and click **OK**.
>The host address may come in the format of an IP address. To allow all the clients to access the database using the database account, enter '%'.
>
![](https://main.qcloudimg.com/raw/113ed501aa7687c9812da29e9314daeb.png)


