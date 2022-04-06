
### What is Big Data D1 instance?

Big Data D1 instance is designed specifically for Hadoop distributed computing, massive log processing, distributed file system, large data warehouse, and other business scenarios. This CVM instance type is mainly used to solve the cloud computing and storage problems of massive business data.

### Which industry customers and business scenarios are Big Data D1 instances applicable to?

Big Data D1 instance is applicable to customers in the Internet, game, finance and other industries that require big data computing and storage analysis, as well as business scenarios that require massive data storage and offline computing. It can meet the storage, capacity and private network bandwidth requirements of distributed computing businesses represented by Hadoop.
In addition, with the highly available architectural framework of distributed computing businesses represented by Hadoop, Big Data D1 instance features local storage design to achieve a total cost close to that of the self-built Hadoop cluster on an offline IDC, while ensuring massive storage capacity and high performance.

### Big Data D1 instance features

* A single instance has throughput capacity up to 2.3 GB/sec. HDD local disk is the best choice for throughput-intensive storage. With stable and high-performing sequential read/write throughput, Big Data D1 instance is designed specifically for Hadoop distributed computing, massive log processing, large data warehouse and other business scenarios.
* Local storage has a unit price as low as 1/10. Big Data D1 instance features massive storage capacity and high performance, while ensuring optimal cost-efficiency for big data scenarios. It has a total cost close to that of the self-built Hadoop cluster on an offline IDC.
* Read/write latency is minimized to 2 ms-5 ms. Big Data D1 instance, with its high-performing and enterprise-level model, is suitable for enterprise developers.
*The billing method of pay-as-you-go is supported.

### Big Data D1 instance specifications

| Model | vCPU (core) | Memory (GB) | Local Data Disk | Private Network Bandwidth | Note |
|-------|----|------|------|------|------|
| D1.2XLARGE32 | 8 | 32 | 2 × 3720 GB | 1.5 Gbps | - |
| D1.4XLARGE64 | 16 | 64 | 4 × 3720 GB | 3 Gbps | - |
| D1.6XLARGE96 | 24 | 96 | 6 × 3720 GB | 4.5 Gbps | - |
| D1.8XLARGE128 | 32 | 128 | 8 × 3720 GB | 6 Gbps | - |
| D1.14XLARGE224 | 56 | 224 | 12× 3720 GB | 10 Gbps | Exclusive for host |

### Notes on local data storage for Big Data D1 instance

Big Data D1 instance uses local disk as the data disk, which may lead to **data loss** (e.g., when the host crashes). If your application cannot guarantee data reliability, we recommend you choose an instance that can use cloud disk as the data disk.

Relationship between operating on an instance with local disk and data retention is as follows:

| Operation | Local Disk Data Status | Description |
|------|-----|-----|
| Operating system restart/Console restart/Forced restart | Retained | Local disk storage is retained. Data is retained. |
| Operating system shutdown/Console shutdown/Forced shutdown | Retained | Local disk storage is retained. Data is retained. |
| Terminate (instance) on the console | Erased | Local disk storage is erased. No data is retained. |

> Do not store business data that needs to be retained for a long time on the local disk. Back up data in advance and use a highly available architecture. For long-term retention, we recommend you store the data on CBS disk.

### How can I purchase Big Data D1 local disk?

Local disk cannot be purchased separately. You can only purchase local disk when creating the D1 instance. The number and capacity of local disks depend on instance specifications.

### Does the local storage of Big Data D1 instance support snapshot?
No.

### Does Big Data D1 instance support configuration adjustment and failover?

Configuration adjustment is not supported.
Big Data D1 instance features massive data storage and uses local HDD as data disk. This instance type does not support data disk failover (e.g., when the host crashes or local disk is damaged). To prevent data loss, we recommend you use a redundancy policy, for example, a file system that supports redundancy and fault tolerance (such as HDFS and Mapr-FS). In addition, we recommend you regularly back up data to a persistent storage system, such as Tencent COS. For more information, please see [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436).
After a local disk is damaged, you need to shut down the CVM instance so we can change the local disk. If the CVM instance has crashed, we will notify you and fix it.

### In which regions can I purchase Big Data D1 instance?

The following availability zones are supported:
* Shanghai Zone 2
* Beijing Zone 2
* Guangzhou Zone 3


### Why cannot I find the data disk after purchasing a Big Data D1 instance?

The local disk of a Big Data D1 instance is not mounted automatically. You can mount them as needed.

### What is the difference between Big Data D1 instance and High IO I2 instance?

High IO I2 instance is a CVM instance designed specifically for business scenarios with low latency and high random IO. It has ultra-high IOPS performance, and is used mainly for high-performing database (relational database, NoSQL, etc.). Big Data D1 instance is a CVM instance designed specifically for business scenarios that require high sequential read/write and low-cost massive data storage. It features high-performing storage with cost efficiency and properly configured private network bandwidth.

### How is the disk throughput of Big Data D1 instance?

Take D1.14XLARGE224 as an example, sequential read/write throughput of the local disk of Big Data D1 instances is as below:
* For a single disk, the sequential read/write speed is 190+ MB/sec (128 KB of block size and depth of 32).
* For 12 disks, the concurrent sequential read/write speed is 2.3+ GB/sec (128 KB of block size and depth of 32).

### What is the difference between the local disk of Big Data D1 instance and CBS?

[Cloud Block Storage](https://intl.cloud.tencent.com/document/product/362) provides a highly efficient and reliable storage device for CVM instance. It is a customizable block storage device with high availability, high reliability and low cost, and can be used as an independent scalable disk for CVM. It provides data storage at the data block level and employs a 3-copy distributed mechanism to ensure data reliability for CVM instance, meeting the requirements of different application scenarios. The local disk of Big Data D1 instance is designed specifically for business scenarios that require high sequential read/write for massive local data sets, such as Hadoop distributed computing, large-scale parallel computing, and data warehouse.

