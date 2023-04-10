TencentDB for MySQL supports three types of architectures: single-node, two-node, and three-node. This document describes the single-node architecture.

Single-node instances support different resource isolation policies: basic (formerly basic edition), basic (cloud disk edition), and general (for read-only instances). For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).

## Single-Node - Basic (Cloud Disk Edition)
### Use cases
The single-node architecture has only one database node, so it is very cost-effective and suitable for business scenarios that don't require a high availability, such as testing, development, and learning.

### Features
- The underlying storage adopts SSD or Enhanced SSD cloud disks.
 - SSD cloud disk: It is an all-flash cloud disk storage type with NVMe SSD as the storage media. It provides low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% (nine nines) data security. It is suitable for scenarios that require a high I/O performance.
 - Enhanced SSD cloud disk: It is based on Tencent Cloud's latest storage engine, NVMe SSD storage media and the latest network infrastructure. It provides high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999% (nine nines), making it suitable for I/O-intensive applications with high requirements for latency. Uniquely, the performance and capacity of Enhanced SSD cloud disks can be independently adjusted to meet your requirements.
- Random IOPS formula for SSD cloud disk: Random IOPS = min{1800 + capacity (GiB) * 30, 26000}.
- Throughput formula for SSD cloud disk (MB/s): Throughput = min{120 + capacity (GiB) * 0.2, 260}.
- Random IOPS formula for Enhanced SSD cloud disk: Random IOPS = min{1800 + capacity (GiB) * 50, 50000}.
- Throughput formula for Enhanced SSD cloud disk (MB/s): Throughput = min{120 + capacity (GiB) * 0.5, 350}.

>!
>- As basic instances of cloud disk edition take a long time to recover and don't provide an SLA, we recommend that you use the two-node or three-node version for production environments, which ensures up to 99.99% availability.
>- In order to ensure the data availability and recoverability of the database instance, a small part (5%) of the disk space is used as the system protection space, which protects the data in the instance but cannot store data.
>- Enhanced SSD cloud disk is supported only in certain regions as displayed on the purchase page for single-node instances of cloud disk edition.

### Basic framework diagram
![](https://staticintl.cloudcachetci.com/yehe/backend-news/KNNI786_4.png)

## Single-Node - Basic (Formerly Basic Edition - Disused)
### Use cases
We do not recommend basic single-node instances for the business production environment. It is more suitable for personal learning, small websites, non-core small enterprise systems, and medium-to-large enterprise development and testing.

### Features
- Supports computation-storage separation. If a compute node fails, fast recovery can be achieved by switching to another node. Underlying data is stored in three copies on cloud disks, which ensures a certain level of data reliability and enables quick data restoration from disk snapshots in case of disk failures.
- Offers over 20 monitoring metrics such as database connection, access, and resource and supports configuring alarm policies as needed. Compared with a self-created CVM-based database, a basic single-node instance is also deployed on a CVM instance but is more convenient and provides higher database performance at a 40% lower cost.
- Uses cost-effective premium cloud disks with stable performance as its underlying storage media, which makes them suitable for 90% of I/O scenarios. The IOPS calculation formula is {min 1,500 + 8 * capacity, max 4,500}. For example, the IOPS value range of a 50 GB disk is {min 1,900, max 4,500}.

### Basic framework diagram
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZyXS008_5.png)

>!As it adopts a single-node architecture, when the node fails, it takes slightly longer to recover than CVM (due to instance startup and data restoration). If your business requires high availability, we recommend that you use two-node or three-node MySQL instances.

## General Single-Node Instances
### Use cases
Currently, it is ideal only for [read-only instances](https://intl.cloud.tencent.com/document/product/236/7270) in various industries with read/write separation requirements.

### Features
It uses local NVMe SSD disks for underlying storage with excellent IO performance and is ideal for [read-only instances](https://intl.cloud.tencent.com/document/product/236/7270) to share business read load.

### Basic framework diagram
![](https://staticintl.cloudcachetci.com/yehe/backend-news/w7Y5168_6.png)

>!
>- Single-node deployment is susceptible to single points of failure. If only one read-only instance is purchased, it is impossible to ensure high availability for your business, because a failure of the single read-only instance will lead to business disruption.
>- As the time taken to recover a single read-only instance depends on the business data volume, the recovery time cannot be guaranteed. As a result, if your business requires high availability, we recommend that you purchase at least two read-only instances for the read-only group as instructed in [Managing the RO Group of Read-Only Instance](https://intl.cloud.tencent.com/document/product/236/11361).

### Relevant operations
- You can create one or more read-only instances, which can be applied to read/write separation and one-source-multiple-replica application scenarios. For more information, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/236/7270).
- You can create one or more read-only instances and put them in an RO group to ensure availability. For more information, see [Managing the RO Group of Read-Only Instance](https://intl.cloud.tencent.com/document/product/236/11361).

