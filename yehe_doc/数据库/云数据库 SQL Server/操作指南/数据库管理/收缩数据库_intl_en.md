
TencentDB for SQL Server supports reducing database size by shrinking all database files to release unused space. This document describes how to shrink a database in the TencentDB for SQL Server console.

## Shrinking one database
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Database Management** tab, locate the row of the database to be shrunk and click **Other** > **Shrink Database** in the **Operation** column.
![](https://main.qcloudimg.com/raw/ffc76302b167d3a198ddcb3310125b07.png)
3. The pop-up window displays the database name and the ratio of remaining space. Currently, only shrinking to 10% of the free space is supported.
>!Only 10% of the database's free space will remain once it has been shrunk. However, if 10% of free space is less than 2 GB, the free space will be shrunk to 2 GB.
>
<img src="https://main.qcloudimg.com/raw/d778ec0f30dfd19ada706dbd2280a84d.png" style="zoom:50%;" /><br>
You can view the task progress of database shrinking through **Running Tasks** in the top-right corner of the **Database Management** tab.
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />

## Batch shrinking databases
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Database Management** tab, select the rows of the databases to be shrunk and click **Batch Management** > **Batch Shrink Databases** at the top of the list.
![](https://main.qcloudimg.com/raw/3f2cc7da03c47fdcee08cce3fd804822.png)
3. The pop-up window displays the database name and the ratio of remaining space. Currently, only shrinking to 10% of the free space is supported.
>!Only 10% of the database's free space will remain once it has been shrunk. However, if 10% of free space is less than 2 GB, the free space will be shrunk to 2 GB.
>
<img src="https://main.qcloudimg.com/raw/38ddbb2395dd0f1b54dc5e63ca584180.png" style="zoom:50%;" /><br>
You can view the task progress of database shrinking through **Running Tasks** in the top-right corner of the **Database Management** tab.
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />

