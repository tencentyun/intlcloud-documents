Databases with excellent performance and scalability can help you quickly increase the load capacity of your existing systems. With the same size of database, TencentDB for MySQL, if appropriately used, can significantly improve database concurrence for higher QPS.

## 1. Select a proper database configuration

### 1.1 Select the database version
TencentDB for MySQL is currently available in v5.5, v5.6, and v5.7, all of which are fully compatible with native MySQL. You are recommended to choose v5.6 and higher, as they use more stable database kernels, deliver better system performance by optimizing the design of v5.5 and lower, and come with a lot of appealing new features.

This document takes MySQL v5.7 as an example to illustrate the features of the new versions. This version is widely recognized for its impressive performance, reliability, and ease of use. Some of its improvements and new features are as shown below:

- **Native JSON support**
In MySQL v5.7, a new data type has been added to store data in the native JSON format in MySQL tables, which has the following advantages:
 - Document verification: Only data segments in line with JSON rules can be written to JSON-type columns, which means that there is automated JSON syntax verification.
 - Efficient access: When a JSON document is stored in a JSON-type column, the data will not be stored as plain text; instead, it will be stored in the optimized binary format, so that its object members and array elements can be accessed more quickly.
 - Performance enhancement: An index can be created on data in JSON-type columns so as to improve the query performance. Such indexes can be implemented through the "function index" created on virtual columns.
 - Convenience: The inline syntax attached to JSON-type columns can be naturally integrated into document queries in SQL statements such as "features". "feature" is a JSON field:
```
 SELECT feature->"$.properties.STREET" AS property_street FROM features WHERE id = 121254;
```
With MySQL v5.7, you can seamlessly integrate the best relational samples with the best document samples in one tool so as to use the most appropriate ones out of them in different applications and use cases, which greatly expands your range of applications.
- **SYS Schema**
MySQL SYS Schema is a database schema consisting of a set of objects such as views, stored procedures, storage methods, tables, and triggers. It gives easy, readable, DBA- and developer-friendly access to the wealth of monitoring data stored in various tables in Performance Schema and INFORMATION_SCHEMA.
It is included in MySQL v5.7 by default and provides summary views to answer the following common questions:
 - What is taking up all the resources of the database service?
 - Which CVM instance accesses the database server most frequently?
 - How is the instance memory used?
- **InnoDB improvements**
 - Online operations in InnoDB (Online DDL): You can dynamically adjust the buffer pool size to make it adaptive to the change of your business needs without restarting MySQL. InnoDB now can automatically empty its UNDO logs and table space online, thus eliminating one of the most common reasons for large shared table space files (ibdata1). In addition, MySQL v5.7 supports renaming indexes and changing the varchar size, both of which could be done only by recreating indexes or tables in previous versions.
 - InnoDB native partitioning: In MySQL v5.7, InnoDB includes the native support for partitioning, which can reduce the load and lower the memory usage by up to 90%.
 - InnoDB cache prefetching: When MySQL restarts, InnoDB will automatically retain 25% of the hottest data in the buffer pool, eliminating your need to preload or prefetch the data cache and preventing potential performance loss caused by MySQL restart.

For more information on improvements and new features in MySQL v5.7, see [MySQL's official documentation](https://dev.mysql.com/doc/refman/5.7/en/mysql-nutshell.html).

### 1.2 Select an instance specification (database memory)
Currently, TencentDB for MySQL doesn't offer separate CPU options; instead, the CPU will be allocated proportionally according to the memory specification. You can purchase database specifications based on your business characteristics. We have conducted thorough benchmark tests on each type of instance so as to provide performance information for your reference when you select specifications.
However, it should be noted that the sysbench-enabled tests cannot represent all business scenarios. You are recommended to perform stress testing on your instance before launching it officially, so that you can better understand how TencentDB for MySQL performs in your business scenario. For more information, see [MySQL Performance Description](https://intl.cloud.tencent.com/document/product/236/8842).

Memory is one of the core instance metrics, which features an access speed much higher than that of a disk. Generally, the more data cached in the memory, the faster the database response. If the memory is small, after the stored data exceeds a certain amount, the excessive data will be stored to the disk. After that, when a new request accesses the data again, the data will be read from the disk into the memory, consuming disk IO and leading to slower database response.

**For businesses with high read concurrence or sensitive to read delay, it is recommended to choose a higher memory specification so as to ensure high database performance.**

### 1.3 Select a disk (data storage capacity)
The disk capacity of a TencentDB for MySQL instance includes only the MySQL data directories but not the logs such as binlog, relaylog, undolog, errorlog, and slowlog. When the amount of written data exceeds the instance disk capacity, if the instance is not upgraded, instance lock may be triggered. Therefore, when you purchase a disk, you are recommended to take into account the possible data volume increase in the future and select a larger disk, which helps prevent your instance from being locked or frequently upgraded due to insufficient disk capacity.

### 1.4 Select a proper data replication mode
TencentDB for MySQL provides three replication modes: async, semi-sync, and strong sync. For more information, see [Database Instance Replication Mode](http://intl.cloud.tencent.com/document/product/236/7913). If your business is sensitive to write latency or database performance, you are recommended to choose the async replication mode.

### 1.5 High availability of TencentDB
High availability of TencentDB for MySQL is guaranteed by the master/slave and master/master architecture. Master-slave data sync is achieved through binlogs. In addition, the database can be rolled back to any previous point in time, which relies on backups and logs. Therefore, you generally do not need to set up a backup and restoration system on your own or pay additional fees to keep your instance highly available.

### 1.6 Scalability of TencentDB
All the different database versions and memory/disk specifications of TencentDB for MySQL support online dynamic hot upgrade. The upgrade process will not interrupt your business, eliminating your concerns over any database bottlenecks caused by business growth.

### 1.7 Use CVM and TencentDB for MySQL together
After a purchase is made, you generally need to use CVM and TencentDB for MySQL together. For more information, see [Accessing TencentDB for MySQL from CVM](https://intl.cloud.tencent.com/document/product/236/3130).

## 2. Use a read-only instance as read extension
In common internet-based businesses, the read/write ratio of databases generally ranges from 4:1 to 10:1, which means that the read load of databases is much higher than the write load. When a performance bottleneck occurs, a common solution is to increase the read load.
TencentDB for MySQL read-only instances are ideal for such issues. For more information, see [Read-only Instance](http://intl.cloud.tencent.com/document/product/236/7270).
Read-only instances can also be used for read-only access in various businesses; for example, the master instance undertakes read/write access for online businesses, while the read-only instance provides read-only query for internal businesses or data analysis platforms.

## 3. Disaster recovery scheme of TencentDB for MySQL
TencentDB for MySQL provides [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272), helping you quickly set up remote disaster recovery for databases.

With the help of disaster recovery instances, multiple data centers in different regions can act as redundancy of each other, so that when one data center cannot provide a service due to failures or force majeure events, the service can be quickly switched to another data center. Disaster recovery instances use private network Direct Connect lines of Tencent Cloud to implement data sync, which can minimize the impact of delayed sync on your business when a disaster occurs. As long as the remote service logic is ready, the disaster recovery switchover can be completed in seconds.

## 4. 2-region-3-DC scheme
With TencentDB for MySQL, it only takes several simple steps to configure the 2-region-3-DC scheme:
- Purchase a TencentDB for MySQL intra-city strong-consistency cluster and select [multi-AZ deployment](http://intl.cloud.tencent.com/document/product/236/8459) (currently in beta test) which provides the 1-region-2-DC capacity.
- Add remote disaster recovery nodes to the cluster in order to build the 2-region-3-DC architecture.

## 5. Use disaster recovery instances to provide users with local access
A disaster recovery instance also adopts the high-availability master/slave and master/master architecture. In addition, it can be accessed in a read-only manner, which helps enable local access to your businesses for end users in different regions.
