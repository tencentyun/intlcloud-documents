## Impact of Sync Delay
The default replica databases, disaster recovery instances, and read-only replicas of TencentDB for MySQL use MySQL's native binlog replication technology and may experience delays during async or semi-sync data replication.

- If a [replica database](https://intl.cloud.tencent.com/document/product/236/38328) has a delay, source/replica instance switch cannot be completed promptly. In this case, the business may not be restored to normal quickly.

## Common Causes and Solutions
You can view the **source-replica delay** using the [monitoring feature](https://intl.cloud.tencent.com/document/product/236/8455). If the delay time is greater than 0, the instances are experiencing a data delay. Common causes are as follows.

### No primary key or secondary index
**Cause**
When DML operations (e.g., delete, update, and insert) are performed on big tables, the rows to be modified will be retrieved based on the primary key or secondary index when the binlog application is executed in the replica databases. If binlogs are in the row format and the corresponding table has no primary key or secondary index, a large number of full-table scans will be caused, slowing down the binlog application and leading to data delays.

**Solutions**
- Create primary keys for all tables; if a primary key cannot be created for a table, it is recommended to create a secondary index for columns with high cardinality.
- It is recommended to use the `truncate` command to delete all records of the table.

### Large transactions
**Cause**
When the source instance executes DML operations involving massive volumes of data, a large number of binlogs will be transferred to the replica database, which needs the same time consumed by the source instance to complete corresponding transactions, leading to data delays in replica database.

**Solutions**
It is recommended to divide large transactions into smaller ones and use the `where` condition to limit the volume of data to be processed at a time. This can help the replica database complete transactions quickly, thereby avoiding data delays in replica database.

### DDL operations
**Cause**
Similar to large transactions, in case of prolonged execution duration of DDL operations in the source instance, the replica database will take the same or even more time to perform the operations, which may jam up DDL operations.

**Solutions**
It is recommended to perform DDL operations during off-hours. If DDL operations are jammed due to the queries of disaster recovery and read-only replicas, you can kill the relevant sessions to restore source-replica data sync.

### Lower instance specification
**Cause**
For read-only replicas and disaster recovery instances, lower specifications than that of the source instance and higher loads will result in data delays.

**Solutions**
It is recommended to make sure that the specifications of read-only replicas and disaster recovery instances are higher than that of the source instance. If their loads are too high due to a large number of analytical businesses, you need to upgrade the instances to appropriate configurations or optimize low-performance SQL statements.


### Waiting for table metadata lock
**Cause**
Transactions which have been executed or uncommitted for a long time will jam up DDL operations and further jam all subsequent operations on the same table.

**Solutions**
We recommend that you use [TencentDB for DBbrain](https://intl.cloud.tencent.com/document/product/1035/36036) to diagnose the instance and business, check monitoring metrics like slow log, and locate long-running transactions.
- Optimize DDL statements based on DBbrain’s diagnosis results.
- Read-only nodes execute queries from users. If a query has been executed on a read-only node for a long time, the query will keep jamming the DDL operations from the source instance until the query is finished, resulting in data delays on the read-only node.
You can use DBbrain to locate the long-running query and kill it to restore the data sync between the read-only node and the source node.
- Use DBbrain to locate the long-running large transaction and divide it into smaller ones. This can help the read-only node complete transactions quickly, thereby avoiding data delays.
