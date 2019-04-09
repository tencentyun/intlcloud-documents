### How do I implement daily auto backup and manual backup in MongoDB?
TencentDB for MongoDB supports two backup methods: daily auto backup and manual backup. Backed-up data is stored in the system for 7 days by default.
 - **Auto backup**
An instance can be automatically backed up once a day. You can view details in **Backup and Rollback** of the instance details page on the [Console of TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb).
- **Manual backup**
In **Backup and Rollback** on the instance details page, click **Manual Backup** in the upper right corner, enter remark information in the pop-up box, and click **Submit** to complete manual backup.

### Can I download backup files?
No.

### Can I restore the file once again if the instance is replaced?
No. The original backup file is no longer available to the replaced instance, so you cannot roll the file back to the previous version anymore. You must double check to make sure that you want to replace the instance. 

### How long does it take to restore a MongoDB instance?
The rollback is based on the latest full backup image and oplog. So the time needed for restoring the instance is determined by the size of oplog to playback.
If the time difference between the start time of the rollback and the time when the full backup is completed is too large, it would take longer for oplog to playback. 

### After restoring a MongoDB instance, what is the difference between a converting and a replacing an instance?
 - Converting an instance means converting the restored temporary instance to a formal instance, and this new instance has no mapping relationship with the original one. By default, the temporary instance is valid for 2 days to convert. Please credit your account in time. 
 - Replacing an instance means overwriting current instance data with the temporary instance data. After the replacement, the backup file of the instance will be deleted and the instance cannot be restored. Please make sure you want to replace the instance.

### Will the backup file be deleted if the MongoDB instance is replaced after being restored?
The original backed-up file is no longer available to the replaced instance. So the backed-up file will be deleted during the rollback.

### How do I back up and roll back a replica set instance in MongoDB?
Sharding cluster instances only support instance-level backup and rollback.
 - **Backup**
On the [console](https://console.cloud.tencent.com/mongodb), click **Manual Backup** in the instance details page, enter remark information, and click **Submit** for instance backup.
 - **Rollback**
You can restore the instance to any point in time within the past 5 days, but you only can specify a time between two backups when the file is successful backed-up and size of oplog is not fully taken up). If none of these conditions is satisfied, please perform [manual backup](https://cloud.tencent.com/document/product/240/7108).

### How do I back up and restore a sharding cluster instance in MongoDB?
Backing up and restoring sharding cluster instances and replica set instances are the same.  You can only back up and restore data at the instance level.
 - **Backup**
On the [console](https://console.cloud.tencent.com/mongodb), click **Manual Backup** on the instance details page, enter remark information, and click **Submit** for instance backup.
 - **Restore**
The oplog space of an instance is a capped collection. When the collection space is used up, newly inserted elements will overwrite the initial head elements. To avoid backup and recovery failures caused by overwritten oplog space, set a reasonable oplog space size according to business requirements. When you frequently write, delete or update data to an instance, you can schedule multiple backups per day to prevent the oplog between two backup points in time from being overwritten, thus ensuring that the data can be restored in time.
