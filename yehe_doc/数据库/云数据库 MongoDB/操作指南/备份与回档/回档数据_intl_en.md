This document describes how to restore TencentDB for MongoDB data in the console.

## Background
To restore the backup data, you can roll back the databases and tables in the console. To restore the data of an entire instance, you can clone the instance.

## Version Description
The current sharded cluster version does not support database and table rollback but only supports instance clone. For detailed directions, see [Cloning Instance](#klsl).

## Notes
- The oplog space of an instance is a capped collection. When the collection space is used up, newly inserted elements will overwrite the initial header elements. If the oplog space is overwritten, backup and restoration may fail, and it will be impossible to guarantee the time point for data restoration. Therefore, set a reasonable oplog space size based on your business conditions.
- Pay close attention to the **Oplog Time Difference** metric in **System Monitoring** on the instance management page. The smaller the metric value, the greater the risk of oplog being overwritten when your business has frequent write, update, and deletion operations.

## Use Limits
- You can select up to 2,000 tables per instance to roll back.
- Sharded clusters don't support database table rollback but only support instance clone.
- Physical backups cannot be used to roll back databases/tables.
- You can roll back data to any time point in the last 7 days.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.
- You have performed logical backup to [back up data](https://intl.cloud.tencent.com/document/product/240/7108).

## Directions
### [Cloning instance](id:klsl)
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Backup and Rollback** > **Backup Task List** page.
7. In the **Backup Task List**, find the backup file to be restored.
8. Click **Clone** in the **Operation** column.
9. On the **Clone TencentDB for MongoDB Instance** page, select configuration items such as billing mode and configuration specification of the new instance. For more information, see [Creating TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/3551).
10. Confirm the order, click **Buy Now**, return to the instance list page, wait for the instance to be created, and then you can use it.

### Rolling back database table
1. On the **Instance Details** page, select the **Backup and Rollback** tab.
2. On the **Backup and Rollback** tab, select the **Backup Task List**.
3. In the **Backup Task List**, find the backup file to be restored.
4. Click **Database table rollback** in the **Operation** column.
![](https://main.qcloudimg.com/raw/b211048c4e8d23bd0f0ebea8c0c6d5f7.png)
5. On the **Batch select databases/tables** page in the **Database table rollback** configuration guide, select the database tables to be rolled back as described below:
<table>
<thead><tr><th>Parameter</th><th>Required</th><th>Description</th></tr></thead>
<tbody><tr>
<td><strong>Search Instance</strong></td>
<td>No</td>
<td>Select the target instance to which the backup data is to be rolled back. You can select the newly cloned instance or current instance. If you want to restore the backup data to the cloned instance, the cloned instance must be in a different AZ in the same region as the current instance.</td></tr>
<tr>
<td><strong>Rollback Method</strong></td>
<td>No</td>
<td>The default value is <strong>database table rollback</strong>.</td></tr>
<tr>
<td><strong>Select Rollback Table</strong></td>
<td>Yes</td>
<td>Select the database tables to be rolled back.</td></tr>
</tbody></table>
6. Click **Next: set the rollback time and database table name** to set the rollback time and database table name after rollback.
7. Click **Complete** and select the **Rollback Task List** tab to view the rollback task progress.
8. Wait for the task to be completed and confirm the rollback data.

