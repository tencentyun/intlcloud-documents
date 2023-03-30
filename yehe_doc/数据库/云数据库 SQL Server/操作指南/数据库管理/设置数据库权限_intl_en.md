## Scenario
TencentDB for SQL Server allows you to grant and modify database account permissions. You cannot modify the permissions of admin and privileged accounts because they have owner permissions of all databases in a TencentDB for SQL Server instance. On the database management page, you can grant other accounts read/write, read-only, or owner permissions of created databases.

## Prerequisites
- You have created an account other than admin or privileged accounts in your TencentDB for SQL Server instance as instructed in [Creating Account](https://intl.cloud.tencent.com/document/product/238/7521).
- You have created at least one database in your TencentDB for SQL Server instance as instructed in [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780).

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/afdf786712bf0a29351a47af34474af5.png)
3. On the instance management page, select **Database Management**, find the target database, and click **Set Permissions** in its **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/8eaadb64e86935c825beac1cf089e579.png)
4. In the pop-up window, select the target account on the left and permissions to be granted on the right and click **OK**.
>?
>- You can batch set permissions. On the database management page, select multiple databases and click **Batch Management** > **Batch Reset Permissions** at the top.
>- Batch resetting permissions will clear all set database account permissions; that is, account permissions of the selected databases will be reset.
>
