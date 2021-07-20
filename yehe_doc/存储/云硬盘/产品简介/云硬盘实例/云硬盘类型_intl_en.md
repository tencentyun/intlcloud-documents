Cloud Block Storage (CBS) provides highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone and expandable disk for CVMs. CBS stores data at the data block level in a three-copy distributed mechanism to ensure data reliability. CBS is classified into four types: **Premium Cloud Storage**, **SSD**, **Enhanced SSD**, and **Tremendous SSD**. Each type has unique performance and characteristics, and the price varies, making CBS suitable for different use cases.

## Notes
- Currently, Enhanced SSD and Tremendous SSD are only available in certain availabilities zone. They will be supported in more availability zones.
- The performance of Enhanced SSD is only guaranteed when it’s attached to S5, M5, and SA2 models created after August 1, 2020, and all later generation models.
- **Tremendous SSD** can only be purchased and used with the Standard Storage Optimized S5se CVM instance.**
- Enhanced SSD and Tremendous SSD cannot be used as the system disk.
- Enhanced SSD and Tremendous SSD cannot be encrypted.
- Enhanced SSD and Tremendous SSD cannot be upgraded from other disk types.


## Overview
- **Premium Cloud Storage**
Tencent Cloud Premium Cloud Storage is a hybrid storage type. It adopts the Cache mechanism to provide a high-performance SSD-like storage, and employs a three-copy distributed mechanism to ensure data reliability. Premium Cloud Storage is suitable for small and medium applications with high requirements for data reliability and standard requirements for performance, such as Web/App servers, business logical processing, as well as small and medium sites.
- **SSD**
SSD is an all-flash cloud disk using NVMe SSD as the storage media, and employs a three-copy distributed mechanism. It provides storage service with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for applications with high requirements for I/O performance.
- **Enhanced SSD**
Enhanced SSD is based on Tencent Cloud’s latest storage engine, NVMe SSD storage media and the latest network infrastructure. It employs a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for I/O-intensive applications with high requirements for latency, such as large databases and NoSQL. Uniquely, the performance and capacity of Enhanced SSD cloud disks can be independently adjusted to meet your requirements.
- **Tremendous SSD**
Tremendous SSD is powered by Tencent Cloud’s latest high-performance distributed storage engine, high-speed network infrastructure, and the latest storage hardware. It boasts long-term and stable performance with ultra low latency. It is suitable for I/O-intensive and throughput-intensive workloads that require ultra low latency, such as large databases (MySQL, HBase, Cassandra, etc.), key-value storage models (etcd, rocksdb, etc.), log search service (Elasticsearch, etc.), and real-time high-bandwidth businesses (video processing, live streaming, etc.). It performs well in key transaction workloads, core database services, large-scale OLTP services, video processing, and other scenarios. The performance and capacity of Tremendous SSD cloud disks can be independently adjusted to meet your requirements.


## Performance Metrics
The table below compares the performances of the four CBS services.

| Metric | Tremendous SSD | Enhanced SSD | SSD | Premium Cloud Storage|
| ----| -----|---- | ----- | --|
| Maximum size (GB)     | 32,000 | 32,000 | 32,000 | 32,000 |
| Maximum IOPS    | 1,100,000 | 100,000 | 26,000 | 6,000 |
| Random IOPS performance      | Basic performance: random IOPS = min{4000+100 × capacity (GiB), 50000}<br>Extra performance: maximum IOPS = min{128 × extra performance, 1050000} <br> | Basic performance: random IOPS = min{1800 + 50 × capacity (GiB), 50000}<br>Extra performance: maximum IOPS = min{128 × extra performance, 50000} <br>For more information, see [Enhanced SSD Performance](https://intl.cloud.tencent.com/document/product/362/39611) | Random IOPS = min{1800 + 30 × capacity (GiB), 26000} | Random IOPS = min{1800 + 8 × capacity (GiB), 6000} |
| Maximum throughput (MB/sec)    | 4,000 MB/sec | 1,000 MB/sec | 260 MB/sec | 150 MB/sec |
| Throughput (MB/sec) performance      | Basic performance: throughput = min{120 + 0.5 × capacity (GiB), 350}<br>Extra performance: throughput = min{1 × extra performance, 3650} <br> | Basic performance: throughput = min{120 + 0.5 × capacity (GiB), 350}<br>Extra performance: throughput = min{1 × extra performance, 650} <br>For more information, see [Enhanced SSD Performance](https://intl.cloud.tencent.com/document/product/362/39611) | Throughput = min{120 + 0.2 × capacity (GiB), 260} | Throughput = min{100 + 0.15 × capacity (GiB), 150} |
| Single-thread random read/write latency | 0.1-0.5 ms | 0.3-1 ms| 0.5-3 ms | 0.8-5 ms|
|Notes| Tremendous SSD can only be purchased with the [Standard Storage Optimized S5se](https://intl.cloud.tencent.com/document/product/213/11518) instances. It cannot be independently purchased, or used on other types of CVM instances. | The performance of Enhanced SSD is only guaranteed when it’s attached to S5, M5, and SA2 and later generation models. | None | None |


>?The main difference among cloud disks is the I/O performance.

## Use Cases
**Enhanced SSD is more suitable for latency-sensitive or I/O-intensive scenarios**, including:
- High performance and high data reliability: suitable for high-load, mission-critical business systems. SSD provides three-copy data redundancy and is equipped with comprehensive capabilities for data backup, snapshots, and data restoration within seconds.
- Medium and large databases: support medium and large relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large NoSQL: support NoSQL businesses such as HBase and Cassandra.
- Elasticsearch: support low-latency ES storage.
- Video service: suitable for applications with high requirements for storage bandwidth, such as audio/video encoding and decoding, live streaming and recording playback.
- Big data analysis: suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.

**Tremendous SSD is more suitable for latency-sensitive scenarios that require ultra low latency**, including:
- Key-value (KV) storage: support rocksdb, etcd, etc. The KV storage service generally writes data to disk in the serial I/O mode, which requires ultra low latency. The single thread latency determines the overall system performance. Tremendous SSD guarantees the latency as low as tens of microseconds, making it fit for core business systems with high requirements for data reliability and availability.
- Large databases: support medium and large relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large NoSQL: support NoSQL businesses such as HBase and Cassandra.
- Elasticsearch: support low-latency ES storage.
- Video service: suitable for applications with high requirements for storage bandwidth, such as audio/video encoding and decoding, live streaming and recording playback.
- Core business systems: suitable for I/O-intensive applications and other core business systems with high requirements for data reliability.
- Big data analysis: suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.
- High performance and high data reliability: suitable for high-load, mission-critical business systems. SSD provides three-copy data redundancy and is equipped with comprehensive capabilities for data backup, snapshots, and data restoration within seconds.

**SSD is applicable for applications with high and medium loads**, including:
- Medium databases: medium and large relational database applications, such as MySQL.
- Image processing: support data analysis and storage businesses, such as image processing.

**Premium Cloud Storage is mainly suitable for the following data scenarios**:
- Small and medium databases and Web/App servers. Provide long-term and stable I/O performance.
- Scenarios that require balanced storage capacity and performance, such as enterprise office services.
- Core business testing and the front and back end debugging.

## Billing Description
For pricing details of cloud disks, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
