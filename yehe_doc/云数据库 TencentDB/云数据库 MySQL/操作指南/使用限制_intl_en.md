## Use Limits

### Limits on data volume
Given the limited resources, TencentDB for MySQL imposes certain limits on data volume of all types of MySQL instances for the purpose of performance issue isolation. This document describes from a technical perspective what impact a single instance or table with a high data volume will have on MySQL:

**Table with a high data volume**: if a table contains too much data, the cost for MySQL to manage table resources (data, indices, etc.) will change, which will affect the table processing efficiency. For example, if the size of a transaction table (InnoDB) exceeds 5 GB, the latency in update operations will soar, increasing the response time for transactions. In this case, the problem can only be solved through sharding and migration.

**Instance with a high data volume**: the default storage engine for TencentDB is InnoDB. If the cache buffer can cache all data and index pages in the MySQL instance, the instance can support a large number of concurrent access requests. If the instance contains too much data, the cache buffer will swap data in/out frequently; in this case, the performance bottleneck of MySQL will soon spread to IO, which will reduce the throughput. For example, a TencentDB instance designed to sustain up to 8,000 access requests per second can merely support 700 ones per second if the data volume is twice the size of the cache buffer.

>If the number of tables in a single instance exceeds 1 million, table backup, monitoring, and upgrade may fail, and database-level monitoring may be affected. Please control this value appropriately and make sure that it is below 1 million.

### Limits on number of connections
The maximum number of connections to a MySQL instance is specified with the MySQL system variable `max_connections`. When the actual number exceeds `max_connections`, no more connections can be established.
The value of `max_connections` is 3,000 for large TencentDB instances and 800 for other instances by default, which can be adjusted if necessary. However, more connections mean that more system resources will be consumed; if the number of connections goes beyond what the actual system load capacity permits, the system service quality will be definitely undermined.
For more information on `max_connections`, please see [MySQL's official documentation](https://dev.mysql.com/doc/).

## Limits on MySQL Client Version
It is recommended to use the MySQL client and library that come with CVM to connect to TencentDB instances.

### Notes on Slow Queries
- For Linux CVM instances, you can use TencentDB's export tool to get slow query logs. For more information, please see [Downloading Backup Files and Logs](https://intl.cloud.tencent.com/document/product/236/31910).
- For Windows-based CVM instances, slow query logs cannot be obtained directly at present. If you need them, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Notes on TencentDB binlog retention duration
TencentDB for MySQL binlogs can be retained for 7 (default value) to 732 days (customizable in automatic backup settings). The number of days set for log backup retention must be smaller than that for data backup retention. 
If binlogs are retained for a prolonged period of time or increase too fast, more space will be needed for backup. If the space exceeds the free tier of backup capacity, fees will be incurred.

### Notes on character set
Just as MySQL, the default character set in TencentDB is LATIN1 (ISO-8859-1).
Even though TencentDB supports changing the default character set, you are recommended to explicitly specify the table encoding format when creating it and specify the connection encoding during connection establishment. In this way, your application will be more portable.
For more information on the resources of MySQL character set, please see [MySQL's official documentation](https://dev.mysql.com/doc/).

The steps to change the TencentDB character set are as follows:
1. Run the following statements to change the default character set encoding for TencentDB instances:
```
SET @@global.character_set_client = utf8;
SET @@global.character_set_results = utf8;
SET @@global.character_set_connection = utf8;
SET @@global.character_set_server = utf8;
```
After the statements are executed, `@@global.character_set_server` will be automatically synced to a local file for persistence in approximately 10 minutes, while the other 3 variables will not. The configured value will stay unchanged even after migration or restart.
2. Run the following statements to change the character set encoding for the current connection:
```
SET @@session.character_set_client = utf8;
SET @@session.character_set_results = utf8;
SET @@session.character_set_connection = utf8;
```
Or
```
SET names utf8;
```
3. For PHP programs, you can configure the character set encoding for the current connection by using the following function:
```
bool mysqli::set_charset(string charset);
```
Or
```
bool mysqli_set_charset(mysqli link, string charset);
```
4. For Java programs, you can configure the character set encoding for the current connection as shown below:
```
jdbc:mysql://localhost:3306/dbname?useUnicode=true&characterEncoding=UTF-8
```

### Limits on operations
1. Do not modify the information and permissions of the existing accounts for a MySQL instance; otherwise, some cluster services may become unavailable.
2. InnoDB is recommended for creating databases and tables, so that the instances can better support a large number of concurrent access requests.
3. Do not modify or terminate the master-slave relationship; otherwise, hot backup may fail.

### Limits on table name
Please note that Chinese table names are not supported because they may result in failures of processes such as rollback and upgrade.

## Notes
### Database account permission
TencentDB for MySQL no longer provides the super user permission. To modify parameters that require this permission, you can use the parameter configuration feature in the console or submit a ticket for assistance; however, certain parameters cannot be modified at all.

### Database engine
InnoDB is recommended for higher performance and security. MyISAM and Memory engines are no longer supported in TencentDB for MySQL 5.6 or higher.

### Network options
For the comparison between VPC and basic network, please see [VPC's product documentation](https://intl.cloud.tencent.com/document/product/215).
- As VPC and basic network cannot intercommunicate, instances in each network environment can only be accessed separately.
