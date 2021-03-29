TencentDB for MySQL supports three types of architectures: single-node, two-node, and three-node. This document describes the three-node architecture.

- Three-node instances adopt a one-source-two-replica architecture and support strong sync replication. They guarantee strong data consistency through real-time hot backup and provide finance-grade reliability and high availability.
- Three-node instances support two resource isolation policies: general and dedicated. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).

## Use Cases
Ideal for industries such as gaming, internet, IoT, retail, e-commerce, logistics, insurance, and securities.

## Features
- Supports such source/replica replication modes as async (default), strong sync, and semi-sync.
- Supports a complete set of features including read-only replicas, security groups, data migration, and multi-AZ deployment. For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- Achieves a high availability of up to 99.99%. For more information, see [TencentDB Service Level Agreement (New Version)](https://intl.cloud.tencent.com/zh/document/product/301/30977).
- Deploys data nodes on powerful hardware devices and uses local NVMe SSD disks as underlying storage with an IOPS of up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to the specific configuration, page size, and business load).

## Basic Framework Diagram
![](https://main.qcloudimg.com/raw/456eb478b8090f0ddd2e07ec28d010d2.png)

## Upgrading
- The engine versions of TencentDB for MySQL can be upgraded. For more information, see [Upgrading Database Engines](https://intl.cloud.tencent.com/document/product/236/8126).
- The kernel minor versions of TencentDB for MySQL can be upgraded automatically or manually. For more information, see [Upgrading Kernel Minor Versions](https://intl.cloud.tencent.com/document/product/236/36816).

