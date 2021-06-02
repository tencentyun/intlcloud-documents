
### What preparations do I need to use TencentDB for MySQL?
Before using TencentDB for MySQL, you need to consider the two questions:
- Is a database suitable for your application? For example, for scenarios with small data volume, high access traffic, and key-value storage, a memory-level persistent storage service is recommended.
- Is your database appropriately designed? For example, you should consider splitting a table with obvious query hotspots or high data volume into multiple tables.

### How does TencentDB for MySQL manage MySQL?
You don't need to worry about the daily maintenance and adjustment of MySQL, which is taken care of by the OPS system of TencentDB.
In case of an exception with MySQL, the OPS system can immediately identify the issue and notify the OPS team. Developers will not need to make any changes.

### Is TencentDB for MySQL based on physical machines?
Yes.

### Can TencentDB for MySQL help me split databases and tables?
No, because the standards for splitting databases and tables are subject to your specific business logic.

### What is the difference between occupied capacity and used capacity in TencentDB for MySQL?
Used capacity: includes only MySQL's data directories but not logs such as binlog, relaylog, undolog, errorlog, and slowlog.
Occupied capacity: includes MySQL's data directories and logs such as binlog, relaylog, undolog, errorlog, and slowlog.

### Does TencentDB for MySQL have any buffer during task execution?
**Question:**
If multiple SQL statements are sent to TencentDB for execution within a very short period of time, will TencentDB for MySQL run them one by one or crash? What is the maximum number of allowed concurrent connections?
**Answer:**
A TencentDB for MySQL instance works in the same way as a self-built MySQL instance. Whether concurrently executed statements will cause a crash depends on system resources and SQL statements themselves.
When the number of connections reaches the limit (`max_connections`), the instance will not provide services normally. This happens generally due to the following reasons:
- There are too many null sessions caused by bugs in the business application;
- Frontend access goes far beyond the instance's processing capability;
- A connection which is executed for too long takes up MySQL resources exclusively, resulting in a large number of blocked access requests.

### What are the precautions for using TencentDB for MySQL?
For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/236/7259).

### How do I enable or disable the read-only permission to the default replica of a TencentDB for MySQL instance?
The default replica cannot be read from or written to. It is primarily used for high-availability switchover.

### Which monitoring metrics of the instance should I pay attention to?
CPU utilization, memory utilization, and disk space utilization. You can [configure alarms](https://intl.cloud.tencent.com/document/product/236/8457) as needed, and when you receive alarms, you can take corresponding measures to resolve them.

### [Does TencentDB for MySQL support replica access?](id:congkufangwen) 
For database security purposes, TencentDB for MySQL doesn't allow you to read from or write to the replica. This allows you to, for example, quickly switch to the replica when the source fails.
If you need greater read/write capability, please consider upgrading the instance configuration or purchasing a [read-only instance](https://intl.cloud.tencent.com/document/product/236/7270).

### [What if I need to use the MyISAM database engine?](id:myisam)
You can use MySQL v5.5 to support MyISAM. However, we recommend that you choose a higher version like MySQL v5.7. This is because the InnoDB engine in higher versions can provide row-level locking with a finer granularity, deliver higher write performances, guarantee data integrity, and avoid data loss in case of database failure.

### [Does TencentDB for MySQL support cross-region access?](id:kuadiyufangwen) 
Cross-region access is unavailable for instances in VPCs by default, as VPCs in different regions are isolated from each other. We recommend that you purchase TencentDB for MySQL instances in the same region as your CVM instances to enable local data access that guarantees high service speed and stability.

### Why can't I grant a user the "file" permission?
The "shutdown" and "file" permissions are unavailable to root users now, so a root user cannot create users with all permissions. Please refer to the following commands for authorization:
```
grant SELECT,INSERT, UPDATE, DELETE, CREATE, DROP, ALTER on *.* to 'myuser'@'%' identified by 'mypasswd';
```

### [How do I change the TencentDB for MySQL region?](id:genghuandiyu)
Region modification is currently not available. You can use [DTS](https://intl.cloud.tencent.com/document/product/571/13706) to migrate data between instances in different regions. DTS supports real-time data sync. After data migration is completed, you can return the source instance via self-services.

### What takes up the instance capacity?
User data (excluding backup data), the data needed for the instance to run (including the system database, database logs, indexes, etc.), and the binlogs generated by MySQL databases.

### How many databases can I run in an instance?
The maximum number of databases and tables you can create in a TencentDB for MySQL instance depends on MySQL. For more information, please see [MySQL’s official documentation](https://dev.mysql.com/doc/).

### Can single-node instances be upgraded to two-node or three-node instances?
No. Currently, only two-node instances can be upgraded to three-node instances.

### Why can't I convert InnoDB to MyISAM?
Probably because the instance is running MySQL v5.6 or v5.7 which only support InnoDB. To support MyISAM, please use MySQL v5.5.

### Is there a limit to the number of RO groups I can create?
By default, up to 5 RO groups can be created for a source instance.

### Can I use Canal to pull binlogs from TencentDB for MySQL?
Yes. Please pay attention to the following when using Canal:
- The CVM instance where Canal is deployed and the TencentDB for MySQL instance must be in the same VPC.
- You need to create a TencentDB for MySQL database account used for data sync and grant permissions correctly.
- You need to set the following TencentDB for MySQL database parameters: `binlog_row_image=FULL` and `binlog_format=ROW`. 

### Are TencentDB for MySQL instances deployed on physical machines or CVMs?
TencentDB for MySQL instances are deployed on physical clusters with the virtualization technology. Different from physical clusters, CVMs are mainly used to provide a scalable cloud computing service.

### Does cloning have any impact on the original instance?
No, because TencentDB clones an instance by pulling the backup data. After cloning is completed, the original instance can be used normally, or terminated if you don't need it any more.
