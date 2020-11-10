TencentDB for MySQL supports four types of architectures: the High-availability Edition, the Finance Edition, the Single-node High IO Edition, and the Basic Edition. This document describes the High-availability Edition.


The High-availability Edition adopts a highly available one-source-one-replica architecture and supports real-time hot backup, automatic detection of failure, and automatic failover.

## Use Cases
Ideal for industries such as gaming, internet, IoT, retail, e-commerce, logistics, insurance, and securities.

## Features
- Offers two source/replica replication modes: async (default) and semi-sync. You can change the replication mode or [upgrade to the Finance Edition](https://intl.cloud.tencent.com/document/product/236/35986) (with the one-source-two-replica strong sync mode) on the instance details tab of the instance in the [console](https://console.cloud.tencent.com/cdb).
- Supports a complete set of features including read-only instances, disaster recovery instances, security groups, data migration, and multi-AZ deployment. For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- Achieves a high availability of up to 99.95%. For more information, see [TencentDB Service Level Agreement (New Version)](https://intl.cloud.tencent.com/zh/document/product/301/30977).
- Its data nodes are deployed on powerful hardware devices and its underlying storage uses local NVMe SSD disks with an IOPS of up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to the specific configuration, page size, and business load).

## Basic Framework Diagram
![Alt text](https://main.qcloudimg.com/raw/19d5619f983d3dc550b3218c0520b447.png)

## Upgrading
- The engine versions of TencentDB for MySQL can be upgraded. For more information, see [Upgrading Database Engines](https://intl.cloud.tencent.com/document/product/236/8126).
- TencentDB for MySQL can be upgraded from the High-availability Edition to the Finance Edition. For more information, see [Upgrading from the High-availability Edition to the Finance Edition](https://intl.cloud.tencent.com/document/product/236/35986).
- The kernel minor versions of TencentDB for MySQL can be upgraded automatically or manually. For more information, see [Upgrading Kernel Minor Versions](https://intl.cloud.tencent.com/document/product/236/36816).
