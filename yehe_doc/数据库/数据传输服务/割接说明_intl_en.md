
## Notes
- To better distinguish between sessions and improve data security, we recommend you create a separate database account for data migration.
- To avoid data inconsistency between the source and target databases due to business cutover failures, switch the business in the source database to a backup database before cutover.
- As cutover requires pausing data writes into the source database, we recommend you cut over the business during off-peak hours. 

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration) and proceed based on whether incremental migration is involved:
   - Incremental migration is involved: go to step [2](#step2).
   - Incremental migration is not involved: go to step [6](#step6).
2. [](id:step2)Wait until the **Migration Step** of the data migration task becomes **Syncing Incremental Data**, the source-target database data gap is 0 MB, and the source-target database time lag is 0s.
![](https://qcloudimg.tencent-cloud.cn/raw/c32cafc476ba23e39456ea7cd2219170.png)
3. Pause the business in the source database and stop writing new data.
4. Choose the appropriate code below based on your source database type to view whether there is new session information. If the result shows that no new sessions are being executed except the connection of the DTS migration instance in 1–5 minutes, the business can be considered completely stopped.
 - MySQL 
```
show processlist  
```
 - SQL Server
```
select * from sys.dm_exec_connections;
```
 - PostgreSQL
```
select * from pg_stat_activity;
```
 - MongoDB
```
use admin
db.runCommand({currentOp: 1, $all:[{"active" : true}]})
```
5. Stop the incremental migration task.
View the migration task again, wait for at least 1 minute after the source-target database data gap is 0 MB and the source-target database time lag is 0s, and click **Complete** to stop the incremental migration task.
![](https://qcloudimg.tencent-cloud.cn/raw/1ffcd386bc18f2f7296ff172ded02faa.png)
6. [](id:step6)After confirming that the data in the source and target databases is consistent, determine the cutover time, route the business system to the target database, and resume the business.

