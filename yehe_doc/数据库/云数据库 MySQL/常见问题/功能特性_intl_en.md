### What preparations do I need to use TencentDB for MySQL?
Before using TencentDB for MySQL, you need to consider the two questions:
- Is a database a good choice for your application? For example, if your business scenario involves frequent access to a small amount of key-value data, you should consider [TencentDB for Memcached](https://cloud.tencent.com/product/cmem).
- Is your database appropriately designed? For example, you should consider splitting a table with obvious query hotspots or high data volume into multiple tables.

### How does TencentDB for MySQL manage MySQL?
You don't need to worry about the daily maintenance and adjustment of MySQL, which is taken care of by the Ops system of TencentDB.
In case of an exception with MySQL, the Ops system can immediately identify the issue and notify the Ops team. Developers will not need to make any changes.

### Is TencentDB for MySQL based on physical machines?
Yes.

### Can TencentDB for MySQL help me split databases and tables?
No, because the standards for splitting databases and tables are subject to your specific business logic.

### What is the difference between used capacity and occupied capacity in TencentDB for MySQL?
Used capacity: Includes only MySQL's data directories but not logs such as binlog, relaylog, undolog, errorlog, and slowlog.
Occupied capacity: Includes MySQL's data directories and logs such as binlog, relaylog, undolog, errorlog, and slowlog.

### Does TencentDB for MySQL have any buffer during task execution?
**Question:**
If multiple SQL statements are sent to TencentDB for execution within a very short period of time, will TencentDB for MySQL run them one by one or crash? What is the maximum number of allowed concurrent connections?
**Answer:**
A TencentDB for MySQL instance works in the same way as a self-built MySQL instance. Whether concurrently executed statements will cause a crash depends on system resources and SQL statements themselves.
When the number of connections reaches the limit (`max_connections`), the instance will not provide services normally. This happens generally for the following reasons:
- There are too many null sessions caused by bugs in the business application;
- Frontend access goes far beyond the instance's processing capability;
- A long-running connection takes up MySQL resources exclusively, resulting in a large number of blocked access requests.

### What are the precautions for using TencentDB for MySQL?
For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/236/7259).

### How do I enable or disable the read-only permission to the default replica of a TencentDB for MySQL instance?
The default replica cannot be read from or written to. It is primarily used for high-availability switchover.

### Which monitoring metrics of the instance should I pay attention to?
CPU utilization, memory utilization, and disk space utilization. You can configure alarms as needed, and when you receive alarms, you can take corresponding measures to resolve them. For more information, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457) 

[](id:congkufangwen) 
### Does TencentDB for MySQL support replica access?
For database security purposes, TencentDB for MySQL doesn't allow you to read from or write to the replica. This allows you to, for example, quickly switch to the replica when the source fails.
If you need greater read/write capability, consider upgrading the instance configuration or purchasing a [read-only instance](https://intl.cloud.tencent.com/document/product/236/7270).

[](id:myisam)
### What if I need to use the MyISAM database engine?
You can use MySQL v5.5 to support MyISAM. However, we recommend that you choose a higher version like MySQL v5.7. This is because the InnoDB engine in higher versions can provide row-level locking with a finer granularity, deliver higher write performances, guarantee data integrity, and avoid data loss in case of database failure.

[](id:kuadiyufangwen) 
### Does TencentDB for MySQL support cross-region access?
Cross-region access is unavailable for instances in VPCs by default, as VPCs in different regions are isolated from each other. We recommend that you purchase TencentDB for MySQL instances in the same region as your CVM instances to enable local data access, which guarantees high service speed and stability.

### Why can't I grant a user the "file" permission?
The "shutdown" and "file" permissions are unavailable to root users now, so a root user cannot create users with all permissions. Refer to the following commands for authorization:
```
grant SELECT,INSERT, UPDATE, DELETE, CREATE, DROP, ALTER on *.* to 'myuser'@'%' identified by 'mypasswd';
```

[](id:genghuandiyu)

### How do I change the TencentDB for MySQL region?
Region change is not supported for the time being. You can use [DTS](https://www.tencentcloud.com/document/product/571) to migrate data between instances in different regions. DTS supports real-time data sync. After data migration is completed, the source instance can be returned in a self-service manner.

### What takes up the instance capacity?
User data (excluding backup data), the data needed for the instance to run (including the system database, database logs, indexes, etc.), and the binlogs generated by MySQL databases.

### How many databases can I run in an instance?
The maximum number of databases and tables you can create in a TencentDB for MySQL instance depends on MySQL. For more information, see [MySQL's official documentation](https://dev.mysql.com/doc/).

### Can single-node instances be upgraded to two-node or three-node instances?
No. Currently, only two-node instances can be upgraded to three-node instances.

### Does the pay-as-you-go to monthly subscription billing mode change affect the database service?
No. The change only involves billing modes. For detailed directions, see [Pay-as-You-Go to Monthly Subscription](https://www.tencentcloud.com/document/product/236/52515).

### Why can't I convert InnoDB to MyISAM?
Probably because the instance is running MySQL v5.6 or v5.7 which only support InnoDB. To support MyISAM, use MySQL v5.5.

### Is there a limit to the number of real-only groups I can create?
By default, up to 5 read-only groups can be created for a source instance.

### Can I use Canal to pull binlogs from TencentDB for MySQL?
Yes. Pay attention to the following when using Canal:
- The CVM instance where Canal is deployed and the TencentDB for MySQL instance must be in the same VPC.
- You need to create a TencentDB for MySQL database account used for data sync and grant permissions correctly.
- You need to set the following TencentDB for MySQL database parameters: `binlog_row_image=FULL` and `binlog_format=ROW`. 

### Are TencentDB for MySQL instances deployed on physical machines or CVMs?
TencentDB for MySQL instances are deployed in physical clusters with the virtualization technology. Different from physical clusters, CVM instances are mainly used to provide a scalable cloud computing service.

### Does cloning have any impact on the original instance?
No, because TencentDB clones an instance by pulling the backup data. After cloning is completed, the original instance can be used normally, or terminated if you don't need it any more.
