This document describes the usage specifications and suggestions for TencentDB for SQL Server.

## Purpose
- To standardize the management and maintenance of TencentDB for SQL Server to avoid unavailability and other issues caused by improper operations.
- To provide guidance for database developers on how to write SQL statements to ensure optimal performance of TencentDB for SQL Server.

## Suggestions for instance specification
- Do not use instances with the 1-core specification in the production environment, which is suitable for feature testing only.
- Use instances with the 2-core or higher specification in the production environment. As SQL Server runs on Windows, the engine and the system require many resources. Therefore, the 1-core specification isn't suitable for sustaining the production business, and problems such as low system memory and system lags may occur after long-time operations on this specification.

## Suggestions for instance selection
- Use two-node (formerly High Availability/Cluster Edition) primary/replica instances. Compared with a single-node (formerly Basic Edition) instance, two-node instances can greatly improve the availability and reliability of the production business.
- If your business has fewer write requests but massive read requests and you need to add read-only instances, use SQL Server 2017/2019 two-node instances to sync data more efficiently and stably.
- Select multi-AZ deployment for Dual-Server High Availability/Cluster Edition instances to implement AZ-level disaster recovery.

## Suggestions for database connection
- Use `ip,port` to connect to a TencentDB for SQL Server instance. Note that the IP and port are separated by a comma.
- Do not use the server name for connection. Your application should better have a reconnection mechanism for database connection, so it can reconnect to databases in time through retries in case of database failure or disconnection.

## Permission management specifications
- To ensure the stability and security, permission restrictions are imposed on `sysadmin` and `shutdown` in TencentDB for SQL Server. The following errors may occur when you run certain statements:
 - `User does not have permission to perform this action.`
 - `You do not have permission to run the RECONFIGURE statement.`
Solution: Modify parameters, manage databases and users, and restore backups in the console.
- Grant permissions on demand. It is sufficient to grant general applications the read/write permissions of specified databases.
- Grant privileges to users of general application at the database level.
- Allow authorized users to access TencentDB for SQL Server only from specific IPs or IP ranges. This can be achieved by configuring security groups in the console as prompted.
- Separate management, development, and application accounts. Avoid using admin accounts for development or business operations.

## Daily operation specifications and suggestions
- If there are too many databases, the TencentDB for SQL Server instance performance will drop, and more resources such as worker threads will be used. If the limit on the number of created instances is exceeded, primary/replica sync exceptions may occur. We recommend that you keep the number of databases created in a single instance below the upper limit, which is subject to the CPU core quantity of the instance. For more information, see [Constraints and Limits > Database quantity](https://www.tencentcloud.com/document/product/238/2021).
- The database name can contain up to 64 digits, letters, and underscores.
- For enhanced instance security, do not use weak passwords. Perform account and database management operations in the console in general cases.
- For login over the private network, make sure that the CVM instance of the client and the TencentDB for SQL Server instance are in the same VPC in the same region under the same account.
- Applications should not rely on `sysadmin` permissions to use databases. Accounts with the `sysadmin` role have the super admin permissions. If they are used improperly, the database security and stability will be compromised. Therefore, TencentDB doesn't open up the super admin permissions by default.
- Check the database size and shrink databases promptly. If a database is used for a long time, the used physical space may not be released in time, and you need to shrink the database to release such space. Check the log file size and physical file size frequently, so that you can shrink databases during off-peak hours when you find that the file size increases rapidly.
- After long-term operations, instances may suffer from a performance drop. Therefore, restart instances at least once every three months during off-peak hours.
- Do not create tables or write data in system databases. Store data in created custom databases. Although permissions to use system databases are opened up, any data stored in system databases is insecure.
- Do not set databases to the single-user mode. In this mode, only one session is allowed to access databases, causing TencentDB Ops problems. If the single-user mode is set, change back to the multi-user mode promptly.
- Extended events are used for slow log collection. This is a lightweight tracking method and basically has no impact on instances.
- Reindex database regularly. After a database runs for a long time, it may generate many index fragments, which compromise the database access performance. Therefore, you need to regularly reindex databases by creating SQL agent jobs, preferably once every month.
- Update the statistics regularly by creating SQL agent jobs, preferably once every week. This helps guarantee the performance.
- Set the maximum concurrency, which determines the business CPU utilization.
- Perform backup and restoration operations through the console or APIs rather than SSMS or SQL statements. For more information on backup and restoration methods and database migration to the cloud, see [Cold Backup Migration](https://www.tencentcloud.com/document/product/238/39005).
- Do not set the database recovery model to simple model. Use the full model instead.
 - If the simple recovery model is used, incremental backup won't be implemented on the database, so the database cannot be restored to the specified time point.
 - For two-node (formerly High Availability/Cluster Edition) instances, after you set the database recovery model to simple model, the database cannot establish replication relationships and thus cannot support primary/replica switch or specification change.
 Therefore, use the simple recovery model with caution.
- Avoid performing DDL operations during peak hours.
- Avoid performing batch operations during peak hours. To delete an entire table, use `TRUNCATE` or `DROP` during off-peak hours.
- Avoid running an instance for multiple businesses to minimize the risk of mutual interference between businesses due to high coupling.
- Avoid using automatic transaction committing and develop a habit of using `begin tran;` for online operations, which helps minimize the risk of data loss caused by maloperations. In case of a maloperation, you can use the rollback feature of TencentDB for SQL Server for data restoration. After a transaction begins, commit it in time to avoid instance blocking.
- Perform database operations in the console rather than on the SSMS client.
- Estimate the resources required in advance and optimize the instances for promotional campaigns of your business. In case of a great demand for resources, contact your Tencent Cloud sales rep timely.

## Suggestions for using DTS for database migration
**Check the following before migrating a database to the cloud:**
- Version numbers of source and target databases. The target database must be on a version later than or equal to the source database. For example, if the source database is on v2016, the target database can only be on v2016, v2017, or v2019.
- Architecture versions of source and target databases. If the source instance is a self-built database in a local IDC, CVM instance, or cloud server in another cloud vendor, or is a cloud SQL Server instance in another cloud vendor, you can migrate it to a TencentDB for SQL Server single-node (formerly Basic Edition) instance or two-node (formerly High Availability/Cluster Edition) instance on any architecture version. If the source instance is a TencentDB for SQL Server two-node (formerly High Availability/Cluster Edition) instance, it cannot be migrated to a single-node (formerly Basic Edition) instance through DTS. If the source instance is a TencentDB for SQL Server single-node (formerly Basic Edition) instance, it can be migrated to a two-node (formerly High Availability/Cluster Edition) instance through DTS.
- Network connectivity between source and target databases. The source and target databases must be connected. The server where the source database resides must have enough outbound bandwidth; otherwise, the migration efficiency will be affected.
- Names of source and target databases. The source and target instances cannot have databases with the same name.
- Account permissions of the source database. You need to change to "local" for SQL service startup in the source database. The source database account is unrestricted but needs to have the sysadmin permissions.
- Account permissions of the target database. The target database needs to have an account with admin permissions for migration.
- Ports of the source database. The source database needs to open port 1433, and the service where the source database is located must open the file sharing port 445 for Windows server sharing.
- Recovery model of the source database. The source database must be set to "full recovery model", and we recommend that you make a full backup before migration.
- Local disk space of the source database. The local disk space of the source database must be large enough, so that the remaining free space can fit the size of the database to be migrated.
- Disk space of the target database. The disk space of the target database must be at least 1.5 times the size of the source database.
- Status of the target database. The target database cannot have access requests or active businesses; otherwise, the migration will fail.

You need to keep the following operation limits in mind when migrating data to the cloud:
- Only one migration task can be initiated at any time for the same source instance.
- Only database-level migration is supported (i.e., all objects in the database must be migrated together), while single-table migration is not supported.
- Logins, jobs, triggers, and database links (link server) at the instance level cannot be migrated.
- Do not modify or delete user information (including username, password, and permissions) in the source and target databases and port numbers during migration; otherwise, the migration task will fail.
- Do not perform transaction log backup during incremental sync; otherwise, the transaction log will be truncated and become discontinuous.
- If you only perform full data migration, do not write new data into the source database during migration; otherwise, the data in the source and target databases will be inconsistent. In scenarios with data writes, to ensure the data consistency in real time, we recommend that you select full + incremental data migration.
- For full + incremental data migration, after you click **Complete** and the task status becomes **Completed**, do not write new data to the source database. We recommend that you stop writing for two minutes; otherwise, the data in the source and target databases may be inconsistent.

**Check the following after migrating data to the cloud:**
- Permission completeness. Permissions will affect operations performed on the database. The migration only restores data. To restore other service-level permissions, such as database users and login usernames, you need to create them again and associate them with database accounts.
- Reindexing. As the physical environment of the data files changes, database indexes will become invalid, and you need to create indexes again; otherwise, the database performance may be significantly compromised.
- Instance-level objects such as logins, jobs, triggers, and database links (link server). You need to create them again after the migration is completed.

## Database and table design specifications
**Notes**
- TencentDB for SQL Server versions earlier than 2014 don't support memory-optimized tables. If you need to use this type of tables, we recommend that you use TencentDB for Redis and Memcached.
- Follow the third normal form (3NF) when creating tables and specify the primary key for each table. Even if you can't select an appropriate column as the primary key, you still need to select one. 
- Define fields as NOT NULL and set default values. NULL fields will cause unavailability of indexes, thus bringing problems to SQL development. NULL calculation can only be implemented based on IS NULL and IS NOT NULL.

**Suggestions:**
- Plan the resources used by databases reasonably based on business scenario analysis and estimation of data access (including database read/write QPS, TPS, and storage). You can also configure various monitoring metrics for TencentDB for SQL Server in the TCOP console.
- Put the tables for the same type of businesses into one database when building databases and try not to mix and match. Do not perform cross-database correlation operations in programs, as doing so will affect subsequent quick rollbacks.
- Use the same character set to avoid garbled text caused by conflicts between different character sets.
- Use the `DECIMAL` type to store decimal values. The `FLOAT` and `DOUBLE` types have insufficient precision, especially for businesses involving money. 
- Do not use the TEXT or BLOB type to store a large quantity of text, binary data, images, files, and other contents in a database; instead, save such data as local disk files and only store their index information in the database.
- Avoid using foreign keys. We recommend that you implement the foreign key logic at the application layer. Foreign key and cascade update are not suitable for high-concurrence scenarios, because they may reduce the insertion performance and lead to deadlock in case of high concurrence.
- Reduce the coupling of business logic and data storage, use databases mainly for storing data, implement business logic at the application layer, and minimize the use of instance-level triggers, link servers, jobs, and other advanced features due to their poor portability and scalability. If such objects exist in an instance, after data migration, you need to migrate them to the new instance manually.
- If you don't have a significant increase in business volume in the near future, do not use partitioned tables, which are mainly used for archive management. Partitioned tables have no obvious improvement on the performance if most queries in your business don't involve partition fields.
- Purchase read-only instances to implement read/write separation at the database level for business scenarios with a high read load and low requirement for consistency (where a data delay within seconds is acceptable).

## Index design specifications
**Notes**
- Do not create indexes on the columns that are updated frequently and have a lower selectivity. Record updates will change the B+ tree, so creating indexes on frequently updated fields may greatly reduce the database performance.
- Put the column with the highest selectivity on the far left when creating a composite index; for example, in `select xxx where a = x and b = x;`, if a and b are used together to create a composite index and a has a higher selectivity, then the composite index should be created as `idx_ab(a,b)`. If `Not Equal To` and `Equal To` conditions are used at the same time, the column with the `Equal To` condition must be put first; for example, in `where a xxx and b = xxx`, b must be placed on the far left even if a has a higher selectivity, because a will not be used in the query.

**Suggestions:**
- Use no more than 5 indexes in a single table and no more than 5 fields in a single index. Too many indexes may affect the filtering, occupy much more capacity, and consume more resources for management.
- Create indexes on the columns that are used for SQL filtering most frequently with a small number of duplicate values. It is meaningless to create indexes on a column not involved in SQL filtering. The higher the uniqueness of a field, the better the index filtering effect. 
- Avoid using redundant indexes. If both index (a,b) and index (a) exist, (a) is considered a redundant index. If the query filtering is based on column a, the index (a,b) is sufficient.
- Use `INCLUDE index` reasonably to reduce I/O overheads. Commonly used columns should be placed on the left, and columns that will not be used as query conditions can be placed in `INCLUDE`.

## SQL statement writing specifications
**Notes**
- For `UPDATE` and `DELETE`, use `WHERE` for exact match. To delete a large amount of data, delete the data in batches during off-peak hours.
- When using `INSERT INTO t_xxx VALUES(xxx)`, explicitly specify the column attributes to be inserted to prevent data errors caused by changes in the table structure.
- Pay attention to the following common causes of invalid indexes in SQL statements:
 - Implicit type conversion; for example, if the type of index a is `VARCHAR` and the SQL statement is `where a = 1`, then `VARCHAR` is changed to `INT`.
 - Math calculations and functions are performed on the index columns; for example, date column is formatted using a function.
 - Multiple columns with different sorting orders; for example, the index is (a,b), but the SQL statement is `order by a b desc`.
 - Use the `WHERE` condition for exact match to avoid fuzzy match of conditions and batch matches of `IN` and `NOT IN`.

**Suggestions:**
Ensure query on demand and reject `select *` to avoid the following problems:
- The covering index does not work and the problem of TABLE ACCESS BY INDEX ROWID occurs, which leads to extra IO overhead.
- Three is an additional memory load. A large amount of cold data is imported to the cache, which may reduce the query hit rate.
- Additional overhead in network transfer.
- Instance blocking or primary/replica delay may occur. To prevent this, avoid using large transactions and split a large transaction into multiple small ones.
- Commit transactions in the business code in a timely manner to avoid unnecessary lock waits.
- Minimize the use of `JOIN` operations on multiple tables and big tables. When joining two tables, use the smaller one as the driving table and select indexed columns with the same character set for join.

**Note**
- It is difficult to completely avoid the aforementioned issues. The solution is to set the aforementioned conditions as secondary filtering conditions for indexes rather than as primary filtering conditions.
- If a large number of full-table scans is found in the monitoring data, you can download slow log files in the console for analysis.
- Perform the required SQL audit before a business is released. In daily Ops work, download slow query logs regularly for targeted optimization.
