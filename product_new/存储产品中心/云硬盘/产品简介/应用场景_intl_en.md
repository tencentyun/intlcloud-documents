## Typical application scenarios for CBS
### Delocalization
- **Data storage with high performance and high reliability**: Cloud Block Storage (CBS) efficiently supports hot migration of CVMs, preventing business interruption caused by physical failures. CBS provides three-copy data redundancy, and has comprehensive capabilities of data backup, snapshots, and recovery within seconds. Cloud disks are suitable for high-load and mission-critical systems.
- **Elastic expansion**: Cloud disks can be freely mounted and unmounted in the same availability zone without shutting down or restarting the CVM. Cloud disk capacity can be elastically configured, and expanded on demand.
![](//mccdn.qcloud.com/static/img/b6611d7eb39538f8376c2ed32ac58a5e/image.png)

### Massive data analysis
RDD reads/writes and shuffle writes of disks by a typical Spark-HDFS offline data analytics framework are all sequential IO. Only shuffle read IO is random IO, and sequential IO accounts for 95%. CBS features an excellent multi-thread concurrent throughput performance, enabling efficient offline data processing at the terabyte and petabyte levels for Hadoop-Mapreduce, HDFS, and Spark.
With multi-disk concurrency, a single HDFS cluster can achieve a throughput performance of 1GB/s.
CBS supports big data applications such as data analytics, data mining, and business intelligence for companies like RED, Giant Interactive Group, Ele, Yoho!, and wpiao.cn.
![](//mccdn.qcloud.com/static/img/fcd7c911ceec7205a36562dcf5f5288a/image.png)
**Deployment environment**: 5 CVM servers (12Core 40GB RAM), simulating offline data analysis of 1.5TGB of data.
**Test performance**:
- Each CVM has one 1TB HDD cloud disk mounted. Five HDD cloud disks provide a read speed of 500MB/s, allowing data to be read to memory in 50 minutes. 
- Each CVM has one 1TB SSD cloud disk mounted, allowing data to be read to memory in 25 minutes.

### Core Database
SSD cloud disk is ideal for scenarios with high requirements for IO performance and data reliability. It is especially suitable for medium and large relational database applications like PostgreSQL, MySQL, Oracle, and SQL Server; for IO-intensive core business systems with high data reliability requirements; and for medium and large development and testing environments with high data reliability requirements.
SSD cloud disk offers both data reliability and high performance. It has provided reliable support for companies such as Heroes Evolved, Wendao, Yoho!, weipiao.com, RED, etc.
![](//mccdn.qcloud.com/static/img/9867c8f2376fdf5d0878ca44159d6b66/image.png)
**Deployment environment**: 4 CVM servers (4Core 8GB RAM), each has one 800G SSD cloud disk mounted, with MySQL version 5.5.42 deployed.
**Test performance**: Simulate OLTP performance testing using sysbench, with a test set of 10 million records. In this test, TPS and QPS reach 1,616 and 29,000 respectively, meaning a single disk is sufficient to support concurrent transactions performed by more than 10 thousand people per second.

## SSD local disk application scenarios
>When using SSD local disk, we recommend that data redundancy is performed at the application layer to ensure data availability, preventing the risk of a single point of failure. For core business, we recommend you use a SSD cloud disk.

- For low-latency scenarios: SSD local disk can provide microsecond-level access latency, suitable for scenarios that require high response speed.
- For log storage of large online applications: Large online applications can produce a large amount of log data, requiring high-performance storage but not highly reliable storage.
- For temporary read cache: SSD local disk has excellent random read performance (4 KB/8 KB/16 KB random read) and can be the read-only slave for relational databases such as MySQL and Oracle. Since the cost of memory is higher than that of solid state drives, SSD local disk can also be used as a secondary cache for cache services such as Redis and Memcache. 

## Typical business scenarios for I/O models
- **Hourly data synchronization**
 ![](//mc.qcloudimg.com/static/img/fe55cf64bba9717aa3d1ba481162c68f/image.png)
- **High load OLTP services**
 ![](//mc.qcloudimg.com/static/img/f7d7ddad897df7dde608fda20d5387d5/image.png)
- **Periodic ultra-high loads**
 ![](//mc.qcloudimg.com/static/img/83c11d14843c325b486993c58c50e408/image.png)
- **Continuous sequential read-write**
 ![](//mc.qcloudimg.com/static/img/01528b8dea5a53d3ffa40e4b2f08c1ae/image.png)
