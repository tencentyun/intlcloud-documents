TencentDB for MySQL supports four types of architecture: High-Availability Edition, Finance Edition, Single-Node High IO Edition, and Basic Edition. Currently, only the High-Availability Edition can be upgraded to the Finance Edition.

<span id = "gaokeyongban"></span>
## High-Availability Edition
The High-Availability Edition adopts a highly available one-master-one-slave architecture and supports real-time hot backup, automatic detection of failure, and automatic failover. It is ideal for a wide variety of industries such as gaming, internet, IoT, retail, ecommerce, logistics, insurance, and securities.
Its features are highlighted as below:
- It offers two master/slave replication modes: async (default) and semi-sync. The replication mode can be changed on the "Instance Details" tab in the [console](https://console.cloud.tencent.com/cdb). You can also upgrade to the [Finance Edition](https://intl.cloud.tencent.com/document/product/236/35986) (with one-master-two-slave strong sync mode).
- It has a complete set of features including read-only instance, disaster recovery instance, security group, data migration, and multi-AZ deployment. For more information, please see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- It can achieve a high availability of up to 99.95%. For more information, please see [Service Level Agreement](https://intl.cloud.tencent.com/document/product/301/30977).
- Its data nodes are deployed on powerful hardware devices and its underlying storage uses local NVMe SSD disks with excellent IO performance. Its IOPS can be up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to specific configuration, page size, and business load).

Its architecture is as follows:
![Alt text](https://main.qcloudimg.com/raw/baf6c165620f79a5dd5f56b6a02d9eb0.svg)


<span id = "jrb"></span>
## Financial Edition
>The former one-master-two-slave High-Availability Edition with strong sync replication has been renamed as the Finance Edition. The edition name of existing one-master-two-slave instances displayed in the console has been updated accordingly.
>
The Finance Edition adopts a one-master-two-slave architecture (three nodes in total) and supports strong sync replication. It guarantees strong data consistency through real-time hot backup to provide finance-grade reliability and high availability.
- Master/slave replication mode: strong sync.
- It has a complete set of features including read-only instance, disaster recovery instance, security group, data migration, and multi-AZ deployment. For more information, please see [Strengths](https://intl.cloud.tencent.com/document/product/236/5148).
- It can achieve a high availability of up to 99.99%. For more information, please see [Service Level Agreement](https://intl.cloud.tencent.com/document/product/301/30977).
- Its data nodes are deployed on powerful hardware devices and its underlying storage uses local NVMe SSD disks with excellent IO performance. Its IOPS can be up to 240,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to specific configuration, page size, and business load).

Its architecture is as follows:
![](https://main.qcloudimg.com/raw/09f1ed1756fd1b7e533a5bbe4c937b0b.png)


<span id = "danjiedian"></span>
## Single-Node High IO Edition
The Single-Node High IO Edition employs a single-physical node architecture with high cost effectiveness. It uses local NVMe SSD disks for underlying storage with excellent IO performance. It is ideal for read-only instances as a means to share the business load in various industries that require read/write separation.

Its architecture is as follows:
![Alt text](https://main.qcloudimg.com/raw/9c18abaf213f5b2c66f36e538eb86273.svg)
>
>- Single-node deployment is susceptible to single points of failure. If only one read-only instance is purchased, it is impossible to ensure high availability for your business, because a failure of the single read-only instance will lead to business interruption.
>- As the time it takes to recover a single read-only instance is dependent on the business data volume, fast recovery cannot be guaranteed. As a result, if your business requires high availability, you are recommended to purchase at least two read-only instances for the [RO group](https://intl.cloud.tencent.com/document/product/236/11361).


<span id = "jichuban"></span>
## Basic Edition
The Basic Edition adopts a single-node deployment method and offers extremely high cost effectiveness. Its features are highlighted as below:
- It supports computation-storage separation. If a compute node fails, fast recovery can be achieved by switching to another node. Underlying data is stored in three copies on CBS, which ensures a certain level of data reliability and enables quick data restoration from disk snapshots in case of disk failures.
- It offers over 20 monitoring metrics such as database connection, access, and resource and supports configuring alarm policies as needed. Compared with a self-built CVM-based database, it is more convenient and features a higher cost performance where the cost is 40% lower.
- It uses premium cloud disks as its underlying storage media, making it suitable for 90% I/O scenarios with low costs and stable performance. The specific IOPS calculation formula is {min 1500 + 8 * capacity, max 4500}.

Its architecture is as follows:
![Alt text](https://main.qcloudimg.com/raw/2293e213a7908bd8de95fa21c141c9eb.svg)

>
> - The Basic Edition is not recommended for a business production environment; instead, it is suitable for personal learning, small websites, non-core small corporate systems, and medium-to-large corporate development and testing.
> - As it adopts a single-node architecture, when the node fails, it takes slightly longer to recover than CVM (due to instance startup and data restoration). If your business requires high availability, you are recommended to use the High-Availability Edition or Finance Edition MySQL instances.


