## Typical Use Cases
### Delocalization
- **Data storage with high performance and high reliability**: Cloud Block Storage (CBS) efficiently supports hot migration of CVMs, preventing business interruption caused by physical failures. CBS uses the three-copy data redundancy mechanism to back up your data and snapshots, and recover data within seconds, making it suitable for high-load and mission-critical systems.
- **Elastic expansion**: cloud disks can be freely mounted and unmounted in the same availability zone without shutting down or restarting the CVM. Cloud disk capacity can be elastically configured, and expanded on demand.
![](https://main.qcloudimg.com/raw/1cdbb7fadac1aa88d823eba12a106522.png)

### Massive data analysis
In a typical Spark-HDFS offline data analytics framework, RDD reads/writes and shuffle writes of disks by are all sequential IO, except for the random shuffle read I/O. The sequential I/O accounts for 95%. CBS features an excellent multi-thread concurrent throughput performance, enabling efficient offline data processing at the terabyte and petabyte levels for Hadoop-Mapreduce, HDFS, and Spark.
With multi-disk concurrency, a single HDFS cluster can achieve a throughput up to 1 GB/s.
CBS supports big data applications such as data analytics, data mining, and business intelligence for companies like Xiaohongshu, Giant Interactive Group, Ele, Yoho!BUY, and wepiao.com.
![](https://main.qcloudimg.com/raw/4be675dc660f05c9a7fcd35d9e83973d.png)
**Deployment environment**: 5 CVM servers (with 12-Core 40 GB RAM), simulating offline data analysis of 1.5TB data volume.
**Test performance**:

- Each CVM has mounted one 1 TB HDD cloud disk. Five HDD cloud disks provide a read speed of 500 MB/s, allowing data to be read to memory in 50 minutes.
- Each CVM has mounted one 1 TB SSD, allowing data to be read to memory in 25 minutes.

### Core database
SSD is ideal for scenarios with high requirements for IO performance and data reliability. It is particularly suitable for medium and large relational database applications like PostgreSQL, MySQL, Oracle, and SQL Server; for IO-intensive core business systems with high data reliability requirements; and for medium and large development and testing environments with high data reliability requirements.
SSD offers both data reliability and high performance. It constantly provides reliable support for companies such as Heroes Evolved, Wendao, Yoho!BUY, weipiao.com, Xiaohongshu, etc.
![](https://main.qcloudimg.com/raw/a826f514194aad6d398069b00ab817da.png)
**Deployment environment**: 4 CVM servers (with 4-Core 8 GB RAM). Each has one 800 GB SSD cloud disk mounted, with MySQL version 5.5.42 deployed.
**Test performance**: simulate OLTP performance testing using sysbench, with a test set of 10 million records. In this test, TPS and QPS reach 1,616 and 29,000 respectively, meaning a single disk is sufficient to support 10 thousand concurrent transactions per second.



## Typical business scenarios for I/O models
- **Hourly data persistence**
![](https://main.qcloudimg.com/raw/11e16a3ee744c3cdd313de199b461881.png)
- **High load OLTP services**
![](https://main.qcloudimg.com/raw/a835908f6a9bcaf8407a299607d33dee.png)
- **Periodic ultra-high loads**
![](https://main.qcloudimg.com/raw/66b6e76d8cc2d477698a21e12cffff8d.png)
- **Continuous sequential read-write**
![](https://main.qcloudimg.com/raw/f08c8eb9b38a1bf0a94cec35fea5538e.png)
