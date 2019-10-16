Cloud Block Storage is a highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone and expandable disk for CVMs. It provides data storage at the data block level and uses a three-copy distributed mechanism to ensure data reliability. Cloud Block Storage provides three types of cloud disks, **SSD cloud storage**, **premium cloud storage** and **HDD cloud storage**. Disk performance, features and pricing vary by type, you can choose according to the requirements of your deployed applications.

- **SSD cloud storage**: SSD cloud disks are based on NVMe SSD storage, and use a three-copy distribution mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O capability, and data security up to 99.9999999%. SSD disks are suitable for scenarios with relatively high requirements for I/O performance.
- **Premium cloud storage**: Premium cloud storage by Tencent Cloud is a hybrid storage type. It provides a high-performance storage capability that approaches SSD, and uses a three-copy distribution mechanism to ensure data reliability. Premium cloud storage is suitable for mid- and small-sized applications with high data reliability requirements and normal performance requirements, as well as for mid- to small-sized relational database applications, such as MySQL, SQL Server, and PostgreSQL.
- **HDD cloud storage**: HDD cloud disk is the first generation cloud disk type provided by Tencent Cloud. It is suitable for business scenarios with low I/O loads where data is not accessed frequently. It uses magnetic storage, and a three-copy distribution mechanism to implement highly reliable data storage.

Performance differences between **SSD cloud storage**, **Premium cloud storage**, and **HDD cloud storage** are as follows:

|               | SSD cloud storage                                                    | Premium cloud storage                                                 | HDD cloud storage                                                   |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Random IOPS       | Maximum random IOPS = 1800 + Storage capacity (GB) × 30<br/>Maximum random IOPS does not exceed 26000 | Maximum random IOPS = 1800 + Storage capacity (GB) × 8<br>Maximum random IOPS does not exceed 6000 | Provide specification options of 10GB - 16000GB and random IOPS performance of up to several hundreds |
| Throughput (MB/s) | Maximum throughput = 120 + Storage capacity (GB) × 0.2<br/>Maximum throughput does not exceed 260MB/s | Maximum throughput = 100 + Storage capacity (GB) × 0.15<br>Maximum throughput does not exceed 150MB/s | Support I/O throughput performance of 50MB/s                            |
| Latency           | <3ms                                                 | <4ms                                                 | -                                                         |

Main difference between **SSD cloud storage** and **Premium cloud storage** is I/O requirement.

**SSD cloud storage is more suitable for intensive I/O scenarios, such as:
- High performance, high data reliability: Suitable for high-load, mission-critical business systems. Provide three-copy data redundancy, and comprehensive capabilities for data backup, snapshots, and recovery within seconds.
- Mid- and large-sized databases: Support mid- and large-sized relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large-sized NoSQL: Satisfy storage performance requirements of NoSQL businesses such as HBase and Cassandra.
- Core business systems: For I/O-intensive applications and other core business systems with high requirements for data reliability .
- Big Data analysis: Provide distributed processing capabilities for data  at TB and PB levels, suitable for data analysis, data mining, business intelligence, and more.

**Premium cloud storage is primarily suitable for the following data scenarios**:
- Suitable for mid- to small-sized databases and web servers, provide long-term and stable I/O performance.
- Suitable for scenarios with balanced requirements for storage capacity and performance, such as enterprise office services and log services.
- Satisfy I/O requirements for core business testing and developing joint testing environments.
  

Pricing for the three types of cloud disks varies by region. Generally, high-performance SSD cloud storage is the most expensive. For more billing information on the three types of cloud storage, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

