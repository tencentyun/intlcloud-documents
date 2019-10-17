## Typical application scenarios for CBS
### Delocalization
- **Data storage with high performance and high reliability**: Cloud Block Storage (CBS) efficiently supports hot migration of CVMs, preventing business interruption caused by physical failures. CBS provides three-copy data redundancy, and has comprehensive capabilities of data backup, snapshots, and recovery within seconds. Cloud disks are suitable for high-load and mission-critical systems.
- **Elastic expansion**: Cloud disks can be freely mounted and unmounted in the same availability zone without shutting down or restarting the CVM. Cloud disk capacity can be elastically configured, and expanded on demand.
![](https://main.qcloudimg.com/raw/1cdbb7fadac1aa88d823eba12a106522.png)

### Massive data analysis
RDD reads/writes and shuffle writes of disks by a typical Spark-HDFS offline data analytics framework are all sequential IO. Only shuffle read IO is random IO, and sequential IO accounts for 95%. CBS features an excellent multi-thread concurrent throughput performance, enabling efficient offline data processing at the terabyte and petabyte levels for Hadoop-Mapreduce, HDFS, and Spark.
With multi-disk concurrency, a single HDFS cluster can achieve a throughput performance of 1GB/s.
CBS supports big data applications such as data analytics, data mining, and business intelligence for companies like RED, Giant Interactive Group, Ele, Yoho!, and wpiao.cn.
![](https://main.qcloudimg.com/raw/4be675dc660f05c9a7fcd35d9e83973d.png)
**Deployment environment**: 5 CVM servers (12Core 40GB RAM), simulating offline data analysis of 1.5TGB of data.
**Test performance**:
- Each CVM has one 1TB HDD cloud disk mounted. Five HDD cloud disks provide a read speed of 500MB/s, allowing data to be read to memory in 50 minutes. 
- Each CVM has one 1TB SSD cloud disk mounted, allowing data to be read to memory in 25 minutes.

### Core Database
SSD cloud disk is ideal for scenarios with high requirements for IO performance and data reliability. It is especially suitable for medium and large relational database applications like PostgreSQL, MySQL, Oracle, and SQL Server; for IO-intensive core business systems with high data reliability requirements; and for medium and large development and testing environments with high data reliability requirements.
SSD cloud disk offers both data reliability and high performance. It has provided reliable support for companies such as Heroes Evolved, Wendao, Yoho!, weipiao.com, RED, etc.
![](https://main.qcloudimg.com/raw/a826f514194aad6d398069b00ab817da.png)
**Deployment environment**: 4 CVM servers (4Core 8GB RAM), each has one 800G SSD cloud disk mounted, with MySQL version 5.5.42 deployed.
**Test performance**: Simulate OLTP performance testing using sysbench, with a test set of 10 million records. In this test, TPS and QPS reach 1,616 and 29,000 respectively, meaning a single disk is sufficient to support concurrent transactions performed by more than 10 thousand people per second.

## SSD local disk application scenarios
>When using SSD local disk, we recommend that data redundancy is performed at the application layer to ensure data availability, preventing the risk of a single point of failure. For core business, we recommend you use a SSD cloud disk.

- For low-latency scenarios: SSD local disk can provide microsecond-level access latency, suitable for scenarios that require high response speed.
- For log storage of large online applications: Large online applications can produce a large amount of log data, requiring high-performance storage but not highly reliable storage.
- For temporary read cache: SSD local disk has excellent random read performance (4 KB/8 KB/16 KB random read) and can be the read-only slave for relational databases such as MySQL and Oracle. Since the cost of memory is higher than that of solid state drives, SSD local disk can also be used as a secondary cache for cache services such as Redis and Memcache. 

## Typical business scenarios for I/O models
- **Hourly data synchronization**
 ![](https://main.qcloudimg.com/raw/11e16a3ee744c3cdd313de199b461881.png)
- **High load OLTP services**
 ![](https://main.qcloudimg.com/raw/a835908f6a9bcaf8407a299607d33dee.png)
- **Periodic ultra-high loads**
 ![](https://main.qcloudimg.com/raw/66b6e76d8cc2d477698a21e12cffff8d.png)
- **Continuous sequential read-write**
 ![](https://main.qcloudimg.com/raw/f08c8eb9b38a1bf0a94cec35fea5538e.png)
