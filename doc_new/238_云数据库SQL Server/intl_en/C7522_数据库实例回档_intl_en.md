## Scenario
TencentDB for SQL Server provides a rollback tool for rolling back an instance. Historical data can be re-constructed using periodical image backup and real-time transactions to roll back the instance to a specified time where the time slices of all data are guaranteed to be identical. The full and log backups in TencentDB for SQL Server are retained for 7 days. Therefore, you can roll back the instance data to any time point within the past 7 days. This document describes how to roll back an instance in the console.

## Directions
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver), click the instance name to enter the instance details page, and click **Rollback** in the top-right corner.
![](//mccdn.qcloud.com/static/img/6e9523611eb2bb6574c23bb78f2ed3c3/image.png)
2. Select the database to be rolled back, set the rollback time, decide if the original database should be overwritten, and click **Next**.
![](//mccdn.qcloud.com/static/img/71e6e919e84f6c38e396daed4ea1c7fd/image.png)
3. After confirming that the parameters are correctly set, click **Rollback** to start the rollback task.
4. Return to the instance list. You should see the instance status change to **task in progress**. You can view the rollback progress in the task list.
![](//mccdn.qcloud.com/static/img/6745a9fe2877d953d07de00cfaade272/image.png)
5. The rollback task is successful. As "Overwrite Original Database" was not selected, you can see the generated duplicate database on the database management page.
![](//mccdn.qcloud.com/static/img/5e8c765027e5acea83a52f4b7e8203d2/image.png)
>!
>- Rollback is currently only supported for local instances, and you can choose to overwrite the original database or generate a duplicate database.
>- If you choose to generate a duplicate database, note that the disk capacity after rolling back cannot exceed the disk capacity available for the instance; otherwise, rollback will fail.
