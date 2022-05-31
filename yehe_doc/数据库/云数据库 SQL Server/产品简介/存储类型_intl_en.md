This document describes the storage types of TencentDB for SQL Server and their uses cases, including SSD cloud disk, high-performance cloud disk, and high-performance local SSD.

## Storage Type Description

| Storage Type | Description | Applicable Database Architecture | Application Scenario |
|---------|---------|---------|---------|
| SSD cloud disk | All-flash cloud disk storage type with NVMe SSD as the storage media. It adopts a three-copy distributed storage mechanism to provide low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% data security. | Basic Edition | Application scenarios such as I/O-intensive applications and small and medium relational databases. |
|  High-performance cloud disk | Hybrid storage type offered by Tencent Cloud. It provides high-performance storage capabilities close to SSD through the cache mechanism and adopts a three-copy distributed mechanism to ensure the data reliability. | Basic Edition | Small and medium application scenarios that require high data reliability and moderate performance, such as web/app servers, business logic processing, and small and medium websites. |
| High-performance local SSD | High I/O local disk storage type, which has an excellent I/O throughput. A 90-core 720 GB MEM TencentDB for SQL Server instance can sustain up to 4.5 million TPM. | Dual-Server High Availability Edition/Cluster Edition | Business scenarios that have extremely high requirements for storage I/O performance and high-availability architecture at the application layer, such as online games, ecommerce, ERP software services, video live streaming, and media. |

## Selecting Storage Type
You can select the disk type after selecting the instance model on the [TencentDB for SQL Server purchase page](https://buy.intl.cloud.tencent.com/sqlserver).
![](https://qcloudimg.tencent-cloud.cn/raw/7cf42a49c0b224bfc0c782749e61a0c1.png)

## Storage Type Comparison

| Storage Type         | I/O Performance                                            | Maximum Disk Capacity (GB) |
| -------------- | --------------------------------------------------- | ---------------------------- |
| SSD cloud disk     | Excellent I/O throughput                                    | 3,000                         |
| High-performance cloud disk   | Stable I/O performance                                    | 3,000                         |
| High-performance local SSD | Low I/O latency and higher I/O throughput than cloud disk | 6,000                         |

