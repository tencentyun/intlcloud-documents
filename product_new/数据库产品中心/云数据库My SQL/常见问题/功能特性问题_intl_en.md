### What preparations do I need to make before using TencentDB for MySQL?
Before using TencentDB for MySQL, you need to consider the following two questions:
- Is a database suitable for your application? For example, for scenarios with small data volume, high access traffic, and key-value storage, a memory-level persistent storage service is recommended.
- Is your database appropriately designed? For example, you should consider splitting a table with obvious query hotspots or high data volume into multiple tables.

### How does TencentDB for MySQL manage MySQL?
You don't need to care about the daily maintenance and adjustment of MySQL, which is taken care of by the OPS system of TencentDB.
In case of an exception with MySQL, the OPS system can identify it and notify the OPS personnel immediately, and you don't need to make any changes.

### Is there a physical machine behind TencentDB for MySQL?
Yes.

### Can TencentDB for MySQL help me split databases and tables?
No, because the standards for splitting databases and tables are subject to your specific business logic.

### What is the difference between occupied capacity and used capacity in TencentDB for MySQL?
The capacity actually used by your data and the capacity occupied by log data such as binlogs are calculated separately. The occupied capacity displayed in the TencentDB for MySQL Console equals the used capacity.

### Does TencentDB for MySQL have any buffer during task execution?
**Q:**
If multiple SQL statements are sent to TencentDB for execution within a very short period of time, will TencentDB for MySQL run them one by one or crash? What is the maximum number of allowed concurrent connections?
**A:**
A TencentDB for MySQL instance works in the same way as a self-built MySQL instance. Whether concurrently executed statements will cause a crash depends on system resources and SQL statements themselves.
When the number of connections reaches the upper limit (max_connections), the instance will basically not able to provide services properly. This is generally caused by the following reasons:
- There are too many null sessions caused by bugs in the business application;
- Frontend access goes far beyond the instance's processing capability;
- A connection which is executed for too long takes up MySQL resources exclusively, resulting in a large number of blocked access requests.

### What are the precautions for using TencentDB for MySQL?
For specific precautions, see [Use Limits](http://intl.cloud.tencent.com/document/product/236/7259).

### How to apply for enabling or disabling the read-only permission to the default standby database of TencentDB for MySQL?
Instead of providing external access, the default standby database is primarily used for high-availability switchover.

<span id = "congkufangwen"></span>

### Does TencentDB for MySQL support slave database access? 
For the sake of database security (for example, when the master instance fails, you can quickly switch to the slave database), TencentDB for MySQL doesn't allow you to read from or write to the slave database.
If greater read/write capability is desired, you can consider upgrading the instance configuration or purchasing a [read-only instance](http://intl.cloud.tencent.com/document/product/236/7270).

<span id = "genghuandiyu"></span>
### How to change the TencentDB for MySQL region?
Region change is not supported for the time being. You can use [DTS](http://intl.cloud.tencent.com/document/product/571/13706) to migrate data between instances in different regions. DTS supports real-time data sync. After data migration is completed, the source instance can be returned in a self-service manner.

<span id = "shilixiaohui"></span>
### What if a TencentDB for MySQL instance is terminated?
After termination, a monthly subscribed instance will be retained in the recycle bin for 7 days, and a pay-as-you-go instance for 1 day. During the retention period, terminated instances can be recovered from the recycle bin.

<span id = "zhanghaomima"></span>
### What if I accidentally delete an account or forgot the password?
- If an account is deleted accidentally, click **Database Management** > **Account Management** > **Create Account** on the instance management page or create an account using an SQL statement.
- If the password is forgotten, find the corresponding account in **Database Management** > **Account Management** and reset the password in **Reset Password**.
The above operations can also be performed through [TencentCloud API](http://intl.cloud.tencent.com/document/product/236/17497).

<span id = "myisam"></span>
### What if I need to use the MyISAM database engine?
You can use MySQL v5.5 which supports MyISAM. Even so, you are recommended to choose a higher version like MySQL v5.7, as the InnoDB engine can provide finer-grained row-level locking, deliver a higher write performance, guarantee data integrity, and avoid data loss in case of database failure.

<span id = "kuadiyufangwen"></span>
### Does TencentDB for MySQL support cross-region access? 
Cross-region access is unavailable in VPC by default, as VPCs in different regions are isolated from each other. You are recommended to purchase TencentDB for MySQL instance in the same region as your CVM instances, so that local access can be enabled for data, which guarantees high service speed and stability.

