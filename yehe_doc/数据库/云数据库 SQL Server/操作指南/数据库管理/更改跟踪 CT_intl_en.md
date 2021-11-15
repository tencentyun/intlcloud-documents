
Change tracking (CT) can be applied to track a specific table or even column in a database. When you perform an addition, modification, or deletion operation in a table with CT enabled, the system will automatically generate a version number for the operation and record the operation information, including the operation timestamp, operation type, and primary key of the affected data.

CT only records whether the rows in the table have been changed but not the changed data, so it has little impact on the performance of data operations. Such information will be recorded in the SQL Server system table and automatically cleared and maintained by the system.

## Enabling/Disabling CT for One Database
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select the **Database Management** tab, select the row of the target database, and click **Other** > **Enable/Disable CT** in the **Operation** column.
![](https://main.qcloudimg.com/raw/521e8a6f5d36f2b2d29ca4cf0fa72ef2.png)
3. The pop-up window displays the name and current CT status of the database. After enabling or disabling CT, click **OK**. If you enable CT, you can set the data retention period.
![](https://main.qcloudimg.com/raw/bf32e15a168c9d43a69655f0df209558.png)
You can view the task progress of enabling or disabling CT through **Current Task** in the top-right corner of the **Database Management** tab.
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)

## Batch Enabling/Disabling CT for Multiple Databases
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID to access the instance management page.
2. On the instance management page, select the **Database Management** tab, select the rows of the target databases, and click **Batch Management** > **Batch Enable/Disable CT** at the top of the list.
![](https://main.qcloudimg.com/raw/90ee38dc0216b446a52ea238819a31e4.png)
3. The pop-up window displays the names and current CT status of the databases. After enabling or disabling CT, click **OK**. If you enable CT, you can set the data retention period.
![](https://main.qcloudimg.com/raw/bf32e15a168c9d43a69655f0df209558.png)
You can view the task progress of enabling or disabling CT through **Current Task** in the top-right corner of the **Database Management** tab.
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)
