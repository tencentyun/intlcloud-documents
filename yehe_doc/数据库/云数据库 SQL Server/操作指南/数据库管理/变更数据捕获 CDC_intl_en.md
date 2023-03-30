
Change data capture (CDC) is used to capture insertions, updates, and deletion applied to SQL Server tables and provide the details of these changes in a convenient relational format.

The change table used for CDC contains the columns of the column structure of the source table tracked by the image, as well as the metadata required for understanding the changes that have occurred. After CDC is enabled for a table, all DML and DDL operations on it will be recorded, which helps track changes to it.

## Enabling/Disabling CDC for one database
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Database Management** tab, locate the row of the target database and click **Other** > **Enable/Disable CDC** in the **Operation** column.
![](https://main.qcloudimg.com/raw/b527d8852328d14a7a375dc0ab693d76.png)
3. The pop-up window displays the name and current CDC status of the database. After enabling or disabling CDC, click **OK**.
<img src="https://main.qcloudimg.com/raw/ea3716dbfcbbd14eec5a84faa057137a.png" style="zoom:40%;" /><br>
You can view the task progress of enabling or disabling CDC through **Running Tasks** in the top-right corner of the **Database Management** tab.
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />

## Batch enabling/disabling CDC for multiple databases
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID to enter the instance management page.
2. On the instance management page, select the **Database Management** tab, select the rows of the target databases, and click **Batch Management** > **Batch Enable/Disable CDC** at the top of the list.
![](https://main.qcloudimg.com/raw/492b21e192566c64c17917325160182b.png)
3. The pop-up window displays the names and current CDC status of the selected databases. After enabling or disabling CDC, click **OK**.
<img src="https://main.qcloudimg.com/raw/ea3716dbfcbbd14eec5a84faa057137a.png" style="zoom:40%;" /><br>
You can view the task progress of enabling or disabling CDC through **Running Tasks** in the top-right corner of the **Database Management** tab.
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />
