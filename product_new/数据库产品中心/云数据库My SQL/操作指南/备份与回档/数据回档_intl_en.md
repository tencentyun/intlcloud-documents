## Operation Scenario
TencentDB will not alter any of your data. Data corrupted due to personal reasons can be recovered through rollback in a self-service manner. A rollback tool is provided to roll back databases or tables in Tencent Cloud based on cold backup and binlog, and real-time data rollback is supported.

By re-constructing periodical images and real-time transactions, the TencentDB rollback tool can roll back a database or table to the specified point in time where the time slices of all data are guaranteed to be identical. A new database or table will be generated in the original instance by the rollback operation, and during the process, the original database or table can be accessed normally. Upon the completion of rollback, you can see both the new and original databases/tables.

## Prerequisites
The rollback feature is correlated with backup cycle and retention period settings and only supports rollback to any point in time within the past 7 days for daily backup. For backup cycle settings, see [Backup Method](https://intl.cloud.tencent.com/document/product/236/7513).

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. Choose one ore more instances to be rolled back from the instance list and select **More** > **Rollback**.
>
>- If rollback is to be performed on only one instance, you can also go to the instance management page and click **Rollback** in the top-right corner.
>- A maximum of 500 tables in the same instance can be rolled back at a time.
>- Up to 5 rollback tasks can be initiated at a time under the same APPID.
>
![](https://main.qcloudimg.com/raw/85f08362342f02fb27ded34a487b4090.png)
3. Select the table to be rolled back and click **Next step: set the rollback time and database table name**.
>
>- Only tables whose name contains digits, letters, underscores, or their combinations can be rolled back, while those whose name contains special characters are not supported.
>- If the table to be rolled back has been dropped, you need to log in to the TencentDB instance and create a table first before performing rollback in the console.
>
![](https://main.qcloudimg.com/raw/6cb2fa4d3e8b0d795bd5bf19f8d69d86.png)
4. Set the post-rollback table name and rollback time and click **Rollback**.
>
>- Each instance can be set with only one rollback time.
>- The table name after rollback can contain up to 64-bit letters, digits, decimal points (.), dashes (-), underscores (_), and $.
>
![](https://main.qcloudimg.com/raw/62377981b147bdb453d79631b3557d12.png)
5. After submission, go to **Operation Log** > **Rollback Log** where you can view the rollback progress. Click **View Details** to view the rollback log in real time.
![](https://main.qcloudimg.com/raw/b5206b3c23d532553fb54dfc4fe7bfd0.png)
6. Upon the completion of rollback, select **Database Management** > **Database List** and you can see the new table after rollback in the original instance.
![](https://main.qcloudimg.com/raw/9b939d9a6a7da59092df0051f452b5cd.png)

