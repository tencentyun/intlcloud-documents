TencentDB for MySQL supports four types of architectures: the High-availability Edition, the Finance Edition, the Single-node High IO Edition, and the Basic Edition. This document describes the Basic Edition.

The Basic Edition adopts a single-node deployment method and offers extremely high cost effectiveness.

## Use Cases
We do not recommend the Basic Edition for the business production environment. It is more suitable for personal learning, small websites, non-core small enterprise systems, and medium-to-large enterprise development and testing.

## Features
- Supports computation-storage separation. If a compute node fails, fast recovery can be achieved by switching to another node. Underlying data is stored in three copies on CBS, which ensures a certain level of data reliability and enables quick data restoration from disk snapshots in case of disk failures.
- Offers over 20 monitoring metrics such as database connection, access, and resource and supports configuring alarm policies as needed. Compared with a self-created CVM-based database, a Basic Edition instance is also deployed on a CVM instance but is more convenient and provides higher database performance at a 40% lower cost.
- Uses cost-effective premium cloud disks with stable performance as its underlying storage media, which makes them suitable for 90% of I/O scenarios. The IOPS calculation formula is {min 1,500 + 8 * capacity, max 4,500}. For example, the IOPS value range of a 50 GB disk is {min 1,900, max 4,500}.

## Basic Framework Diagram
![Alt text](https://main.qcloudimg.com/raw/fc709a3c5b65fd750ebb3ccb86ed8408.png)

>!As the Basic Edition adopts a single-node architecture, when the node fails, it takes slightly longer to recover than the CVM (due to instance startup and data restoration). If your business requires high availability, we recommend you use MySQL instances of the High-availability Edition or the Finance Edition.

