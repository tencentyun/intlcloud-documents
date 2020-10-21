## Impact of Sync Delay
The default slave databases, disaster recovery instances, and read-only instances of TencentDB for MySQL use MySQL's native binlog replication technology and may experience delays during async or semi-sync data replication.

- If a [slave database](https://intl.cloud.tencent.com/document/product/236/38328) has a delay, master/slave instance switch cannot be completed promptly. In this case, the business may not be restored to normal quickly.
- If a disaster recovery instance has a delay, it cannot be promoted to a master instance before the heaped binlogs run out. During this period, business continuity will be affected.
- If a read business has relatively high requirements for data consistency, a delay-triggered removal policy can be configured for the read-only group, so that when the master-slave delay exceeds the configured threshold, the corresponding read-only instance will be removed automatically and hence cannot be accessed by the read business.

## Solution for Sync Delay
You can view the **master-slave delay** using the monitoring function. If the delay time is greater than 0, the instances are experiencing a data delay. Common reasons include:

### No Primary Key or Secondary Index
**Cause**
When DML operations (e.g., delete, update, and insert) are performed on big tables, the rows to be modified will be retrieved based on the primary key or secondary index when the binlog application is executed in the slave databases. If binlogs are in the row format and the corresponding table has no primary key or secondary index, a large number of full-table scans will be caused, slowing down the binlog application and leading to data delays.

**Solution**
- Create primary keys for all tables; if a primary key cannot be created for a table, it is recommended to create a secondary index for columns with high cardinality.
- It is recommended to use the `truncate` command to delete all records of the table.

### Large Transactions
**Cause**
When the master instance executes DML operations involving massive volumes of data, a large number of binlogs will be transferred to the slave database, which needs the same time consumed by the master instance to complete corresponding transactions, leading to data delays in slave database.

**Solution**
It is recommended to divide large transactions into smaller ones and use the `where` condition to limit the volume of data to be processed at a time. This can help the slave database complete transactions quickly, thereby avoiding data delays in slave database.

### DDL Operations
**Cause**
Similar to large transactions, in case of prolonged execution duration of DDL operations in the master instance, the slave database will take the same or even more time to perform the operations, which may jam up DDL operations.

**Solution**
It is recommended to perform DDL operations during off-hours. If DDL operations are jammed due to the queries of disaster recovery and read-only instances, you can kill the relevant sessions directly to restore master-slave data sync.

### Lower Instance Specification
**Cause**
For read-only and disaster recovery instances, lower specifications than that of the master instance and higher loads will result in data delays.

**Solution**
It is recommended to make sure that the specifications of read-only and disaster recovery instances are higher than that of the master instance. If their loads are too high due to a large amount of analytical businesses, you need to upgrade the instances to appropriate configurations or optimize low-performance SQL statements.
