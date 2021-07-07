## Operation Scenarios
This document describes how to restore TencentDB for MongoDB data in the console.
>?
>- The oplog space of an instance is a capped collection. When the collection space is used up, newly inserted elements will overwrite the initial header elements. If the oplog space is overwritten, backup and restoration may fail, and it will be impossible to guarantee the time point for data restoration. Therefore, please set a reasonable oplog space size based on your business conditions.
>- Please pay close attention to the **Oplog Time Difference** metric in **System Monitoring** on the instance management page. The smaller the metric value is, the greater the risk of oplog being overwritten when your business has frequent write, update, and deletion operations.


## Prerequisites
The instance data has been backed up. For more information, please see [Backing up Data](https://intl.cloud.tencent.com/document/product/240/7108).

## Directions
1. Log in to the [MongoBD Console](https://console.cloud.tencent.com/mongodb), click an instance ID in the instance list and enter the management page.
2. Select **Backup and Rollback** > **Backup List** and click **Roll back Instance** in the row of the backup file to be rolled back.
![](https://main.qcloudimg.com/raw/b211048c4e8d23bd0f0ebea8c0c6d5f7.png)
3. On the rollback page, you can select the time point to be rolled back to and rollback type (rollback of entire instance or database table rollback).
   - If you select **Rollback of entire instance**, the system will create a temp instance free of charge to store the rollback data. The username and password of the temp instance will be the same as those of the original instance. The original instance will remain unchanged and the business will not be affected.
>?
   >- Within 48 hours since rollback of the whole source instance is completed, you need to access the temp instance to confirm the rolled-back data, and "promote" the temp instance to a formal instance which no longer relies on the source instance and can be accessed by your business normally.
>- If no operation is performed after 48 hours, the temp instance will be terminated by the system.
>
![](https://main.qcloudimg.com/raw/c5dfb5d5a304a3fe67e2cc90322579b8.png)
   - If you select **Database table rollback**, the system will roll back the original instance according to the selected database table, name of the database table after rollback, and rollback time. After the rollback is completed, please confirm the data rolled back promptly.
>?
>- As physical backup does not support database table rollback, you cannot select database table rollback if there is a physical backup in the current backup list.
>- A single database table rollback task currently supports up to 20 database tables.
>- Sharded clusters v3.6 do not support database table rollback.
>
![](https://main.qcloudimg.com/raw/58520ca0f49c7959b22f4e616b0e09a8.png)

