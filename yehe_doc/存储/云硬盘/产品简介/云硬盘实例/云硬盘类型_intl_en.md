Cloud Block Storage(CBS) is a highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone and expandable disk for CVMs. It provides data storage at the data block level and uses a three-copy distributed mechanism to ensure data reliability. CBS provides two cloud disks including**SSD** and **Premium Cloud Storage**, which have different performance, features and prices. You can select a cloud disk according to the requirements of your deployed applications.

- **SSD**: based on the NVMe SSD storage, it uses a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O capability, and data security up to 99.9999999%. SSD is suitable for scenarios with high requirements for I/O performance.
- **Premium Cloud Storage**: as a hybrid storage type, it resembles SSD providing high-performance storage based on Cache, and uses a three-copy distributed mechanism to ensure data reliability. Premium Cloud Storage is suitable for mid and small-sized applications with high requirements for data reliability and standard requirements for performance, as well as for mid and small-sized relational database applications such as MySQL, SQL Server, and PostgreSQL.


Performance differences between **SSD**, and **Premium cloud storage** are as follows:

|    Metric           | SSD                                                    | Premium Cloud Storage                                                 | 
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | 
| Random IOPS       | Maximum random IOPS = 1800 + Storage capacity (GB) × 30<br/>Maximum random IOPS does not exceed 26000 | Maximum random IOPS = 1800 + Storage capacity (GB) × 8<br>Maximum random IOPS does not exceed 6000 | 
| Throughput (MB/s) | Maximum throughput = 120 + Storage capacity (GB) × 0.2<br/>Maximum throughput does not exceed 260 MB/s | Maximum throughput = 100 + Storage capacity (GB) × 0.15<br>Maximum throughput does not exceed 150 MB/s | 
| Latency           | < 3ms                                                 | < 4ms                                                 | 

Main difference between **SSD** and **Premium Cloud Storage** is I/O requirement.

**SSD is more suitable for intensive I/O scenarios**, such as:
- Data storage with high performance and high reliability: suitable for high-load, mission-critical business systems. Provide the three-copy data redundancy mechanism to back up your data and snapshots, and recover data within seconds.
- Mid and large-sized databases: support mid and large-sized relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large-sized NoSQL: satisfy storage performance requirements of NoSQL businesses such as HBase and Cassandra.
- Core business systems: suitable for I/O-intensive applications and other core business systems with high requirements for data reliability.
- Big data analysis: suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.

**Premium Cloud Storage is suitable for the following data scenarios**:
- Suitable for mid and small-sized databases and web servers. Provide long-term and stable I/O performance
- Suitable for scenarios with balanced requirements for storage capacity and performance, such as enterprise office services and log services.
- Satisfy I/O requirements of core business testing and developing joint testing environments.
  

Pricing of the two cloud disks varies with region. Generally, high-performance SSD is the most expensive. For pricing details, see [Pricing List](https://intl.cloud.tencent.com/document/product/362/2413).
