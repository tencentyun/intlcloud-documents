
### What is TDSQL-C for MySQL?
TDSQL-C for MySQL is a proprietary new-generation cloud native relational database developed by Tencent Cloud. It combines the strengths of traditional databases, cloud computing, and cutting-edge hardware technologies to provide elastic scalable database services, which features high performance, security, and reliability.

### How is TDSQL-C for MySQL different from traditional databases?
TDSQL-C for MySQL combines the strengths of traditional databases and cloud computing. First, it has all the five characteristics of cloud computing:
- On-demand self-service
- Broad network access
- Resource pooling
- Rapid elasticity
- Measured service

Secondly, TDSQL-C for MySQL truly implements the concept of log as a database through transformation and optimization of the open-source database kernel in combination with the SOA architecture and distributed storage. It optimizes the system performance at critical paths at the software level to reduce the costs of use.

### Why is TDSQL-C for MySQL better than traditional databases?
Compared with traditional databases, the cloud-native TDSQL-C for MySQL can store petabytes of data and provide high availability and reliability, fast and elastic configuration adjustment, and instant scaling. For more information, see [Strengths](https://www.tencentcloud.com/document/product/1098/40616).

### What are clusters and instances in TDSQL-C for MySQL?
A TDSQL-C for MySQL cluster adopts the multi-node architecture with one read-write instance and multiple read-only instances. A single cluster supports cross-AZ management and billing.
- A cluster has its ID and name. It consists of multiple instances: one read-write instance and one or multiple read-only instances.
- An instance has its ID and name. It can be referred to as a database server.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/V9WH150_7.png)
- A cluster is a logical concept, and its configuration and specification are based on read-write and read-only instances. Different read-only instances can have different configurations, which can be separately adjusted.
- All instances in a cluster share the same storage space, which doesn't need to be purchased in advance for serverless and pay-as-you-go clusters.

### What programming languages are supported in TDSQL-C for MySQL?
TDSQL-C for MySQL supports all languages supported by native MySQL, such as Java, Python, PHP, Go, C, C++, .NET, and Node.js. For more information, see [MySQL Connectors](https://www.mysql.com/cn/products/connector/?spm=a2c4g.11186623.0.0.58e25c27mKFTJq).

### Is TDSQL-C for MySQL a distributed database?
TDSQL-C for MySQL is a distributed storage cluster implemented with the three-replica strong consistency algorithm at the storage layer. The computing engine consists of 1–16 compute nodes distributed on different servers, and the storage space can reach petabyte level, with up to 88 CPU cores and 710 GB memory supported. The storage space and computing specification can be scaled dynamically online without affecting normal business operations.

### What are the use limits of TDSQL-C for MySQL?
TDSQL-C for MySQL imposes certain use limits on naming and operations to ensure the stable and secure operation of your cluster. For more information, see [Use Limits](https://www.tencentcloud.com/document/product/1098/46425).

### Are self-built replica instances supported? Are there any recommended implementation methods?
Yes. After the binlog is enabled, you can sync a TDSQL-C for MySQL database to other MySQL databases to form a source-replica architecture. Tencent Cloud offers and recommends Data Transmission Service (DTS) for data sync and subscription. For more information on how to use DTS, see:
- [Sync from TDSQL-C for MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/47345)
- [Creating MySQL or TDSQL for MySQL Data Subscription](https://intl.cloud.tencent.com/document/product/571/47354)

Between May 17 and December 31, 2022, DTS allowed you to create pay-as-you-go tasks of migration and sync to TDSQL-C for MySQL free of charge.
