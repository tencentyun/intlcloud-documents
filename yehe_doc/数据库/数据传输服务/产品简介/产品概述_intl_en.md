## Overview
Tencent Cloud Data Transmission Service (DTS) supports the migration of various relational databases such as MySQL, MariaDB, PostgreSQL, Redis, and MongoDB as well as NoSQL databases. It enables you to migrate your databases to Tencent Cloud with no business interruptions, create a high-availability database disaster recovery architecture through real-time sync channels, and use data subscription to meet your requirements for commercial data mining and async business decoupling.



## Features
- [**Data migration**](https://intl.cloud.tencent.com/document/product/571/13711)
The data migration feature refers to data replication between different data sources. DTS supports non-stop data migration to minimize the impact of database downtime on the business. It is applicable to diverse business scenarios, including data migration to Tencent Cloud, cross-TencentDB instance data migration, and data migration from third-party cloud databases to TencentDB.

- [**Data sync**](https://intl.cloud.tencent.com/document/product/571/42667)
  The data sync feature refers to real-time data sync between two database sources. It is suitable for cloud-local active-active, multi-site active-active, and cross-border data sync as well as real-time data warehousing.   

  Unlike data migration which is a one-time short-term task to migrate the entire database, data sync is a continuous task. After a task is created, the data will be continuously synced to keep consistency between the source and target databases.

- [**Data subscription**](https://intl.cloud.tencent.com/document/product/571/13713)
Data subscription refers to the process through which DTS gets the data change information of a key business from the database, converts it into message objects, and pushes them to Kafka for the downstream businesses to subscribe to, get, and consume. DTS allows you to directly consume data through a Kafka client, so you can build data sync features between TencentDB databases and heterogeneous systems, such as cache update, real-time ETL (data warehousing technology) sync, and async business decoupling.
