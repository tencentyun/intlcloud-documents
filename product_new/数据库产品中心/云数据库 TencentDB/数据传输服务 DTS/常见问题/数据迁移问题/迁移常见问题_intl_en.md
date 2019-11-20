### Does DTS support data migration between TencentDB instances under two different Tencent Cloud accounts?
Yes. For that purpose, you need to log in to the DTS Console with the Tencent Cloud account of the target TencentDB instance and select self-built database with public IP as the source instance type.

### Can I monitor the progress of database migration tasks?
Yes. You can log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page) and open the "Data Migration" page to do so.

### Will DTS delete the data in the source database after migration?
No. When DTS performs data migration, it simply replicates the data of the source database with no impact on it.

### Does DTS support scheduled automatic migration?
Yes. When modifying the configuration for a created data migration task, you can select scheduled migration and specify the start time.

### Which version of Redis instances can be migrated?
Source instances on version 3.2 or above cannot be migrated.

### When will the instance be restarted during MySQL migration?
- For migration of full instance, the parameters will be synced, and one restart is required for the parameters to take effect.
- For migration of some tables, `replicate_do_table` will be set, and there will be one restart.

### Will the tables be locked during MySQL migration?
- For InnoDB, short table locking is required to get the consistent time point after your long-running transactions end.
- For MyISAM, all tables will be locked until cold backup is completed.

### Which MySQL versions are supported for data migration?
MySQL 5.1, 5.5, 5.6, and 5.7. As TencentDB no longer supports MySQL 5.1, you are recommended to upgrade MySQL 5.1 to MySQL 5.5 first and then migrate data to TencentDB for MySQL 5.5. You can also use DTS to directly migrate from a local MySQL 5.1 instance to a TencentDB for MySQL 5.5 instance.
In addition, the following restrictions apply:
- Currently, migration is supported between MySQL 5.6 and 5.7 instances but not between MySQL 5.5 and 5.7 instances.
- Virtual columns and JSON in MySQL 5.7 instances are not supported.
  
### Are TencentDB for MySQL Basic Edition instances supported for migration?
 - TencentDB for MySQL Basic Edition instances can be migrated as source instances over the public network but not the private network.
 - They cannot be used as target instances currently.

### What if the connectivity check fails?
You can click **View Details** to find a possible solution.

### Why is a target instance unavailable?
Possible reasons include:
1. It is not initialized.
2. It is locked by another task.
3. It has data.
4. Its capacity is smaller than the data volume in the source instance.

### Why does a warning occur when I check a task?
You can click **View Details** on the right of the warning to view the cause and solution.

### Why does an error occur during migration and cause the migration task to fail?
- The BGSAVE operation on the source instance failed during migration.
- During migration, the volume of data written to the source instance is too large and exceeds the configured sync buffer, which causes the migration task to continuously retry establishing the sync connection and generate RDB.

### Why is there a 15-day limit on incremental migration?
Currently, incremental migration is performed through the nearest proxy server via Tencent Cloud Direct Connect, which eliminates network jitters and ensures the quality of data transfer. The 15-day limit can reduce the connection pressure on the proxy server and is only intended for reasonable utilization of resources for migration. Currently, connections will not be force closed after 15 days.

### Why is some data missing in a target instance where the subscription feature is enabled?
As cold backup needs to be imported during migration, `binlog` is disabled for higher write performance, resulting in loss of some data. To prevent data loss, you need to create a migration task first, confirm that the target instance is in sync, and then set the subscription feature for it.

### What if the TokuDB engine is used in the source instance?
In this case, TokuDB will be converted to InnoDB by default during migration. As tables containing clustered indices or compressed with TokuDB need to be pre-processed before migration, they are not supported currently. DDL operations on TokuDB are not supported either.

### Why does the error about super permission occur for full check during migration?
This is because session needs to be in binlog format for full check, which requires super permission. The solution is as follows:
1. Super permission is not required for spot check.
2. Grant the super permission to the account.

### Why does an error occur during DTS task check for TokuDB table migration?
TokuDB cannot be converted to InnoDB if there are tables compressed with TokuDB or containing clustered index in the source instance.


