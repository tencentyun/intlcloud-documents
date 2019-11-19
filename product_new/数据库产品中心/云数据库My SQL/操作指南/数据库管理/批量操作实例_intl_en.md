## Batch Rollback

### Operation Scenario
You can roll back databases or tables on the Tencent Cloud platform. Based on cold backup and binlog, rollback operations can be performed in real time. By re-constructing periodical images and real-time transactions, the TencentDB rollback tool can roll back instances or tables to the specified point in time where the time slices of all data are guaranteed to be identical. New databases or tables will be generated from rollback operations, and during the process, original databases or tables can be accessed normally. Upon the completion of rollback, you can see both the new and original databases/tables.

>TencentDB won't change any of your data. Data corrupted due to personal reasons can be recovered through automatic rollback.

### Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. Choose one ore more instances to be rolled back from the instance list and select **More** > **Rollback**.
![](https://main.qcloudimg.com/raw/fd8621340547fdfff3443537af4443c3.png)
3. Select the table to be rolled back and click **Next: set rollback time and database table name**.
![](https://main.qcloudimg.com/raw/b476d0bc95dd980a55a01e1d996a25fa.png)
4. Set the table name and rollback time and click **Roll back**.
> Each instance can be set with only one rollback time.
> 
5. After submission, go to **Operation Logs** > **Rollback Log** where you can view the rollback progress. Click **View Details** to view the rollback log in real time.
![](https://main.qcloudimg.com/raw/568a4a01cd8febbe24ec1eef20343bc0.png)
6. Upon the completion of rollback, select **Database Management** > **Database List** and you can see the new table after rollback in the original instance.


## Batch SQL Operations

### Operation Scenario
This feature allows you to execute SQL statements on multiple selected instances or databases. You can also use this feature to create databases/tables and change table structure in batches so as to initialize or modify multiple instances. To use this feature, make sure that the username and password of the selected instances match.

### Directions
1. Choose one ore more instances for SQL operations from the instance list and select **More** > **SQL Operation**.
![](https://main.qcloudimg.com/raw/90c2878a3176810447c5f560a3a6232e.png)
2. Select the instance or database to be manipulated and click "Next".
![](https://main.qcloudimg.com/raw/3055a0e8d41ce54790dee846105c254f.png)
3. Select an SQL file. If you cannot find the required SQL file, click **Add File** to upload one.
![](https://main.qcloudimg.com/raw/853f1a913cb4260ffdf7645451eb1df8.png)
4. Confirm the instance or database to be manipulated and the SQL file. Then, enter the password after confirming that everything is correct and click **Start**.
![](https://main.qcloudimg.com/raw/0f4628fd30564348c90bb4ad60720fb4.png)
5. After an operation is submitted, view the task information in the **Task List** on the left sidebar.

