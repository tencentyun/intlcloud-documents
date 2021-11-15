
## Overview
TencentDB for MySQL will not alter any of your data. Data corrupted due to personal reasons can be recovered through rollback in a self-service manner. A rollback feature is provided to roll back databases or tables in Tencent Cloud based on data backup and binlog backup. Real-time data rollback is supported.

By re-constructing periodical images and real-time transactions, the TencentDB for MySQL rollback feature can roll back a database or table to the specified point in time and the time slices of all data are guaranteed to be identical. A new database or table will be generated in the original instance, and during the process, the original database or table can be accessed normally. Upon the completion of rollback, you can see both the new and original databases or tables.

## How Rollback Works
The rollback feature can roll back databases or tables to a specified point in time based on `cold data backup and corresponding binlog backup`.
![](https://main.qcloudimg.com/raw/89ab32296ba576cf8e087d760b5a8109.png)
1. Data is exported from the MySQL replica and imported to the cold backup system daily.
2. To roll back databases or tables, request for a temp rollback instance from the rollback system. Export the cold data from the cold backup system and import it to the temp rollback instance (types of imported data vary with the rollback methods).
3. Establish a source-replica relationship between the rollback instance and MySQL source instance, set the rollback time, and specify the databases or tables to be rolled back.
4. Replicate the databases or tables after rollback to the MySQL source instance.

## Feature Limits
- Only source instances can be rolled back. Read-Only replicas or disaster recovery instances cannot be rolled back.
- Only specified databases or tables can be rolled back. The databases or tables after rollback will be renamed and replicated to the source instance.

## Notes
- The rollback feature is subject to the backup cycle and retention days set for automatic backup. It enables data rollback based on data backup and binlog backup according to the configured retention days and backup cycle. For the backup cycle settings, please see [Backing up MySQL Data Automatically](https://intl.cloud.tencent.com/document/product/236/37796). To ensure MySQL data security, set the automatic backup cycle to at least twice a week.
- If the database or table to be rolled back does not exist or has been dropped, you need to log in to the TencentDB instance and create one first before performing rollback in the console.
- If the cold backup before rollback does not contain the table, the rollback will fail.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, select one or more instances and click **More** > **Rollback**.
>?
>- If rollback is to be performed on only one instance, you can also go to the instance management page and click **Rollback** in the top-right corner.
>- Up to 5 rollback tasks can be initiated at a time under the same APPID.
>
![](https://main.qcloudimg.com/raw/abd517cf8b6db3db57b622f13d365893.png)
2. On the rollback page, set the rollback method (described as below), select databases or tables to be rolled back, and click **Next step: set the rollback time and database table name**.
   - Fast: full backup of the instance is imported, and the selected databases or tables are rolled back. This rollback mode is slow but has no limit.
   - Faster: full backup and database-level binlogs are imported. For cross-database operation, if the associated database is not selected at the same time, rollback may fail.
   - Ultrafast: full backup and table-level binlogs are imported. For cross-table operation, if the associated table is not selected at the same time, rollback may fail.
>?
>- Only databases/tables whose name contains digits, letters, underscores, or their combinations can be rolled back. Databases/tables with names containing special characters are not supported.
>- In the mode where specified databases/tables can be rolled back only, a maximum of 500 databases/tables in the same instance can be rolled back at a time.
>- If the rollback involves composite operations on other databases or tables during the execution of binlogs, the SQL statements may fail.
>- If the rollback involves foreign keys and other constraints of the table during the execution of binlogs, the SQL statements may fail.
>
![](https://main.qcloudimg.com/raw/6cb2fa4d3e8b0d795bd5bf19f8d69d86.png)
3. Set the post-rollback database or table name and rollback time, and click **Rollback**.
>?
>- Only one rollback time can be set for each instance.
>- If you choose to set a batch rollback time, all databases or tables will be rolled back at the specified time.
>- If you choose to set a single-table rollback time, tables will be rolled back at their respective rollback time.
>- The database or table name after rollback can contain up to 64 letters, digits, or symbols (.-\_$).
>
![](https://main.qcloudimg.com/raw/62377981b147bdb453d79631b3557d12.png)
4. After submission, go to **Operation Log** > **Rollback Log** to view the rollback progress. Click **View Details** to view the rollback log in real time.
![](https://main.qcloudimg.com/raw/b5206b3c23d532553fb54dfc4fe7bfd0.png)
5. Once the rollback completes, go to **Database Management** > **Database List** to view the new database or table after rollback in the original instance.
![](https://main.qcloudimg.com/raw/9b939d9a6a7da59092df0051f452b5cd.png)

