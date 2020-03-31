
### How do I initialize a TencentDB for MariaDB instance?
For detailed directions, please see [Initializing TencentDB for MariaDB Instances](https://intl.cloud.tencent.com/document/product/237/7055?from_cn_redirect=1).

### How do I degrade a TencentDB for MariaDB instance?
TencentDB for MariaDB does not support degrading currently.

### How do I restart a TencentDB for MariaDB instance?
You can change the character set in the console to restart a TencentDB for MariaDB instance, which, however, is not recommended.
You can also [submit a ticket](https://console.cloud.tencent.com/workorder/category) indicating the restart reason for application. Our dedicated engineers will restart your database if your application is approved.

### Do I need to configure read/write separation separately for my program?
Read/write separation of the database is not fully automatic and takes effect only after you [create a read-only account](https://intl.cloud.tencent.com/document/product/237/35409) in the console and modify your program configuration.

### How do I effectively delete large amounts of data from a TencentDB for MariaDB instance?
The deletion method is similar to batch insertion. You are recommended to delete small amounts of data (e.g., 10,000 entries) at a time and repeat the operation multiple times.

### What should I do if some parameters I want to modify don't exist or cannot be modified in TencentDB for MariaDB parameter settings?
The TencentDB Console supports most common database parameters and sets security thresholds for them. If a parameter to be modified does not exist or cannot be modified to a specific value, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance and we will process it as soon as possible.

### How do I use mysqldump to import data to a TencentDB for MariaDB instance?
mysqldump is easy to use but requires long downtime, so it is only suitable for small amounts of data or situations that allows relatively long downtime.
For detailed directions, please see [Using mysqldump to Import Data](https://intl.cloud.tencent.com/document/product/237/8481).

### What are the functional limitations of TencentDB for MariaDB?
- You cannot change any data in the `mysql`, `information_schema`, `performance_schema`, or `sysdb` database.
- SQL statements cannot be directly used to set accounts or grant permissions, which can only be done in the console.
  The following 19 common permissions are supported, and only few rarely used permissions are not supported:
 - SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER
 - CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW
 - CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER, SHOW DATABASES
- No super admin account is provided.
- The InnoDB storage engine is used, while other engines are unavailable currently.

### How do I roll back a TencentDB for MariaDB instance?
With the database rollback feature, system loss can be minimized. TencentDB for MariaDB can roll back data to any time point in the last 30 days based on the retention of backups and logs.
For detailed directions, please see [Rolling back Databases](https://intl.cloud.tencent.com/document/product/237/8719?from_cn_redirect=1).

