TencentDB for MySQL supports three types of architecture: basic edition, high availability (HA) edition, and single-node high-IO edition. Currently, you cannot switch among them.

<span id = "jichuban"></span>

## Basic Edition
The basic edition adopts a single-node deployment method and offers extremely high cost effectiveness. Its features are highlighted as below:
- It supports computation-storage separation. If a compute node fails, fast recovery can be achieved by switching to another node. Underlying data is stored in three copies on CBS, which ensures a certain level of data reliability and enables quick data restoration from disk snapshots in case of disk failures.
- It offers over 20 monitoring metrics such as database connection, access, and resource and supports configuring alarm policies as needed. Compared with a self-built CVM-based database, it is more convenient and features a higher cost performance where the cost is 40% lower.
- It uses premium cloud disks as its underlying storage media, making it suitable for 90% I/O scenarios with low costs and stable performance. The specific IOPS calculation formula is {min 1500 + 8 * capacity, max 4500}.

Its architecture is as follows:
![Alt text](https://main.qcloudimg.com/raw/2293e213a7908bd8de95fa21c141c9eb.svg)

>- The basic edition is not recommended for business production environment; instead, it is suitable for personal learning, small websites, non-core small corporate systems, and medium-to-large corporate development and testing.
> - As it adopts a single-node architecture, when the node fails, it takes slightly longer to recover than CVM (due to instance startup and data restoration). If your business requires high availability, you are recommended to use MySQL instances of high availability edition.


<span id = "gaokeyongban"></span>

## High Availability Edition
The high availability edition adopts a highly available one-master-N-slave architecture and supports real-time hot backup, automatic detection of failure, and automatic failover. It is ideal for a wide variety of industries such as gaming, internet, finance, IoT, retail, ecommerce, logistics, insurance, and securities.
Its features are highlighted as below:

- It offers three master-slave replication methods: async, semi-sync, and strong sync.
- It has a complete set of features including read-only instance, disaster recovery instance, security group, data migration, and multi-AZ deployment. For more information, see [Benefits](http://intl.cloud.tencent.com/document/product/236/5148).
- It can achieve a high availability of up to 99.95%. For more information, see [Service Level Agreement](https://intl.cloud.tencent.com/document/product/301/30977).
- Its data nodes are deployed on powerful hardware devices and its underlying storage uses local NVMe SSD disks with excellent IO performance.

Its architecture is as follows:
![Alt text](https://main.qcloudimg.com/raw/baf6c165620f79a5dd5f56b6a02d9eb0.svg)


>- The high availability edition uses the one-master-one-slave async replication method by default. You can switch to the one-master-two-slave strong sync replication method by making purchases and upgrades.
> - It uses local SSD disks for underlying storage with an IOPS of up to 500,000 (this value is the test result with MySQL's default page size of 16 KB and for your reference only. The actual value is subject to specific configuration, page size, and business load).


<span id = "danjiedian"></span>

## Single-node High-IO Edition
The single-node high-IO edition employs a single-physical node architecture with high cost effectiveness. It uses local NVMe SSD disks for underlying storage with excellent IO performance. It is ideal for read-only instances as a means to share the business load in various industries that require read/write separation.

Its architecture is as follows:
![Alt text](https://main.qcloudimg.com/raw/9c18abaf213f5b2c66f36e538eb86273.svg)


>- Single-node deployment is susceptible to single points of failure. If only one read-only instance is purchased, it is impossible to ensure high availability for your business, because a failure of the single read-only instance will lead to business interruption.
>- As the time it takes to recover a single read-only instance is dependent on the business data volume, no fast recovery can be guaranteed. As a result, if your business requires high availability, you are recommended to purchase at least two read-only instances for the [RO group](https://intl.cloud.tencent.com/document/product/236/11361).

## List of Feature Differences

| Feature     | Basic Edition             | High Availability Edition                                               | Single-node High-IO Edition                       |
| :--------- | :----------------- | :----------------------------------------------------- | :----------------------------------- |
| Version       | MySQL v5.7</li> | <li>MySQL v5.5</li><li>MySQL v5.6</li><li>MySQL v5.7</li> | <li>MySQL v5.6</li><li>MySQL v5.7</li> |
| Number of nodes     | 1                  |  ≥ 2                                                    | 1                                    |
| Specification configuration   | Up to 8 GB/1 TB        | Up to 488 GB/6 TB                                         | Up to 488 GB/6 TB                       |
| Monitoring and alarming | Available               | Available                                                   | Available                                 |
| Security group     | Unavailable             | Available                                                   | Available                                 |
| Backup       | Unavailable             | Available                                                   | Unavailable                               |
| Rollback       | Unavailable             | Available                                                   | Unavailable                               |
| Upgrade | Available               | Available                                                   | Available                                 |
| Parameter setting       | Available             | Available                                                   | Unavailable                               |
| Read-only instance   | Unavailable             | Available (only in MySQL v5.6 and v5.7)         | Available                                 |
| Disaster recovery instance   | Unavailable             | Available (only in MySQL v5.6 and v5.7)         | Unavailable                                  |
| Databases auditing   | Unavailable             | Available (only in MySQL v5.6 and v5.7)         | Unavailable                                  |
| Data migration     | Unavailable             | Available                                                   | Available                                 |
