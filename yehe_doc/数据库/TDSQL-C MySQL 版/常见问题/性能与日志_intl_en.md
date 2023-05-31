
### How do I test and compare the performance of TDSQL-C for MySQL and TencentDB for MySQL?
Before comparing the performance of TDSQL-C for MySQL and TencentDB for MySQL, note the following to get more accurate and reasonable comparison results:
- Use TDSQL-C for MySQL and TencentDB for MySQL instances with the same specification configuration.
- Use TDSQL-C for MySQL and TencentDB for MySQL instances on the same version.
The implementation mechanism varies by version. For example, MySQL 8.0 optimizes the performance of multiple CPU cores and separately abstracts threads such as `log_writer`, `log_fluser`, `log_checkpoint`, and `log_write_notifier`, but its performance is lower than MySQL 5.6 or 5.7 when there are only a few CPU cores.
- Compare the actual performance in a scenario simulating the pressure in the production environment or use sysbench for comparison. In this way, the obtained test data will be more realistic.
- Do not use an individual SQL statement to compare the read performance.
As TDSQL-C for MySQL adopts the computing-storage separation architecture, if only one SQL statement is tested, it may be affected by the network latency, and the read performance will be lower than that of TencentDB for MySQL. The cache hit rate of a database in the production environment is generally above 99%, and only the first read will call I/O, which lowers the read performance. However, as subsequent data is in the cache pool and requires no I/O calls, the performance will become the same.
- Do not use an individual SQL statement to compare the write performance either. We recommend you perform the stress test in a simulated production environment.

For the results of performance comparison between TDSQL-C for MySQL and TencentDB for MySQL, see [Test Results - Full Cache Scenario](https://www.tencentcloud.com/document/product/1098/46226).

### How do I prevent some inefficient SQL statements from lowering the overall database performance?
If your TDSQL-C for MySQL cluster is on v8.0, you can use the statement concurrency control feature to limit the number of executions of specified statements.

### Does TDSQL-C for MySQL support idle session timeout?
Yes. Yes. You can modify the `wait_timeout` parameter to customize the timeout period of idle sessions.

### How do I discover and optimize slow SQL statements?
You can discover and optimize slow SQL statements in the following two ways:
- Set an alarm policy for the monitoring metric of slow queries on the instance monitoring page to observe slow SQL statements, and then use the slow SQL analysis feature of [DBbrain](https://console.cloud.tencent.com/dbbrain/performance/analysis?instId=cynosdbmysql-ins-qw43wuqj) in the console to analyze the performance of such statements and optimize them based on the suggestions provided by DBbrain. For more information, see [Slow SQL Analysis](https://intl.cloud.tencent.com/document/product/1035/48637).
- After connecting to the database cluster, run `show processlist;` to find SQL statements with a long execution time, run `EXPLAIN` to analyze their execution plans and locate root causes, and then optimize them accordingly. For more information on how to connect to a database cluster, see [Connecting to Cluster](https://www.tencentcloud.com/document/product/1098/40627).

### Can I improve the query performance of TDSQL-C for MySQL by partitioning tables?
Generally, if a query SQL statement can fall in a partition, its performance can be improved.

Is there any relationship between the compute instance specification and the maximum IOPS? Can I adjust the specification of a computing instance to increase its maximum IOPS?
Yes. For specific computing instance specifications and their maximum IOPS values, see [Product Specifications](https://www.tencentcloud.com/document/product/1098/46430).

### How is the IOPS limited and isolated? Will I/O preemption occur between multiple nodes in a TDSQL-C for MySQL cluster?
In a TDSQL-C for MySQL cluster, the IOPS values of nodes are subject to the specification and isolated without affecting each other.

### Will the performance be affected after I enable binlog?
After binlog is enabled, the query (SELECT) performance won't be affected, but the write (INSERT, UPDATE, and DELETE) performance will. Generally, in a database with balanced reads/writes, enabling binlog will compromise the performance by 10%–20%.

### Will the performance be affected after I enable database audit?
Enabling database audit will compromise the performance by 3%–5%.

### What high-speed network protocol does TDSQL-C for MySQL use?
Between TDSQL-C for MySQL compute nodes and storage nodes and between multiple replicas of the stored data, the dual-25 Gbps RDMA technology is leveraged to deliver a low-latency high-throughput I/O performance.
