Cloud Block Storage (CBS) is a highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone and expandable disk for CVMs. CBS uses a three-copy distributed mechanism to store data at the data block level and ensure data reliability. CBS is classified into three types: **Premium Cloud Storage**, **SSD**, and **Enhanced SSD**. Each type has unique performance and characteristics, and the price varies, making CBS suitable for different use cases.

>!
>- Currently, Enhanced SSD is only available in Guangzhou Zone 3, Guangzhou Zone 4, Shanghai Zone 2, Shanghai Zone 3, Shanghai Zone 5, Beijing Zone 3, Beijing Zone 4, Chengdu Zone 1, Chongqing Zone 1, Nanjing Zone 1, Nanjing Zone 2, and Qingyuan Zone 1. It will be supported in more availability zones.
>- Enhanced SSD only supports mounting to S5, M5, SA2, IT3, and D3 models created after August 1, 2020, or a new release in the future. **The performance of Enhanced SSD cannot be assured if it is mounted to earlier or existing instances**.
>- Enhanced SSD cannot be used as the system disk.
>- Enhanced SSD cannot be encrypted.
>- Enhanced SSD cannot be upgraded from other disk types.

- **Premium Cloud Storage**: Tencent Cloud Premium Cloud Storage is a hybrid storage type. It adopts the Cache mechanism to provide a high-performance SSD-like storage, and employs a three-copy distributed mechanism to ensure data reliability. Premium Cloud Storage is suitable for small and medium applications with high requirements for data reliability and standard requirements for performance, such as Web/App servers, business logical processing, as well as small and medium sites.
- **SSD**: SSD uses NVMe SSD as the storage media, and employs a three-copy distributed mechanism. It provides storage service with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for applications with high requirements for I/O performance.
- **Enhanced SSD**: Enhanced SSD is provided with the latest storage engine design, NVMe SSD storage media and the latest network infrastructure. It employs a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for I/O-intensive applications with high requirements for latency, such as large databases and NoSQL.


The table below compares the performances of **Premium Cloud Storage**, **SSD** and **Enhanced SSD**.

|        Performance Metric       |               Enhanced SSD             |SSD                                                    | Premium Cloud Storage                                                 |
| -------------- | ------------------------------|------------------------------ | ------------------------------------------------------------ |
| Random IOPS       | Maximum random IOPS = 1800 + storage capacity (GB) × 50<br/>Maximum random IOPS does not exceed 50,000 | Maximum random IOPS = 1800 + storage capacity (GB) × 30<br/>Maximum random IOPS does not exceed 26,000 | Maximum random IOPS = 1,800 + storage capacity (GB) × 8<br>Maximum random IOPS does not exceed 6,000 |
| Throughput (MB/sec) | Maximum throughput = 120 + storage capacity (GB) × 0.5<br/>Maximum throughput does not exceed 350 MB/sec | Maximum throughput = 120 + storage capacity (GB) × 0.2<br/>Maximum throughput does not exceed 260 MB/sec |Maximum throughput = 100 + storage capacity (GB) × 0.15<br>Maximum throughput does not exceed 150 MB/sec |
| Latency | 0.3-1 ms | 0.5-3 ms | 0.8-4 ms|

The main difference among **Enhanced SSD**, **SSD** and **Premium Cloud Storage** is the I/O requirement.

**Enhanced SSD is more suitable for latency-sensitive or I/O-intensive applications**, including:
- High performance and high data reliability: suitable for high-load, mission-critical business systems. SSD provides three-copy data redundancy and is equipped with comprehensive capabilities for data backup, snapshots, and data restoration within seconds.
- Medium and large databases: support medium and large relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large NoSQL: support NoSQL businesses such as HBase and Cassandra.
- ElasticSearch: support low-latency ES storage.
- Video service: suitable for applications with high requirements for storage bandwidth, such as audio/video encoding and decoding, live and recorded streaming.
- Core business systems: suitable for I/O-intensive applications and other core business systems with high requirements for data reliability.
- Big data analysis: suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.

**SSD is more suitable for applications with high or regular load**, including:
- Medium and large databases: support medium and large relational database applications including MySQL.
- Image processing: support data analysis and storage businesses including image processing.

**Premium Cloud Storage is mainly suitable for the following data scenarios**:
- Suitable for small and medium databases and Web/App servers. Provide long-term and stable I/O performance.
- Suitable for scenarios with balanced requirements for storage capacity and performance, such as enterprise office services.
- Meet I/O requirements for core business testing and the development of joint testing environments.
  

For pricing details of cloud disks, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
