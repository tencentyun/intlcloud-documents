TencentDB for MySQL supports three types of architectures: single-node, two-node, and three-node. This document describes the single-node architecture.

Single-node instances support two resource isolation policies: basic and general. Basic single-node instances are formerly known as the Basic Edition, and read-only replicas adopt the general single-node architecture. For more information, please see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).

## Basic Single-node Instances
### Use cases
We do not recommend basic single-node instances for the business production environment. It is more suitable for personal learning, small websites, non-core small enterprise systems, and medium-to-large enterprise development and testing.

### Features
- Supports computation-storage separation. If a compute node fails, fast recovery can be achieved by switching to another node. Underlying data is stored in three copies on cloud disks, which ensures a certain level of data reliability and enables quick data restoration from disk snapshots in case of disk failures.
- Offers over 20 monitoring metrics such as database connection, access, and resource and supports configuring alarm policies as needed. Compared with a self-created CVM-based database, a basic single-node instance is also deployed on a CVM instance but is more convenient and provides higher database performance at a 40% lower cost.
- Uses cost-effective premium cloud disks with stable performance as its underlying storage media, which makes them suitable for 90% of I/O scenarios. The IOPS calculation formula is {min 1,500 + 8 * capacity, max 4,500}. For example, the IOPS value range of a 50 GB disk is {min 1,900, max 4,500}.

### Basic framework diagram
![Alt text](https://main.qcloudimg.com/raw/fc709a3c5b65fd750ebb3ccb86ed8408.png)

>!As it adopts a single-node architecture, when the node fails, it takes slightly longer to recover than CVM (due to instance startup and data restoration). If your business requires high availability, we recommend you use two-node or three-node MySQL instances.

## General Single-node Instances
### Use cases
Currently, it is ideal only for [read-only replicas](https://intl.cloud.tencent.com/document/product/236/7270) in various industries with read/write separation requirements.

### Features
It uses local NVMe SSD disks for underlying storage with excellent IO performance and is ideal for [read-only instances](https://intl.cloud.tencent.com/document/product/236/7270) to share business read load.

### Basic framework diagram
![Alt text](https://main.qcloudimg.com/raw/769ab41c522200ebfabfb4326d603fbb.svg)
>!
>- Single-node deployment is susceptible to single points of failure. If only one read-only replica is purchased, it is impossible to ensure high availability for your business, because a failure of the single read-only replica will lead to business disruption.
>- As the time taken to recover a single read-only replica depends on the business data volume, the recovery time cannot be guaranteed. As a result, if your business requires high availability, we recommend you purchase at least two read-only replicas for the [RO group](https://intl.cloud.tencent.com/document/product/236/11361).

### References
- You can create one or more read-only replicas, which can be applied to read/write separation and one-source-multiple-replica application scenarios. For more information, please see [Creating Read-only Replicas(https://intl.cloud.tencent.com/document/product/236/7270).
- You can create one or more read-only replicas and put them in an RO group to ensure availability. For more information, please see [RO Group of Read-only Replicas](https://intl.cloud.tencent.com/document/product/236/11361).

