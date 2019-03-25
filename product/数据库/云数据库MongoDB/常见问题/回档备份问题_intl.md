
### How do I perform daily auto backup and manual backup in MongoDB?
TencentDB for MongoDB supports two backup methods: daily auto backup and manual backup. The backup data is kept for 7 days by default.
- **Auto backup**
An instance can be automatically backed up once a day. You can view details in **Backup and Rollback** of the instance details page on the [Console of TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb).
- **Manual backup**
In **Backup and Rollback** on the instance details page, click **Manual Backup** in the upper right corner, enter remark information in the pop-up box, and click **Submit** to complete manual backup.

### Can I download backup files?
No.

### Can I perform rollback again if the instance is replaced after rollback?
No. The original backup file is no longer applicable to the replaced instance, so you cannot perform rollback again. You must perform the replacement operation with caution.

### What determines the rollback time of a MongoDB instance?
Rollback is based on the latest full backup image + oplog. The rollback time is determined by the amount of oplog playback.
If the rollback is performed a long time after the full backup is completed, it will take much time for oplog playback.

### After rollback of a MongoDB instance, what is the difference between a conversion operation and a replacement operation?
Conversion is to convert the rolled-back temporary instance to a formal instance, which has no mapping relationship with the original one. By default, the temporary instance has a validity period of 2 days. Please renew in time.
Replacement is to overwrite the current instance data with the temporary instance data. After replacement, the backup file of the instance will be deleted and the instance cannot be rolled back. Please proceed with caution.

### Will the backup file be deleted if the MongoDB instance is replaced after rollback?
The original backup file is no longer applicable to the replaced instance. So the backup file will be deleted during the rollback.
 
### How do I back up and roll back a replica set instance in MongoDB?
Sharding cluster instances only support instance-level backup and rollback.
- **Backup**
On the [console](https://console.cloud.tencent.com/mongodb), click **Manual Backup** in the instance details page, enter remark information, and click **Submit** for instance backup.
- **Rollback**
You need to enter a date to which you want to roll the instance back. You can enter any time point within the past 5 days, but you can only select a time between two backups (successful backup and oplog is not fully occupied). If there is no backup to satisfy this condition, please perform [manual backup](https://cloud.tencent.com/document/product/240/7108).

### How do I back up and roll back a sharding cluster instance in MongoDB?
Backup and rollback operations in sharding cluster instances are the same with those in replica set instances. You can only back up and roll back data at the instance level.
- **Backup**
On the [console](https://console.cloud.tencent.com/mongodb), click **Manual Backup** in the instance details page, enter remark information, and click **Submit** for instance backup.
- **Rollback**
The oplog space of an instance is a capped collection. When the collection space is used up, new inserted elements will overwrite the initial head elements. To avoid backup and recovery failures caused by overwritten oplog space, set a reasonable oplog space size according to business details. When a business involves frequent write, delete and update operations, you can schedule multiple backups per day to prevent the oplog between two backup time points from being overwritten. If the oplog space between two backup time points is overwritten, the data recovery time may not be guaranteed.

