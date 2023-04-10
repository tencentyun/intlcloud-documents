TencentDB for MySQL supports three types of architectures: single-node, two-node, and three-node. This document describes the three-node architecture.

- Three-node instances are built on a one-source-two-replica architecture that supports strong sync replication. They deliver finance-grade reliability and high availability by ensuring strong data consistency with real-time hot backup.
- Three-node instances support two resource isolation policies: general and dedicated. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).

## Use cases
They are widely used in a variety of industries, including gaming, the internet, IoT, retail, e-commerce, logistics, insurance, and securities.

## Features
- The three-node architecture supports such source/replica replication modes as async (default), strong sync, and semi-sync.
- The three-node architecture supports a complete set of features including read-only instances, disaster recovery instances, security groups, data migration, and multi-AZ deployment. For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- The three-node architecture achieves a high availability of up to 99.99%. For more information, see [Service Level Agreement](https://intl.cloud.tencent.com/document/product/236/30978).
- The three-node instance provides multiple replicas to guarantee data persistence. The source node data can be synced to the replica node; the source instance data can be synced to the read-only instances (if any). This architecture ensures data security and achieves a data persistence of up to 99.99999%.
- The three-node architecture deploys data nodes on powerful hardware devices and uses local NVMe SSD disks as underlying storage with an IOPS of up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to the specific configuration, page size, and business load).
- You can deploy the two replica nodes of a three-node instance in the same AZ (e.g., Beijing Zone 5), but TencentDB's default node distribution policy ensures that they are deployed on different physical servers. You can also deploy the two replica nodes in different AZs (e.g., one replica node in Beijing Zone 5 and the other in Beijing Zone 7).

## Basic framework diagram
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rfRy430_1.png)

## Upgrading
- The engine versions of TencentDB for MySQL can be upgraded. For more information, see [Upgrading Database Engine](https://intl.cloud.tencent.com/document/product/236/8126).
- The kernel minor versions of TencentDB for MySQL can be upgraded automatically or manually. For more information, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816).

