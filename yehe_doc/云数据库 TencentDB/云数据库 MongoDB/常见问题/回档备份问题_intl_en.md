
### How do I perform daily auto backup and manual backup in TencentDB for MongoDB?
TencentDB for MongoDB supports two backup modes: daily auto backup and manual backup. The backup data is retained for 7 days by default.
- **Auto backup**
An instance can be automatically backed up once a day. You can view details in **Backup and Rollback** on the instance details page in the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb).
- **Manual backup**
In **Backup and Rollback** on the instance details page, click **Manual Backup** in the top-right corner, enter remarks in the pop-up box, and click "Submit" to complete manual backup.


### What determines the rollback time of a TencentDB for MongoDB instance?
Rollback is based on the latest full backup image and oplog. The rollback time is subject to the amount of replayed oplogs.
If the rollback is performed a long time after the full backup is completed, it will take more time to replay oplogs.


 
### How do I back up and roll back a replica set instance in TencentDB for MongoDB?
Replica set instances currently support instance-level and database/table-level backup and rollback.
- **Backup**
In the [console](https://console.cloud.tencent.com/mongodb), click **Manual Backup** on the instance details page or set auto backup on the backup and rollback page.
- **Rollback**
You need to enter a date to which you want to roll the instance back. You can enter any time point within the last 5 days, but you can only select a time between two backups (backup succeeds and oplog is not fully occupied). If there are no backups to satisfy this condition, please perform [manual backup](https://intl.cloud.tencent.com/document/product/240/7108).

### How do I back up and roll back a sharded cluster instance in TencentDB for MongoDB?
Sharded cluster instances currently support instance-level backup and rollback.
- **Backup**
In the [console](https://console.cloud.tencent.com/mongodb), click **Manual Backup** on the instance details page or set auto backup on the backup and rollback page.
- **Rollback**
The oplog space of an instance is a capped collection. When the collection space is used up, newly inserted elements will overwrite the initial header elements. To avoid backup and restoration failures caused by overwritten oplog space, please set a reasonable oplog space size based on your business conditions. If your business involves frequent write, deletion, and update operations, you can schedule multiple backups per day to prevent the oplogs between two backup time points from being overwritten. If the oplog space is overwritten, the data restoration time point may not be guaranteed.
