## Limits on Data Volume
Due to limited resources, TencentDB for MySQL imposes restrictions on data volume of all types of MySQL instances to isolate users from getting affected by others. The following discusses the technical impacts caused by large data volume when using single instance or single table in TencentDB for MySQL.

**Instance with large data volume**: the default storage engine for TencentDB for MySQL is InnoDB. When the cache/buffer of InnoDB is able to cache all the data and index pages in the MySQL instance, the instance supports a large number of concurrent access requests. If the instance contains too much data, the cache/buffer will swap data in/out frequently. In this case, the bottleneck of MySQL shifts to IO soon, leading to the decline of access throughput. For example, for a TencentDB instance supporting 8,000 access requests per second, when data volume is twice larger than the cache/buffer, the instance can only process 700 access requests per second.


**Table with large data volume**: when a table contains too much data, the cost for MySQL to manage the table resources (data, indexes, etc.) will change, which will affect the efficiency when handling the table. For example, when a transaction table (InnoDB) contains more than 5 GB data, the delay for update operations will increase significantly, affecting the response time for transactions. In this case, users have to solve this problem by migrating data to partitioned tables.


>?If the number of tables in a single instance exceeds one million, backup and upgrade may fail and database monitoring may be affected. Please make sure the number of tables in a single instance is no more than one million.

## Limits on Number of Connections
The maximum number of connections to a TencentDB for MySQL instance is specified with the MySQL system variable `max_connections`. When the number of connections to a MySQL instance reaches `max_connections`, no more connection can be established.
The default number of connections to a TencentDB for MySQL instance can be viewed on the parameter settings page in the [MySQL Console](https://console.cloud.tencent.com/cdb), which can be adjusted if necessary. However, more connections mean that more system resources will be consumed; if the number of connections goes beyond what the actual system load capacity permits, the system service quality will be definitely undermined.
For more information on `max_connections`, see [MySQL's official documentation](https://dev.mysql.com/doc/).

## Limits on MySQL Client Connecting to TencentDB
We recommend using the MySQL client and library supplied with the CVM instance to connect to TencentDB for MySQL instances.

### Notes on slow logs
- For Linux-based CVM instances, you can use TencentDB's export tool to obtain slow query logs. For more information, see [Step 1. Download the backup file](https://intl.cloud.tencent.com/document/product/236/31910).
- For Windows-based CVM instances, slow query logs cannot be obtained directly at present. If you need them, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Notes on binlog retention duration in TencentDB
TencentDB for MySQL binlogs can be retained for 7 (default value) to 732 days (customizable in automatic backup settings). The number of days set for log backup retention must be smaller than or equal to that for data backup retention. 
If binlogs are retained for a prolonged period of time or increase too fast, more space will be needed for backup. If the space exceeds the free tier of backup capacity, fees will be incurred.

### Notes on character set
The default character set of TencentDB for MySQL is UTF8.
Although TencentDB supports changing the default character set, we recommend that you explicitly specify the table encoding when creating a table and specify the connection encoding when establishing a connection for more portable application experience.
For more information on MySQL character set, please see [MySQL's official documentation](https://dev.mysql.com/doc/).

You can change the character set in the [MySQL Console](https://console.cloud.tencent.com/cdb) or by following the steps below:
1. Execute the following statements to change the default character set encoding for a TencentDB for MySQL instance:
```
SET @@global.character_set_client = utf8;
SET @@global.character_set_results = utf8;
SET @@global.character_set_connection = utf8;
SET @@global.character_set_server = utf8;
```
The `@@global.character_set_server` will be automatically synchronized to local file for persistence in about 10 minutes (the other 3 variables will not). The configured values remain unchanged upon migration or restart.
2. Execute the following statements to change the character set encoding for the current connection:
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
1. Do not modify the information and permissions of existing accounts for the MySQL instance to prevent some of the cluster services from becoming unavailable.
2. We recommend that you use InnoDB engine when creating databases and tables to allow the instance to perform better in case of a high access volume.
3. Do not modify or stop source-replica relationship to avoid any hot backup failures.

### Limits on table name
Please note that Chinese table names are not supported when creating tables. A Chinese table name may result in a failure of rollback, upgrade, etc.

## Database Account Permission
TencentDB for MySQL no longer provides the super user permission. To modify parameters that require this permission, you can use the parameter configuration feature in the [console](https://console.cloud.tencent.com/cdb) or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Selecting Network
We recommend using a VPC. In the VPC, you can define IP range segmentation, IP addresses, and routing policies as needed. Compared with the classic network, VPC is more suitable for scenarios where custom network configurations are required. For the comparison of VPC and classic network, please see [Managing Classic Networks](https://intl.cloud.tencent.com/document/product/215/31807).

