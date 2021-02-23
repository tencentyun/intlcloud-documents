
### What preparations do I need to use TencentDB for MySQL?
Before using TencentDB for MySQL, you need to consider the two questions:
- Is a database suitable for your application? For example, for scenarios with small data volume, high access traffic, and key-value storage, a memory-level persistent storage service is recommended.
- Is your database appropriately designed? For example, you should consider splitting a table with obvious query hotspots or high data volume into multiple tables.

### How does TencentDB for MySQL manage MySQL?
You don't need to worry about the daily maintenance and adjustment of MySQL, which is taken care of by the OPS system of TencentDB.
In case of an exception with MySQL, the OPS system can immediately identify the issue and notify the OPS team. Developers will not need to make any changes.

### Is there a physical machine behind TencentDB for MySQL?
Yes.

### Can TencentDB for MySQL help me split databases and tables?
No, because the standards for splitting databases and tables are subject to your specific business logic.

### What is the difference between occupied capacity and used capacity in TencentDB for MySQL?
The capacity actually used by your data and the capacity occupied by log data such as binlogs are calculated separately. The occupied capacity displayed in the TencentDB for MySQL Console equals the used capacity.

### Does TencentDB for MySQL have any buffer during task execution?
**Question:**
If multiple SQL statements are sent to TencentDB for execution within a very short period of time, will TencentDB for MySQL run them one by one or crash? What is the maximum number of allowed concurrent connections?
**Answer:**
A TencentDB for MySQL instance works in the same way as a self-built MySQL instance. Whether concurrently executed statements will cause a crash depends on system resources and SQL statements themselves.
When the number of connections reaches the limit (max_connections), the instance will not provide services normally. This happens generally due to the following reasons:
- There are too many null sessions caused by bugs in the business application;
- Frontend access goes far beyond the instance's processing capability;
- A connection which is executed for too long takes up MySQL resources exclusively, resulting in a large number of blocked access requests.

### What are the precautions for using TencentDB for MySQL?
For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/236/7259).

### How do I enable or disable the read-only permission to the default replica of TencentDB for MySQL?
The default replica cannot be read from or written to. It is primarily used for high-availability switchover.

### Which monitoring metrics of the instance should I pay attention to?
CPU utilization, memory utilization, and disk space utilization. You can [configure alarms](https://intl.cloud.tencent.com/document/product/236/8457) as needed, and when you receive alarms, you can take corresponding measures to resolve them.

<span id = "congkufangwen"></span>
### Does TencentDB for MySQL support replica access? 
For database security purposes, TencentDB for MySQL doesn't allow you to read from or write to the replica. This allows you to, for example, quickly switch to the replica when the source fails.
If you need greater read/write capability, please consider upgrading the instance configuration or purchasing a [read-only instance](https://intl.cloud.tencent.com/document/product/236/7270).

<span id = "myisam"></span>
### What if I need to use the MyISAM database engine?
You can use MySQL v5.5 to support MyISAM. However, we recommend that you choose a higher version like MySQL v5.7. This is because the InnoDB engine in higher versions can provide row-level locking with a finer granularity, deliver higher write performances, guarantee data integrity, and avoid data loss in case of database failure.

<span id = "kuadiyufangwen"></span>
### Does TencentDB for MySQL support cross-region access? 
Cross-region access is unavailable for instances in VPCs by default, as VPCs in different regions are isolated from each other. We recommend that you purchase TencentDB for MySQL instances in the same region as your CVM instances to enable local data access that guarantees high service speed and stability.


### Why can't I grant a user the "file" permission?
Currently, the "shutdown" and "file" permissions are unavailable to root users. Therefore a root user cannot create users with all permissions. Please refer to the following commands when authorizing users: 
```
grant SELECT,INSERT, UPDATE, DELETE, CREATE, DROP, ALTER on *.* to 'myuser'@'%' identified by 'mypasswd';
```

<span id = "genghuandiyu"></span>
### How do I change the TencentDB for MySQL region?
Region modification is currently not available. You can use [DTS](https://intl.cloud.tencent.com/document/product/571/13706) to migrate data between instances in different regions. DTS supports real-time data sync. After data migration is completed, you can return the source instance via self-services.

### What takes up the instance capacity?
User data (excluding backup data), the data needed for the instance to run (including the system database, database logs, indexes, etc.), and the binlogs generated by MySQL databases.

### How many databases can I run in an instance?
The maximum number of databases and tables you can create in a TencentDB for MySQL instance depends on MySQL. For more information, please see [MySQL’s official documentation](https://dev.mysql.com/doc/).

### Can I upgrade an instance from Basic Edition to High-Availability Edition or Finance Edition?
No. Currently, you can only upgrade an instance from High-Availability Edition to Finance Edition.


