Cloud Block Storage is a highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone and expandable disk for CVMs. It provides data storage at the data block level and uses a three-copy distributed mechanism to ensure data reliability. Cloud Block Storage provides three types of cloud disks, **SSD Cloud Storage**, **Premium Cloud Storage** and **HDD Cloud Storage**. Disk performance, features and pricing vary for all three types. You can select the type you need according to the requirements of your deployed applications.

- **SSD Cloud Storage**: SSD cloud disks are based on NVMe SSD storage, and use a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O capability, and data security up to 99.9999999%. SSD cloud disks are suitable for scenarios with high requirements for I/O performance.
- **Premium Cloud Storage**: Premium Coud Storage by Tencent Cloud is a hybrid storage type. It provides a high-performance storage capability that approaches SSD, and uses a three-copy distributed mechanism to ensure data reliability. Premium Cloud Storage is suitable for mid and small-sized applications with high requirements for data reliability and standard requirements for performance, as well as for mid and small-sized relational database applications such as MySQL, SQL Server, and PostgreSQL.
- **HDD Cloud Storage**: HDD cloud disks are the first generation of cloud disks provided by Tencent Cloud. It is suitable for business scenarios with low I/O loads where data is not accessed frequently. It uses magnetic storage, and a three-copy distributed mechanism to implement highly reliable data storage.

Performance differences between **SSD cloud storage**, **Premium cloud storage**, and **HDD cloud storage** are as follows:

|               | SSD Cloud Storage                                                    | Premium Cloud Storage                                                 | HDD Cloud Storage                                                   |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Random IOPS       | Maximum random IOPS = 1800 + Storage capacity (GB) × 30<br/>Maximum random IOPS does not exceed 26,000 | Maximum random IOPS = 1,800 + Storage capacity (GB) × 8<br>Maximum random IOPS does not exceed 6,000 | Provide specifications of 10 GB to 16,000 GB and random IOPS performance of up to several hundreds |
| Throughput (MB/s) | Maximum throughput = 120 + Storage capacity (GB) × 0.2<br/>Maximum throughput does not exceed 260 MB/s | Maximum throughput = 100 + Storage capacity (GB) × 0.15<br>Maximum throughput does not exceed 150 MB/s | Support I/O throughput performance of 50 MB/s                            |
| Latency           | < 3 ms                                                 | < 4 ms                                                 | -                                                         |

The main difference between **SSD Cloud Storage** and **Premium Cloud Storage** is the I/O requirement.

**SSD Cloud Storage is more suitable for intensive I/O scenarios, such as:
- High performance and high data reliability: suitable for high-load, mission-critical business systems. Provide three-copy data redundancy, and comprehensive capabilities for data backup, snapshots, and data restoration within seconds.
- Mid and large-sized databases: support mid and large-sized relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large-sized NoSQL: satisfy storage performance requirements of NoSQL businesses such as HBase and Cassandra.
- Core business systems: suitable for I/O-intensive applications and other core business systems with high requirements for data reliability.
- Big data analysis: suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.

**Premium Cloud Storage is suitable for the following data scenarios**:
- Suitable for mid and small-sized databases and web servers. Provide long-term and stable I/O performance.
- Suitable for scenarios with balanced requirements for storage capacity and performance, such as enterprise office services and log services.
- Satisfy I/O requirements for core business testing and developing joint testing environments.
  

Pricing of the three types of cloud disks varies with region. Generally, high-performance SSD Cloud Storage is the most expensive. For pricing details, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
