
TencentDB for MySQL supports three types of architectures: single-node, two-node, and three-node. This document describes the two-node architecture.

- Two-node instances are built on a highly available one-source-one-replica architecture that implements real-time hot backup, automatic failure detection, and automatic failover.
- Two-node instances support two resource isolation policies: general and dedicated. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).

## Use cases
They are widely used in a variety of industries, including gaming, the internet, IoT, retail, e-commerce, logistics, insurance, and securities.

## Features
- The two-node architecture offers two source/replica replication modes: async (default) and semi-sync. You can modify the replication mode on the instance details page or when upgrading to the three-node architecture as instructed in [Upgrading Two-Node Instances to Three-Node Instances](https://intl.cloud.tencent.com/document/product/236/35986) in the [console](https://console.cloud.tencent.com/cdb).
- The two-node architecture supports a complete set of features including read-only instances, disaster recovery instances, security groups, data migration, and multi-AZ deployment. For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- The two-node architecture achieves a high availability of up to 99.95%. For more information, see [Service Level Agreement](https://intl.cloud.tencent.com/document/product/236/30978).
- The two-node instance provides multiple replicas to guarantee data persistence. The source node data can be synced to the replica node; the source instance data can be synced to the read-only instances (if any). This architecture ensures data security and achieves a data persistence of up to 99.99999%.
- The two-node architecture deploys data nodes on powerful hardware devices and uses local NVMe SSD disks as underlying storage with an IOPS of up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to the specific configuration, page size, and business load).

## Basic framework diagram
![](https://main.qcloudimg.com/raw/19d5619f983d3dc550b3218c0520b447.png)

## Upgrading
- The engine versions of TencentDB for MySQL can be upgraded. For more information, see [Upgrading Database Engine](https://intl.cloud.tencent.com/document/product/236/8126).
- TencentDB for MySQL can be upgraded from the two-node architecture to the three-node architecture. For more information, see [Upgrading Two-Node Instances to Three-Node Instances](https://intl.cloud.tencent.com/document/product/236/35986).
- The kernel minor versions of TencentDB for MySQL can be upgraded automatically or manually. For more information, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816).

