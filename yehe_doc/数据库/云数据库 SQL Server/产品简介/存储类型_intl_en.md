This document describes the storage types of TencentDB for SQL Server and their uses cases, including premium local SSD, balanced SSD cloud disk, enhanced SSD cloud disk, SSD cloud disk, and premium cloud disk.

## Storage type description

| Storage Type | Description | Applicable Instance Architecture | Application Scenario |
|---------|---------|---------|---------|
| Premium local SSD | It is a high I/O local disk storage type, which has an excellent I/O throughput. A 90-core 720 GB MEM TencentDB for SQL Server instance can sustain up to 4.5 million TPM. | Two-node (formerly High Availability/Cluster Edition) | Business scenarios that have extremely high requirements for storage I/O performance and high-availability architecture at the application layer, such as online games, ecommerce, ERP software services, video live streaming, and media. |
| Balanced SSD cloud disk | It is an entry-level all-flash block storage product provided by Tencent Cloud and highly cost-effective. |<li>Two-node (formerly High Availability/Cluster Edition) <br><li>Single-node (formerly Basic Edition) | Medium applications with high requirements for data reliability and standard requirements for performance, such as web/app servers, business logical processing, KV services, as well as basic database services. |
| Enhanced SSD cloud disk | It is based on Tencent Cloud's latest storage engine, NVMe SSD storage media and the latest network infrastructure. It employs a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O, and data availability up to 99.9999999% (nine nines). |<li>Two-node (formerly High Availability/Cluster Edition) <br><li>Single-node (formerly Basic Edition) | Business scenarios that have extremely high requirements for storage I/O performance and high-availability architecture at the application layer, such as online games, ecommerce, ERP software services, and video live streaming. |
| SSD cloud disk | All-flash cloud disk storage type with NVMe SSD as the storage media. It adopts a three-copy distributed storage mechanism to provide low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% (nine nines) data security. | Single-node (formerly Basic Edition) | Application scenarios such as I/O-intensive applications and small and medium relational databases. |
| Premium cloud disk | It is a hybrid storage type. It adopts the cache mechanism to provide a high-performance SSD-like storage, and employs a three-copy distributed mechanism to ensure data reliability. | Single-node (formerly Basic Edition) | Small and medium application scenarios that require high data reliability and moderate performance, such as web/app servers, business logic processing, and small and medium websites. |


## Storage type selection
You can select the storage type after selecting the instance architecture on the [TencentDB for SQL Server purchase page](https://buy.cloud.tencent.com/sqlserver).
![](https://qcloudimg.tencent-cloud.cn/raw/7cf42a49c0b224bfc0c782749e61a0c1.png)

## Storage type comparison

| Storage Type         | I/O Performance                                            | Maximum Disk Capacity (GB) |
| -------------- | --------------------------------------------------- | ---------------------------- |
| Premium local SSD | Low I/O latency and higher I/O throughput than cloud disk | 6,000                         |
| Balanced SSD cloud disk | Medium I/O throughput | 32000                        |
| Enhanced SSD cloud disk | Ultra high I/O throughput | 32000                         |
| SSD cloud disk     | Excellent I/O throughput                                    | 3,000                         |
| Premium cloud disk   | Stable I/O performance                                    | 3,000                         |

  
