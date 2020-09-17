TencentDB for MySQL supports four types of architectures: the High-availability Edition, the Finance Edition, the Single-node High IO Edition, and the Basic Edition. Currently, only the High-Availability Edition can be upgraded to the Finance Edition.

<span id = "gaokeyongban"></span>
## High-availability Edition
The High-availability Edition adopts a highly available one-source-one-replica architecture and supports real-time hot backup, automatic detection of failure, and automatic failover. It is ideal for industries such as gaming, internet, IoT, retail, e-commerce, logistics, insurance, and securities.
Its features are highlighted below:
- Offers two source/replica replication modes: async (default) and semi-sync. You can change the replication mode or [upgrade to the Finance Edition](https://intl.cloud.tencent.com/document/product/236/35986) (with the one-source-two-replica strong sync mode) on the instance details tab in the [console](https://console.cloud.tencent.com/cdb).
- Supports a complete set of features including read-only instances, disaster recovery instances, security groups, data migration, and multi-AZ deployment. For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- Achieves a high availability of up to 99.95%. For more information, see [TencentDB Service Level Agreement (New Version)](https://intl.cloud.tencent.com/document/product/301/30977).
- Its data nodes are deployed on powerful hardware devices and its underlying storage uses local NVMe SSD disks with an IOPS of up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to the specific configuration, page size, and business load).

See below for its architecture:
![Alt text](https://main.qcloudimg.com/raw/baf6c165620f79a5dd5f56b6a02d9eb0.svg)


<span id = "jrb"></span>
## Finance Edition
>?The former one-source-two-replica High-availability Edition with strong sync replication has been renamed as the Finance Edition. The edition name of the existing one-source-two-replica instances displayed in the console will be updated accordingly.
>
The Finance Edition adopts a one-source-two-replica architecture (three nodes in total) and supports strong sync replication. It guarantees strong data consistency through real-time hot backup and provides finance-grade reliability and high availability.
- Source/replica replication mode: strong sync
- Supports a complete set of features including read-only instances, disaster recovery instances, security groups, data migration, and multi-AZ deployment. For more information, see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- Achieves a high availability of up to 99.99%. For more information, see [TencentDB Service Level Agreement (New Version)](https://intl.cloud.tencent.com/document/product/301/30977).
- Its data nodes are deployed on powerful hardware devices and its underlying storage uses local NVMe SSD disks with an IOPS of up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to the specific configuration, page size, and business load).

See below for its architecture:
![](https://main.qcloudimg.com/raw/09f1ed1756fd1b7e533a5bbe4c937b0b.png)


<span id = "danjiedian"></span>
## Single-node High IO Edition
The Single-node High IO Edition adopts a single-physical node architecture with high cost performance. It uses local NVMe SSD disks for underlying storage with excellent IO performance and is ideal for [read-only instances](https://intl.cloud.tencent.com/document/product/236/7270) to share business read load in various industries with read/write separation requirements.

See below for its architecture:
![Alt text](https://main.qcloudimg.com/raw/9c18abaf213f5b2c66f36e538eb86273.svg)
>!
>- Single-node deployment is susceptible to single points of failure. If only one read-only instance is purchased, it is impossible to ensure high availability for your business since a failure of the single read-only instance will lead to business interruptions.
>- As the time taken to recover a single read-only instance depends on the business data volume, the recovery time cannot be guaranteed. As a result, if your business requires high availability, we recommend you purchase at least two read-only instances for the [RO group](https://intl.cloud.tencent.com/document/product/236/11361).


<span id = "jichuban"></span>
## Basic Edition
The Basic Edition adopts a single-node deployment method and offers extremely high cost effectiveness. Its features are highlighted below:
- Supports computation-storage separation. If a compute node fails, fast recovery can be achieved by switching to another node. Underlying data is stored in three copies on CBS, which ensures a certain level of data reliability and enables quick data restoration from disk snapshots in case of disk failures.
- Offers over 20 monitoring metrics such as database connection, access, and resource and supports configuring alarm policies as needed. Compared with a self-created CVM-based database, a Basic Edition instance is also deployed on a CVM instance but is more convenient and provides higher database performance at a 40% lower cost.
- Uses cost-effective premium cloud disks with stable performance as its underlying storage media, which makes them suitable for 90% of I/O scenarios. The IOPS calculation formula is {min 1,500 + 8 * capacity, max 4,500}. For example, the IOPS value range of a 50 GB disk is {min 1,900, max 4,500}.

See below for its architecture:
![Alt text](https://main.qcloudimg.com/raw/2293e213a7908bd8de95fa21c141c9eb.svg)

>!
> - We do not recommend the Basic Edition for the business production environment. It is more suitable for personal learning, small websites, non-core small corporate systems, and medium-to-large corporate development and testing.
> - As the Basic Edition adopts a single-node architecture, when the node fails, it takes slightly longer to recover than the CVM (due to instance startup and data restoration). If your business requires high availability, we recommend you use MySQL instances of the High-availability Edition or the Finance Edition.


