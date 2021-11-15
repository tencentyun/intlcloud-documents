## Overview
Data Transmission Service (DTS) supports the migration of MySQL, MariaDB, PostgreSQL, Redis, MongoDB and other relational databases and NoSQL database. It can help you migrate your databases without interrupting your business and build a high-availability database architecture for disaster recovery through real-time sync channels. And through data subscription, DTS can meet the requirements of business data mining, business async decoupling and other scenarios.


## Product Features
- **Data migration**
Database migration is available for different database types, under different environments. Source databases that are supported for migration include self-built databases in a public network with public IP, self-built databases with access to Tencent Cloud via VPN, direct connection or other network environments, and self-built databases in CVM. Target database is TencentDB instance. Users can check the statuses of all migration tasks and carry out multi-task batch operation.
The data migration feature of DTS is the best choice for you to migrate data onto cloud. You only need to configure a few steps for data migration, and then you can complete a series of tedious processes for migrating your local data onto the cloud. Meanwhile, the migration process does not prevent your source database from providing external service, thereby minimizing the effect on your business caused by the cloud migration task.
- **Data Sync**
The data synchronization feature of DTS implements real-time data synchronization between two TencentDB instances, which is applicable to scenarios such as remote disaster recovery. Currently, data synchronization is only supported for TencentDB for MySQL instances.
- **Data subscription**
DTS allows you to acquire real-time incremental update data of a cloud database and also to freely consume incremental data based on your business needs to achieve various business scenarios, such as implementation of cache update policy, async businesses decoupling, real-time synchronization of heterogeneous data sources and real-time synchronization of data containing complicated ETL. You can also dynamically add or delete the subscription object, view subscription data online and modify the consumption time point.
Data subscription currently supports [Data Subscription (Legacy)](https://intl.cloud.tencent.com/document/product/571/8774) and [Data Subscription Kafka Edition](https://intl.cloud.tencent.com/document/product/571/39531).

