
TencentDB for SQL Server adopts the mechanism of "allocate first and use later" for the database space, so there may be free space in the database during use. In this case, you can directly shrink the database in the TencentDB for SQL Server console to save the disk space.

## Shrinking One Database
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select the **Database Management** tab, select the row of the target database, and click **Other** > **Shrink Database** in the **Operation** column.
![](https://main.qcloudimg.com/raw/ffc76302b167d3a198ddcb3310125b07.png)
3. The pop-up window displays the database name and the ratio of remaining space. Currently, only shrinking to 10% of the free space is supported.
>!Only 10% of the database's free space will remain once it has been shrunk. However, if 10% of free space is less than 2 GB, the free space will be shrunk to 2 GB.
>
<img src="https://main.qcloudimg.com/raw/d778ec0f30dfd19ada706dbd2280a84d.png" >
You can view the task progress of database shrinking through **Current Task** in the top-right corner of the **Database Management** tab.
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)

## Batch Shrinking Databases
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID to access the instance management page.
2. On the instance management page, select the **Database Management** tab, select the rows of the target databases, and click **Batch Management** > **Batch Shrink Databases** at the top of the list.
![](https://main.qcloudimg.com/raw/3f2cc7da03c47fdcee08cce3fd804822.png)
3. The pop-up window displays the database names and the ratios of remaining space. Currently, only shrinking to 10% of the free space is supported.
>!Only 10% of the database's free space will remain once it has been shrunk. However, if 10% of free space is less than 2 GB, the free space will be shrunk to 2 GB.
>
<img src="https://main.qcloudimg.com/raw/38ddbb2395dd0f1b54dc5e63ca584180.png" style="zoom:70%;" /><br>
You can view the task progress of database shrinking through **Current Task** in the top-right corner of the **Database Management** tab.
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)

