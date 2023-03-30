
## Scenario
TencentDB for SQL Server provides a rollback tool for rolling back an instance. Historical data can be re-constructed by using the periodical backups and real-time transactions so as to roll back the instance to a specified time point where the time slices of all data are guaranteed to be identical.
The retention period of TencentDB for SQL Server data backups is seven days by default and can be customized. The retention period of log backups is the same as that of data backups. You can roll back the instance data to any time point within the configured backup retention period. This document describes how to roll back an instance in the console.


## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click an instance ID to enter the instance details page, and click **Rollback** in the top-right corner.
2. In the pop-up window, select the database to be rolled back, set the rollback time, decide whether to overwrite the original database, and click **Next**.
>!
>- Rollback is currently only supported for the same instance, and you can choose to overwrite the original database or generate a duplicate database.
>- If you choose to generate a duplicate database, note that the disk space after rollback cannot exceed the disk space available for the instance; otherwise, rollback will fail.
>
![](https://main.qcloudimg.com/raw/917bc0d8782e54948bd4cd16aa24875e.png)
3. After confirming that the rollback information is correct, click **Rollback** to start the rollback task.
4. Return to the instance list, and you can see that the instance status changes to **Running task**. You can view the rollback progress in the task list in the top-right corner on the details page.
![](https://main.qcloudimg.com/raw/f093a8173aba0d90de8214b5806e5cf7.png)
5. After the rollback task succeeds, you can see the generated database on the **Database Management** tab.
