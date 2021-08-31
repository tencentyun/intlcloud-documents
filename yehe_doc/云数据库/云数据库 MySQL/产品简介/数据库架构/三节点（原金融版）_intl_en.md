TencentDB for MySQL supports three types of architectures: single-node, two-node, and three-node. This document describes the three-node architecture.

- Three-node instances adopt a one-source-two-replica architecture and support strong sync replication. They guarantee strong data consistency through real-time hot backup and provide finance-grade reliability and high availability.
- Three-node instances support two resource isolation policies: general and dedicated. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).

## Use Cases
Three-node instances are ideal for industries such as gaming, internet, IoT, retail, e-commerce, logistics, insurance, and securities.

## Features
- The three-node architecture supports such source/replica replication modes as async (default), strong sync, and semi-sync.
- The three-node architecture supports a complete set of features including read-only instances, security groups, data migration, and multi-AZ deployment. For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- The three-node architecture achieves a high availability of up to 99.99%. For more information, see [TencentDB Service Level Agreement (New Version)](https://intl.cloud.tencent.com/document/product/301/30977).
- The three-node instance provides multiple replicas to guarantee data persistence. The source node data can be synced to the replica nodes; the source instance data can be synced to the read-only instances (if any). This architecture ensures data security and achieves a data persistence of up to 99.99999%.
- The three-node architecture deploys data nodes on powerful hardware devices and uses local NVMe SSD disks as underlying storage with an IOPS of up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to the specific configuration, page size, and business load).
- You can deploy the two replica nodes of a three-node instance in the same availability zone (e.g., Beijing Zone 5), but the TencentDB’s default node distribution strategy ensures that they are deployed on different physical servers. You can also deploy the two replica nodes in different availability zones (e.g., one replica node in Beijing Zone 5 and the other in Beijing Zone 7).


## Upgrading
- The engine versions of TencentDB for MySQL can be upgraded. For more information, see [Upgrading Database Engines](https://intl.cloud.tencent.com/document/product/236/8126).
- The kernel minor versions of TencentDB for MySQL can be upgraded automatically or manually. For more information, see [Upgrading Kernel Minor Versions](https://intl.cloud.tencent.com/document/product/236/36816).

