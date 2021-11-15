
### How do I initialize a TencentDB for MariaDB instance?
For more information, please see [Initializing Instance](https://intl.cloud.tencent.com/document/product/237/7055).

### How do I downgrade a TencentDB for MariaDB instance?
TencentDB for MariaDB does not support downgrading currently.

### How do I restart a TencentDB for MariaDB instance?
You can restart a TencentDB for MariaDB instance in the [console](https://console.cloud.tencent.com/mariadb), which, however, is not recommended.

### Do I need to configure read/write separation on the program?
Read/write separation of database is not configured automatically. You need to first [create a read-only account](https://intl.cloud.tencent.com/document/product/237/35409) in the console, and modify the program configuration.

### How do I effectively delete large amounts of data from a TencentDB for MariaDB instance?
The deletion method is similar to batch insertion. You are recommended to delete small amounts of data (e.g., 10,000 entries) at a time and repeat the operation multiple times.

### What if the database parameter to be modified cannot be found in parameter configuration options or some parameters cannot be modified?
 The [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb) supports most common database parameters and sets security thresholds for them. If a parameter to be modified does not exist or cannot be modified to a specific value, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance and we will process it as soon as possible.

### How do I use mysqldump to import data to a TencentDB for MariaDB instance?
mysqldump is easy to use but requires long downtime, so it is only suitable for small amounts of data or situations that allows relatively long downtime.
For more information, please see [Importing Data with mysqldump](https://intl.cloud.tencent.com/document/product/237/8481).

### What are the functional limitations of TencentDB for MariaDB?
- You cannot change any data in the `mysql`, `information_schema`, `performance_schema`, or `sysdb` database.
- You cannot use SQL statements to set accounts or grant permissions, which can only be done in the console.
  The following 19 common permissions are supported, and only few rarely used permissions are not supported:
 - SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER
 - CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW
 - CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER, SHOW DATABASES
- The super admin account is not supported.
- The InnoDB storage engine is used, while other engines are unavailable currently.

### How do I roll back a TencentDB for MariaDB instance?
TencentDB for MariaDB can roll back data to any time point in the last 30 days based on the retention of backups and logs. With the database rollback feature, system loss can be minimized.
For more information, please see [Rolling back Databases](https://intl.cloud.tencent.com/document/product/237/8719).
