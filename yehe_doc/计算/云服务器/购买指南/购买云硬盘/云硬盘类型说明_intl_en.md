Cloud Block Storage (CBS) is a highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone and expandable disk for CVMs. CBS uses a three-copy distributed mechanism to store data at the data block level and ensure data reliability. CBS is classified into two types: **SSD**, and **Premium Cloud Storage**. Each type has unique performance and characteristics, and the price varies, making CBS suitable for different use cases.

- **SSD**: SSD uses NVMe SSD as the storage media, and employs a three-copy distributed mechanism. It provides high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for applications with high requirements for I/O performance.
- **Premium Cloud Storage**: Tencent Cloud Premium Cloud Storage is a hybrid storage type. It adopts the Cache mechanism to provide a high-performance SSD-like storage, and employs a three-copy distributed mechanism to ensure data reliability. Premium Cloud Storage is suitable for small and medium applications with high requirements for data reliability and standard requirements for performance, as well as for small and medium relational database applications such as MySQL, SQL Server, and PostgreSQL.


The table below compares the performances of SSD and Premium Cloud Storage.

|        Performance Metric       | SSD                                                    | Premium Cloud Storage                                                | 
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | 
| Random IOPS       | Maximum random IOPS = 1800 + storage capacity (GB) × 30<br/>Maximum random IOPS does not exceed 26,000 | Maximum random IOPS = 1,800 + storage capacity (GB) × 8<br>Maximum random IOPS does not exceed 6,000 |  
| Throughput (MB/sec) | Maximum throughput = 120 + storage capacity (GB) × 0.2<br/>Maximum throughput does not exceed 260 MB/sec | Maximum throughput = 100 + storage capacity (GB) × 0.15<br>Maximum throughput does not exceed 150 MB/sec |  
| Latency           | < 3 ms                                                 | < 4 ms                                                 | 

The main difference between **SSD** and **Premium Cloud Storage** is the I/O requirement.

SSD is more suitable for I/O-intensive applications, including:
- High performance and high data reliability: Suitable for high-load, mission-critical business systems. SSD provides three-copy data redundancy and is equipped with comprehensive capabilities for data backup, snapshots, and data restoration within seconds.
- Medium and large databases: Support medium and large relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large NoSQL: Support NoSQL businesses such as HBase and Cassandra.
- Core business systems: Suitable for I/O-intensive applications and other core business systems with high requirements for data reliability.
- Big data analysis: Suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.

**Premium Cloud Storage is suitable for the following data scenarios**:
- Suitable for small and medium databases and web servers. Provide long-term and stable I/O performance.
- Suitable for scenarios with balanced requirements for storage capacity and performance, such as enterprise office services and log services.
- Meet I/O requirements for core business testing and the development of joint testing environments.
  

Pricing for the two types of cloud disks varies with region. High-performance SSD generally has the highest price. For pricing details, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
