## Scenario
TencentDB for SQL Server provides a rollback tool for rolling back an instance. Historical data can be re-constructed using periodical image backup and real-time transactions to roll back the instance to a specified time where the time slices of all data are guaranteed to be identical. The full and log backups in TencentDB for SQL Server are retained for 7 days. Therefore, you can roll back the instance data to any time point within the past 7 days. This document describes how to roll back an instance in the console.

## Directions
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver), click the instance name to enter the instance details page, and click **Rollback** in the top-right corner.
![](https://main.qcloudimg.com/raw/f01eb6e4fb2d7f48bf6f1286d5ead820.png)
2. Select the database to be rolled back, set the rollback time, decide if the original database should be overwritten, and click **Next**.
![](https://main.qcloudimg.com/raw/917bc0d8782e54948bd4cd16aa24875e.png)
3. After confirming that the parameters are correctly set, click **Rollback** to start the rollback task.
4. Return to the instance list. You should see the instance status change to **task in progress**. You can view the rollback progress in the task list.
![](https://main.qcloudimg.com/raw/f093a8173aba0d90de8214b5806e5cf7.png)
5. The rollback task is successful. As "Overwrite Original Database" was not selected, you can see the generated duplicate database on the database management page.
![](https://main.qcloudimg.com/raw/b43918abbb177b786a46521ec451f34e.png)

>- Rollback is currently only supported for local instances, and you can choose to overwrite the original database or generate a duplicate database.
>- If you choose to generate a duplicate database, note that the disk capacity after rolling back cannot exceed the disk capacity available for the instance; otherwise, rollback will fail.
