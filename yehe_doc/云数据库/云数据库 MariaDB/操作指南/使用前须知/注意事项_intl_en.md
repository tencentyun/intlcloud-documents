- **Storage engine**
TencentDB for MariaDB currently supports the following storage engines. You are recommended to use InnoDB as other ones may compromise the performance. You can run the `SHOW ENGINES` command to view the storage engines supported by the current database:

| Storage Engine | Supported by TencentDB | Reason for Default Disablement |
| ------------------ | ------------------ | ---------------------------------- |
| InnoDB | Yes (default) | - |
| MyISAM | Yes (you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable it) | It may cause data inconsistency and affect sync efficiency |
| Memory | Yes | - |
| Merge | Yes | - |
| Archive | Yes (you need to submit a ticket to enable it) | It may cause data inconsistency and affect sync efficiency |
| Federated | No | It may cause security risks |
| CSV | Yes (you need to submit a ticket to enable it) | It may cause data inconsistency and affect sync efficiency |
| BLACKHOLE | Yes | - |
| MRG_MyISAM | Yes | - |
| PERFORMANCE_SCHEMA | Yes (you need to submit a ticket to enable it) | It may cause data inconsistency and affect sync efficiency |


- **Precautions on upgrading a TencentDB instance**
During the upgrade of a TencentDB instance, the instance will be disconnected for 1–30 seconds (for switch after upgrade); therefore, you need to get prepared and enable automatic reconnection between your application and database in advance to avoid service unavailability.

- **Definitions of master and slave in the documentation**
In TencentDB documentation, slave refers to the hot backup database server under the high-availability scheme. When the master fails, the slave will be put into use in real time for continuous service.

- **The architecture of "one master and two slaves" is recommended if strong sync is required**
When you perform "strong sync" replication, the master database will be hanged if it is disconnected from the slave database or the slave database fails. If there is only one master or slave database, the high-availability scheme is unavailable, because if only one single node is available, part of data will get lost or disorganized when a failure occurs.
 
- **Enabling public network access for a long time and using weak passwords may lead to security risks**
A public network IP of the database is likely to be detected and scanned by malicious users if it is enabled for a long period. If you use a weak password (such as 12345678 or 1234abcd) in this case, your database may be at great security risk.

- **Notes on TencentDB for MariaDB rollback**
 - TencentDB for MariaDB supports data rollback, but you are recommended to back up your key production data before performing rollback.
 - Data is directly rolled back to the temp instance but not the master production instance so as to avoid affecting the production instance after rollback.
 - A temp instance can be promoted to master instance. To avoid confusion, all backup data of the original master instance will become invisible after the switch. If you need such data, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
 - Each master instance has and can generate only one temp instance.
 - A temp instance can be saved for up to 48 hours and will be terminated automatically then.
 - Full backup will not be automatically generated for the temp instance. You can use a third-party tool to back it up manually if necessary.

- **Notes on TencentDB locking policy**
TencentDB has a locking mechanism. If the storage capacity usage of your instance exceeds the threshold (which is usually 103–130%; the read-only threshold for TencentDB for MariaDB is 110% currently), the system will lock your instance which will become read-only. Therefore, you are recommended to periodically check the storage capacity usage and enable SMS reminder for usage in the TencentDB for MariaDB Console. If you cannot expand the instance capacity timely due to financial reasons, you can submit a ticket to apply for temporary unlocking for 1–3 business days.

_ **TencentDB for MariaDB failover**
TencentDB for MariaDB adopts high-availability modes such as one master and one slave or one master and two slaves. When the master database fails, TencentDB for MariaDB can switch to the slave database within 1 second (200 ms in average). However, during the switch, there may be a short period of up to 30 seconds when you cannot access the database (this period of time is used for failure detection and data sync). In this case, you need to set automatic reconnection between your application and the instance in advance to avoid service unavailability. The switch is imperceptible to the business (i.e., the IP and port remain unchanged and no human intervention is required). You only need to ensure that automatic reconnection is enabled for your business.

- **Things to do after purchasing a TencentDB instance:**
After purchasing a TencentDB instance, you do not need to perform basic OPS tasks (such as high-availability maintenance, backup, and security patch), but you should pay attention to the following aspects:
 - CPU, IOPS, capacity, and number of connections of your TencentDB instance. If they become insufficient, you need to optimize or upgrade the instance.
 - Performance of your TencentDB instance, number of slow SQL statements, optimization of SQL statements, redundant or missing indices.

- **You cannot change any data in the `mysql`, `information_schema`, `performance_schema`, or `sysdb` database.**

- **SQL statements cannot be directly used to set accounts or grant permissions, which can only be done in the console. The following 19 common permissions are supported, and only few rarely used permissions are not supported:**
SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER
CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW
CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER, SHOW DATABASES

- **TencentDB for MariaDB does not provide the root account**

- **You are recommended to use the public network address only for routine maintenance but not for connection to your business server**

