### How long does it take to create a TencentDB for SQL Server instance?
Normally, it takes around 20 minutes or 3 minutes to create a Basic Edition instance or a Dual-Server High Availability/Cluster Edition instance respectively. The time it takes to create a read-only instance is subject to the data volume in the primary instance. The greater the data volume, the longer the time. If the primary instance is empty, it takes around 3 minutes to create a read-only instance. If the actual time is longer, there may be a problem during creation. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### How many databases can I create at most in a TencentDB for SQL Server instance?
For performance considerations, we recommend you create databases in a TencentDB for SQL Server instance within the following limits:
- Basic Edition: The number of databases that can be created is unlimited theoretically, but we recommend you keep it below 100.
- Dual-Server High Availability/Cluster Edition: The number of databases that can be created is limited in the console. We recommend you keep it below 70.

You can also use SSMS to connect to the instance and create databases, and databases created via SSMS will be automatically synced to the replica instance. However, to avoid exceptions during primary-replica sync, we recommend you not create more databases than the limit. If you have any questions or special needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Does TencentDB for SQL Server limit the IOPS?
TencentDB for SQL Server has no strict limits on the IOPS metric. Theoretically, as long as the CPU and memory are not restricted and the instance is not locked or blocked, the IOPS can be unlimited.

### Why does a TencentDB for SQL Server instance have a "monitor" database?
The "monitor" database comes with the system and is used to collect monitoring information of databases in the instance. It doesn't compromise the database performance or use your storage space.

[](id:RHGZSS)
### How does TencentDB for SQL Server track deadlocks?
TencentDB for SQL Server can use SQL Server Profiler to track deadlocks. To enable it, open SSMS, select **Tools** > **SQL Server Profiler**, and connect to the database. Note that enabling the profiler for tracking slightly affects the performance and uses a certain amount of space; therefore, disable it in time after using it.

### How do I view the memory usage of a TencentDB for SQL Server instance?
You can view various memory monitoring metrics, including maximum memory, memory usage, and memory utilization, in **Memory** on the **System Monitoring** page of your instance in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).

### How do I view the memory usage of each database in a TencentDB for SQL Server instance?
You can use a client to connect to the instance as instructed in [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626) and [Connecting to TencentDB for SQL Server Instance from Local Computer](https://intl.cloud.tencent.com/document/product/238/11627). Then, you can run the following SQL statements (for reference only) to view the memory usage of each database in the instance:
```
select count(*)*8/1024 as 'cache size(MB)',
       case database_id
           when 32767 then 'ResourceDb'
           else DB_NAME(database_id)
       end as 'datebase'
from sys.dm_os_buffer_descriptors
group by DB_NAME(database_id),
         database_id
order by 'cache size(MB)' desc
```

[](id:NCSYYZZYG)
### What should I do if the memory usage metric value stays high in TencentDB for SQL Server?
The memory mechanisms of TencentDB for SQL Server is the same as that of Microsoft SQL Server. The displayed memory usage of the SQL Server process is the highest memory usage of the instance, which will not be automatically released. SQL Server will perform internal interactions automatically. To release the memory, you need to restart the instance.

For example, 16 GB memory is allocated to an instance. When the instance just starts to be used, it may use only 8 GB memory, and the SQL Server process will occupy 8 GB memory. When the instance uses 16 GB memory, the SQL Server process will occupy all of the allocated 16 GB memory and perform internal interactions to replace the old cached data with new cached data. However, that the process occupies 16 GB memory doesn't mean that the instance actually uses 16 GB memory. In fact, it is possible that the instance only uses 1 GB memory.

### How do I view the storage space usage of a TencentDB for SQL Server instance?
You can view the **used storage space** and **percentage of remaining disk space** in **Storage** on the **System Monitoring** page of your instance in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).

### After a SQL Server database is created, no or only a small amount of data is written, but why does the storage space monitor show that 500 MB of space has been used?
A TencentDB for SQL Server instance automatically allocates a 500 MB initial space to each database. When data is written, it will be written to the initial space first. Therefore, even if you write no or only a very small amount of data, the storage metric will still be displayed as 500 MB.

### Why doesn't the storage space usage decrease after data is deleted from a TencentDB for SQL Server instance?
After data is deleted from a TencentDB for SQL Server instance, the extended data files won't be shrunk, and the free space inside the files can support subsequent operations such as insertion and update.
For example, in a 50 GB instance, if 50 GB data is written to a database and then deleted, the value of the storage space usage metric will be 50 GB, but you can still write a large number of files.

### What will happen after the data volume exceeds the maximum storage space of a TencentDB for SQL Server instance?
- Dual-Server High Availability/Cluster Edition instance: When the size of the data stored in the instance exceeds its disk capacity, features such as database import and rollback will become unavailable. You will need to expand its capacity or delete some database tables in the console to release the storage space.
- Basic Edition Instance: When the size of the data stored in the instance exceeds its disk capacity, the database will become read-only. You will need to expand its capacity or delete some database tables in the console to release the storage space and make it writable.

[](id:CPCYYY)
### Why does disk overuse happen in a TencentDB for SQL Server instance?
The following may cause disk overuse:
- Too much data: As businesses expand, new data is constantly inserted, resulting in data file space growth.
- Too many logs: The TencentDB database backs up and truncates log files regularly. If transactions are not committed for a long time, and there are a high number of UPDATE, INSERT, and DELETE operations in the database, the transaction log file may become too large.

### What should I do if the data volume exceeds the maximum storage space of my TencentDB for SQL Server instance?
- If the data file space usage is excessive, you need to expand the database or delete some tables in the console to free up the storage space. After deleting data, you can shrink the database in the console. We recommend you do so during off-peak hours. For more information, see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783), [Deleting Database](https://intl.cloud.tencent.com/document/product/238/35781), or [Shrinking Database](https://intl.cloud.tencent.com/document/product/238/41606).
- If the log file is too large, there may be some transactions not ended for a long time. You can monitor and clear sessions or transactions with a long execution time.

### Can I directly expand the storage space of a TencentDB for SQL Server instance? Do I need to perform data migration? What is the impact of the expansion?
The storage space can be expanded directly. If the storage space of the physical machine where the instance is deployed is sufficient, the data doesn't need to be migrated, and the expansion won't affect the business; otherwise, the system will automatically create primary and replica instances on physical machines with a sufficient storage space and sync the data from the original instance. During the data sync, the instance access will not be interrupted. After the migration is completed, a momentary database disconnection will occur during instance switch.
For more information on how to expand the storage space and whether the expansion will cause a momentary disconnection, see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783).

### Can I reduce the disk space of a TencentDB for SQL Server instance?
- TencentDB for SQL Server Dual-Server High Availability/Cluster Edition instance: The disk space can be reduced.
- TencentDB for SQL Server Basic Edition instance: The disk space cannot be reduced.

[](id:CPZCKJ)
### What does the disk space of a TencentDB for SQL Server instance consist of?
1. Data file space: It is the space used by your data. The data file space of TencentDB for SQL Server is preallocated. Therefore, each created database takes up nearly 500 MB to store your data.
2. Transaction log file space: Each database in a TencentDB for SQL Server instance has a log file. In full recovery model, database transaction logs will be written to the log file.
3. Temporary database and table files: Files used by `tempdb` of the TencentDB for SQL Server instance and temporary table files generated by complex queries.

### How much disk space is required for DDL operations?
To ensure normal business operations, you should avoid performing operations that may cause disk space usage surges, such as Data Definition Language (DDL) operations. If you must execute a DDL operation, make sure that the available disk space is greater than or equal to twice the size of the tablespace plus 10 GB. For example, if your tablespace is 500 GB, then when performing a DDL operation, make sure that the available disk space is greater than or equal to 500 * 2 + 10 = 1010 GB.

### How do I view the data file size of a business database in a TencentDB for SQL Server instance?
Log in to the SQL Server client and connect to the instance as instructed in [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626) and [Connecting to TencentDB for SQL Server Instance from Local Computer](https://intl.cloud.tencent.com/document/product/238/11627). Then, in the query box, run the following SQL query statements (for reference only) to view the data file size of the target business database.
```
CREATE TABLE #DBspace(
	[DBname] [sysname] NOT NULL,
	[DBsize] [decimal](18, 2) NULL,
	[DataFileSize] [decimal](18, 2) NULL,
	[LogFileSize] [decimal](18, 2) NULL,
	[UnallocatedSize] [decimal](18, 2) NULL,
	[ReservedSize] [decimal](18, 2) NULL,
	[DataSize] [decimal](18, 2) NULL,
	[IndexSize] [decimal](18, 2) NULL,
	[UnusedSiz] [decimal](18, 2) NULL,
	[AcquisitionTime] [datetime] NULL ) 
	EXEC master.sys.sp_MSforeachdb  @command1='use [?] ', @command2=N'
		use [?];
     DECLARE @pages FLOAT 
     DECLARE @dbsize FLOAT  
     DECLARE @logsize FLOAT 
     DECLARE @reservedpages FLOAT 
     DECLARE @usedpages FLOAT 
     SELECT @dbsize = SUM(CONVERT(BIGINT, CASE WHEN status & 64 = 0 THEN size ELSE 0 END)) ,@logsize = SUM(CONVERT(BIGINT, CASE WHEN status & 64 <> 0 THEN size ELSE 0 END))
     FROM   dbo.sysfiles 
     SELECT @reservedpages = SUM(a.total_pages) ,
            @usedpages = SUM(a.used_pages) ,
            @pages = SUM(CASE WHEN it.internal_type IN ( 202, 204, 207, 211,212, 213, 214, 215,216, 221, 222, 236 ) THEN 0 WHEN a.type <> 1 AND p.index_id < 2 THEN a.used_pages WHEN p.index_id < 2 THEN a.data_pages ELSE 0 END)
     FROM   sys.partitions p
            JOIN sys.allocation_units a ON p.partition_id = a.container_id
            LEFT JOIN sys.internal_tables it ON p.object_id = it.object_id 
     INSERT INTO #DBspace
            select  ''?'' ,
                    (( CONVERT (dec(15, 2), @dbsize)+ CONVERT (dec(15, 2), @logsize) ) * 8192 / 1048576 ),
                    (( CONVERT (dec(15, 2), @dbsize) ) * 8192 / 1048576 ),
                    (( CONVERT (dec(15, 2), @logsize) ) * 8192 / 1048576 ),
                    ( (CASE WHEN @dbsize >= @reservedpages THEN ( CONVERT (dec(15, 2), @dbsize)- CONVERT (dec(15, 2), @reservedpages) )* 8192 / 1048576 ELSE 0 END )) ,
                    (( CONVERT (dec(15, 2), @reservedpages) ) * 8192 / 1048576 ),
                    (( CONVERT (dec(15, 2), @pages) ) * 8192 / 1048576) ,
                    (( CONVERT (dec(15, 2), @usedpages - @pages) ) * 8192/ 1048576) ,
                    (( CONVERT (dec(15, 2), @reservedpages - @usedpages) )* 8192 / 1048576),
                    (GETDATE()) '
SELECT * FROM #DBspace ORDER BY UnallocatedSize DESC
DROP TABLE #DBspace
```

[](id:YWSJKRZWJDX)
### How do I view the log file size and status of a business database in a TencentDB for SQL Server instance?
Log in to the SQL Server client and connect to the instance as instructed in [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626) and [Connecting to TencentDB for SQL Server Instance from Local Computer](https://intl.cloud.tencent.com/document/product/238/11627). Then, in the query box, run the following SQL query statements (for reference only) to view the log file size and status of the target business database.
```
create table #T
(
    [dbname] [nvarchar](100) NULL,
    [logsize] [decimal](30, 2) NULL,
    [logused] [decimal](30, 2) NULL,
    [status] [int] NULL
) 
INSERT INTO #T([dbname],[logsize],[logused],[status])
EXECUTE('dbcc sqlperf(logspace)') 
select a.*,b.log_reuse_wait_desc from #T a inner join master.sys.databases b 
on a.dbname = b.name order by a.logsize desc
drop table #T
```

### How do I view the table size in a database in a TencentDB for SQL Server instance?
Log in to the SQL Server client and connect to the instance as instructed in [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626) and [Connecting to TencentDB for SQL Server Instance from Local Computer](https://intl.cloud.tencent.com/document/product/238/11627). Then, in the query box, run the following SQL query statements (for reference only) to view the size of each table in the target database.
```
USE [DBname]
GO
CREATE TABLE #Tablespace(
	[TableName] [nvarchar](100) NOT NULL,
	[Rows] [nvarchar](100) NULL,
	[ReservedSize] [nvarchar](100) NULL,
	[DataSize] [nvarchar](100) NULL,
	[IndexSize] [nvarchar](100) NULL,
	[UnusedSiz] [nvarchar](100) NULL ) 
INSERT INTO #Tablespace EXEC sp_msforeachtable 'sp_spaceused ''?'''
SELECT * FROM #Tablespace 
order by convert(int,replace(DataSize,'KB','')) desc,2 desc
DROP TABLE #Tablespace
```

[](id:RHHSBKJ)
### How does TencentDB for SQL Server repossess the tablespace?
A TencentDB for SQL Server instance can shrink all database files to free up the unused space. For more information, see [Shrinking Database](https://intl.cloud.tencent.com/document/product/238/41606).

### How do I avoid data disk space usage surges caused by massive amounts of data pushed to a TencentDB for SQL Server instance within a short time?
In Dual-Server High Availability/Cluster Edition primary/replica instances, if massive amounts of data is pushed, the instances may fail to be synced promptly. In this case, logs cannot be truncated and shrunk, eventually leading to data disk space usage surges. We recommend you stop for a while accordingly when pushing data, wait for the data to be fully synced, and then continue to push the next batch of data.

### How do I solve the problem of slow queries in TencentDB for SQL Server?
You can solve this problem in the following ways:
1. View slow SQL logs to check whether there are slow SQL queries and analyze the performance characteristics of each query, and locate the cause of slow queries accordingly. Then, log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the target instance ID in the instance list, and [query and download slow query logs](https://intl.cloud.tencent.com/document/product/238/47569) on the slow query log page.
You can also query the DMV view to locate the cause of slow queries in TencentDB for SQL Server.
2. View the CPU utilization metric to locate the problem. For more information, see [Monitoring Metrics](https://intl.cloud.tencent.com/document/product/238/46502).
3. Create a read-only instance dedicated for query to reduce the load of the primary instance and mitigate the database pressure.
4. Add an index to the joined field in multi-table correlated subqueries.
5. Avoid using the `select*` statement to scan the full table; instead, specify the field or add a `where` condition.

### How do I troubleshoot the problem of a high CPU utilization in a TencentDB for SQL Server instance?
The instance CPU utilization may increase for the following reasons:
1. The business SQL statements are unreasonable, as they have a lot of I/O reads and logical operations, such as compilations, recompilations, sorting, aggregations, and table joins.
Symptom: There are slow queries, the curves of changes in the QPS and CPU utilization don't match, and there are statements with a high I/O among CPU-consuming statements.
Troubleshooting method and solution: Use the following query statements (or monitoring records in the event monitor) together with the slow queries to locate the slow SQL statements and analyze them for optimization. (We recommend you create an index in a table and use it in statements as much as possible. Use SSMS to analyze the actual execution plans of the statements. Then, use optimization suggestions provided by execution plan analysis to optimize the statements based on the specific business conditions.)
```
-- Query the CPU usage by real-time sessions:
SELECT C.text,DB_NAME(A.dbid) dbname,A.loginame,A.* FROM sys.sysprocesses A 
CROSS APPLY sys.dm_exec_sql_text(A.sql_handle) C
where status in ('runnable','suspended')
order by cpu desc
-- Query the CPU usage by top 20 session SQL statements:
SELECT TOP 20  
    total_worker_time/1000 AS [total CPU time (ms)],execution_count [number of executions],  
    qs.total_worker_time/qs.execution_count/1000 AS [average CPU time (ms)],  
    last_execution_time AS [last execution time],min_worker_time /1000 AS [minimum execution time (ms)],  
    max_worker_time /1000 AS [maximum execution time (ms)],  
    SUBSTRING(qt.text,qs.statement_start_offset/2+1,   
        (CASE WHEN qs.statement_end_offset = -1   
        THEN DATALENGTH(qt.text)   
        ELSE qs.statement_end_offset END -qs.statement_start_offset)/2 + 1)   
    AS [statement using CPU], qt.text [complete syntax],  
    qt.dbid, dbname=db_name(qt.dbid),  
    qt.objectid,object_name(qt.objectid,qt.dbid) ObjectName  
FROM sys.dm_exec_query_stats qs WITH(nolock)  
CROSS apply sys.dm_exec_sql_text(qs.sql_handle) AS qt  
WHERE  execution_count>1  
--ORDER BY (qs.total_worker_time/qs.execution_count/1000) DESC -- (top 20 SQL statements with the highest CPU utilization)
--ORDER BY  total_worker_time DESC -- (top SQL statement with the longest total CPU time)
```

2. The set instance parallelism is unreasonable.
Symptom: When the current sessions of the instance are queried, it is found that a large number of identical sessions are blocked, and the wait type is CXPACKET.
Description: CXPACKET indicates that threads are waiting to be processed in parallel. Generally, the CXPACKET wait type is normal for SQL Server. It instructs SQL Server to use a parallel plan when executing queries. Such queries are usually faster than those executed serially. When the parallel plan is used, a query will be executed in multiple threads, and the query can continue only after all parallel threads are completed. This means that the query execution time will be determined by the slowest thread. However, if there are excessive parallel simple queries, or data packets of complex queries processed by parallel threads are uneven, CXPACKET wait will occur as an unreasonable parallel execution plan is generated or multiple threads wait for a slow thread to be completed.
Troubleshooting method and solution:
```
SELECT C.text,DB_NAME(A.dbid) dbname,A.loginame,A. wait_type,A.* FROM sys.sysprocesses A 
CROSS APPLY sys.dm_exec_sql_text(A.sql_handle) C
where spid in (select SPID from sys.sysprocesses where blocked <> 0 )
```
 - Configure at the statement level. Find statements with a high CPU utilization via real-time query or slow log analysis and specify `OPTION ( MAXDOP 1 )` to disable parallel processing.
Example: `SELECT * FROM TABLE WHERE L1='******' OPTION ( MAXDOP 1 )`
 - Configure at the instance level. Query the `MAXDOP` value of the current instance:
 `select * from sys.configurations where name like '%max%';`
 ![](https://qcloudimg.tencent-cloud.cn/raw/d7e265d780a4ba574beaeacd57d714b5.jpg)
 Modification method: You can modify in **Parameter Configuration** in the console:
 ![](https://qcloudimg.tencent-cloud.cn/raw/727230e807a7b5a9e34eac59f1795694.png)

3. The business concurrency is high, increasing the instance load.
Symptom: It can be clearly seen from monitoring data that the number of requests, number of connections, and CPU utilization of the instance change in line with each other.
Solution: This problem is caused by a high number of requests. You can optimize the business logic to reduce the time of each request or upgrade the instance specification.

[](id:YJQZXDSQL)
### How do I view current connections and executed SQL statements in TencentDB for SQL Server?
Log in to the SQL Server client and connect to the instance as instructed in [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626) and [Connecting to TencentDB for SQL Server Instance from Local Computer](https://intl.cloud.tencent.com/document/product/238/11627).
1. Use the `sys.sysprocesses` and `sys.dm_exec_sql_text` views to query the current connections and executed SQL statements.
```
SELECT C.text,DB_NAME(A.dbid) dbname,A.* FROM sys.sysprocesses A 
CROSS APPLY sys.dm_exec_sql_text(A.sql_handle) C
--where spid = 
```
2. Use `sys.sysprocesses` to query all current connections.
```
DBCC INPUTBUFFER(spid)
SELECT * FROM sys.sysprocesses;
```
Then, use DBCC or `sys.dm_exec_input_buffer` to query the specific SQL statements of connections.
```
DBCC INPUTBUFFER(spid)
SELECT * FROM sys.dm_exec_input_buffer(session_id, request_id);
```

### How do I analyze and solve blockage in TencentDB for SQL Server?
Symptom: When your business often runs slowly but the separate executions of individual SQL statements are fast, there is a high possibility that blocking occurs in your database and slows down the SQL execution.
Cause: Blocking occurs as another transaction is reading/writing the requested resource, and the current SQL statement can continue to read/write the resource only after the resource lock is released by the transaction. If there are waits, the business operations will become slower.
Troubleshooting method:
1. Use the `sys.sysprocesses` system view to get relevant sessions (`blocked` is `spid` of the blocking source, and `waitresource` is the resource waited for by the blocked session).
```
select * rom sys.sysprocesses where blocked <> 0
SELECT C.text,DB_NAME(A.dbid) dbname,A.loginame,A.* FROM sys.sysprocesses A 
CROSS APPLY sys.dm_exec_sql_text(A.sql_handle) C
where spid in (select SPID from sys.sysprocesses where blocked <> 0 )
```
>?Sometimes, `sys.dm_exec_sql_text` may fail to get the specific SQL text, but the aforementioned SQL statements can query the `spid` values of the blocking source and blocked session. Then, you can use DBCC or `sys.dm_exec_input_buffer` to query specific SQL statements.
2. Enable blocking tracking to get the detailed blocking data (if you need to adjust the threshold for blocking collection, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance).

Optimization suggestions:
1. If blocking already affects your business, run `kill spid` to kill the blocked session.
2. Check whether the blocking source is an uncommitted transaction, and if so, commit it promptly.
3. Analyze and optimize relevant SQL statements and business logic based on the blocking source SQL statement identified in previous troubleshooting steps. For example, if the execution time of the blocking source SQL statement is too long, you can analyze whether the execution plan can be optimized and whether the business logic is reasonable, and then make sure that resources are accessed in sequence to avoid blocking and deadlocks.
4. If `select` is blocked, you can use the `with(nolock)` query hint to prevent the query statement from applying for a lock, so as to avoid blocking. For example, you can run `select * from table with(nolock);`.

