## Preparing the Source and Target Instances
- Before creating a database sync task, you need to enable the binlog feature for the source and target databases and set `binlog_format=row`.
- The capacity of the target database instance must be greater than or equal to the volume of data to be synced.
- You must ensure that the database sync tool can connect to the target database instance.

## Creating a Database Sync Task
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql/synctask).
>Currently, sync tasks of a TDSQL instance need to be created in the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql/synctask) too.
> 
2. On the left sidebar, select **Database Sync** and click **Create Sync Task**.
3. Select the corresponding linkage region and click **Buy at 0 USD**.
4. Go to the creation page, enter the task name, set the source and target database information, and click **Next**.
 - If the target instance type is TencentDB for PostgreSQL, you need to provide an account and password with read/write permission.
 - If the target instance type is CKafka, you need to create a preset service role and grant it data transfer-related permissions. 
 - If the target instance is in Direct Connect, you need to provide an account and password with read/write permission.  
![](https://main.qcloudimg.com/raw/8ffa3678f4216d2f32195038f187e419.png)
5. Select the table name match mode, enter the matched database, and click **Next**.
 - Exact Match: the system will match table names in the source and target databases by using exact match by default.
 - Regex Match: the system will match "exactly identical" table names in the source and target databases by using regex match by default.
>When entering table information, you need to use single quotation marks ('') to enclose the database name, schema name, and table name.
7. Confirm the table match result and click **Next**.
>When data in a TDSQL instance is synced to a CKafka instance or another TDSQL instance, multiple identical tables may be matched in regex match, and this is normal, because there are sharded and broadcast tables and the sync tool will parse each shard.
8. After the verification succeeds, click **Save and Start**. The task will be created and started immediately.
>If the verification fails, you can click the exclamation mark (!) after the specific check item to view the detailed failure information. Then, troubleshoot based on the cause of failure and perform verification again.
> 
![](https://main.qcloudimg.com/raw/ca1bde83613ebcfd0cfe8f8d3d68fdb8.png)
9. The database sync list will be returned, where you can view the database sync task progress.
![](https://main.qcloudimg.com/raw/85dcb059da27bf0bc34d27714884588a.png)
