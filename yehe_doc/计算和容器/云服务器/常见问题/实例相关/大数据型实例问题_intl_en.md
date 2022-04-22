
### What is a big data instance?
Big data instances are designed specifically for scenarios like Hadoop distributed computing, massive log processing, distributed file system, large data warehouse, and more. This CVM instance type is mainly used to solve the cloud computing and storage problems of massive business data.

### Which industry customers and business scenarios are big data instances applicable to?
Big data instances are applicable to customers in the Internet, game, finance and other industries that require big data computing and storage analysis, as well as business scenarios that require massive data storage and offline computing. They can meet the storage, capacity and private network bandwidth requirements of distributed computing businesses represented by Hadoop.
In addition, with the highly available architectural framework of distributed computing services such as Hadoop, big data instances use local storage, making the total cost close to that of a self-built Hadoop cluster in IDC, while ensuring massive storage capacity and high performance.

### Features
* A single instance has a throughput capacity up to 2.8 GB/s. HDD local disk is ideal for throughput-intensive storage. With stable and high-performing sequential read/write throughput, big data instances are designed specifically for Hadoop distributed computing, massive log processing, large data warehouse and other business scenarios.
* Local storage has a unit price as low as 1/10 of S2 instances, making its total cost close to that of a self-built Hadoop clusters in IDC while ensuring massive storage capacity and high performance. Big data instances deliver the optimal cost-efficiency for big data scenarios.
* Read/write latency is as lows as 2-5ms. Big data instances are high-performing models suitable for enterprise developers.
* It supports the pay-as-you-go billing method.

### Specifications
>?For more information on instance specifications, see the “Big Data Family” section in [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518#D).

### Notes on local data storage

Big data instances use local disk as the data disk, which **may lose data** (e.g., when the host crashes). If your application cannot guarantee data reliability, we recommend you choose an instance that can use cloud disks as the data disk.

The table below shows you the local disk data status after you perform different operations on an instance with the local disk.

| Operation | Local Disk Data Status | Description |
|------|-----|-----|
| Log in to an instance to restart it, restart an instance on the console, or forcibly restart an instance | Retained | Local disk storage as well as the data is retained. |
| Log in to an instance to shut it down, shut down an instance on the console, or forcibly shut down an instance | Retained | Local disk storage as well as the data is retained. |
| Terminate (instance) on the console | Erased | Local disk storage is erased. No data is retained. |

>! Do not store business data that needs to be retained for a long time on a local disk. Back up data in advance and use a highly available architecture. We recommend you store the data on a CBS disk for long-term retention.

### How can I purchase a local disk for big data instances?
Local disk can only be purchased when a big data instance is created. The instance specifications determine the number and capacity of local disks you can purchase.

### Does the local storage of big data instances support snapshot?
No.

### Does a big data instance support configuration adjustment and failover?

No.
Big data instances feature massive data storage and use local HDD as data disk. To prevent data loss (when the host crashes or local disk is damaged), we recommend you use a redundancy policy, for example, a file system that supports redundancy and fault tolerance (such as HDFS and Mapr-FS). We also recommend you regularly back up data to a persistent storage system, such as Tencent COS. For more information, please see [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436).
If the local disk is damaged, you will need to shut down the CVM instance for us to replace the local disk. We will notify you and perform fixes if the CVM instance crashes.

### What is the difference between the Big Data family and High IO I2 instances?

High IO I2 instances featuring ultra-high IOPS are designed specifically for business scenarios with low latency and high random IO. They are suitable for high-performance database (relational database, NoSQL, etc.). Big data instances are designed specifically for business scenarios that require high sequential read/write and low-cost massive data storage. This type features high storage cost-efficiency and private network bandwidth.

### How is the disk throughput of big data instances?

Big data D2 instances boast local disks with the sequential read/write throughput as follows.
* For a single disk, the sequential read throughput is 220+ MB/s and sequential write throughput is 220+ MB/s (block size of 128 KB and queue depth of 32).
* For the CVM, the throughput can reach up to 2.8 GB/s (block size of 128 KB and queue depth of 32).

### What is the difference between the local disk of big data instances and CBS?

[Cloud Block Storage](https://intl.cloud.tencent.com/document/product/362) is a highly available, highly reliable, low-cost, and customizable block storage device. It can be used as an independent and scalable disk for CVM, providing efficient and reliable storage devices. It provides data storage at the data block level and employs a three-copy distributed mechanism to ensure data reliability for CVM instance, meeting the requirements of different use cases. The local disk of big data instances is designed specifically for business scenarios that require high sequential read/write for massive local data sets, such as Hadoop distributed computing, large-scale parallel computing, and data warehouse.
