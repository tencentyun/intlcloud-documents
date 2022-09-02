## Feature Overview
Data subscription refers to the process where DTS gets the data change information of a key business in the database, converts it into message objects, and pushes them to Kafka for the downstream businesses to subscribe to, get, and consume. DTS allows you to directly consume data through a Kafka client, so you can build data sync features between TencentDB databases and heterogeneous systems, such as cache update, real-time ETL (data warehousing technology) sync, and async business decoupling.

## How It Works
The following takes MySQL as an example to describe how data subscription pulls the incremental binlog from the source database in real time, parses the incremental data into Kafka messages, and then stores them on the Kafka server. You can consume the data through a Kafka client. As an open-source messaging middleware, Kafka supports multi-channel data consumption and SDKs for multiple programming languages to reduce your use costs.
![](https://qcloudimg.tencent-cloud.cn/raw/7d63b2f34aa9ea1b313e703e5881ccf2.jpg)

## Typical Use Cases
#### Data archiving
By using the data subscription feature of DTS, you can push the updated incremental data in TencentDB to an archive database or data warehouse as a stream in real time.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0c7f8ecfef25e793aa410660548fd1c3.jpg" style="zoom:90%;" />

## Restrictions
- Currently, the subscribed message content is retained for 1 day by default. Once expired, the data will be cleared. Therefore, you need to consume the data promptly.
- The region where the data is consumed should be the same as that of the subscribed database.
- Data subscription to MySQL, MariaDB, and TDSQL for MySQL does not support geometry data types. 

## Supported Subscription Types
DTS allows you to subscribe to databases and tables. Specifically, the following three subscription types are supported:
- Data update: Subscription to DML operations.
- Structure update: Subscription to DDL operations.
- Full: Subscription to the DML and DDL operations of all tables.


## Supported Advanced Features

| **Feature**          | **Description**                        | **Documentation**                           |
| -------------------------- | ---------------------------------- | -------------------- |
| SDKs for various programming languages          | DTS uses the Kafka protocol and supports Kafka client SDKs for multiple programming languages.     | -                    |
| Metric monitoring and default alarm policy          | <li>Data subscription metrics can be monitored. <li>Default configuration is supported for data subscription event monitoring to automatically notify you of abnormal events. | [Supported Events and Metrics](https://intl.cloud.tencent.com/document/product/571/42611)                   |
| Multi-Channel data consumption         | DTS allows creating multiple data channels for a single database, which can be consumed concurrently through a consumer group. | -                    |
| Partitioned consumption               | DTS supports partitioned storage of data in a single topic for concurrent consumption of data in multiple partitions, improving the consumption efficiency. | -                    |
| Custom routing policy | DTS supports routing data fields to Kafka partitions according to custom rules. | - |
| Consumption offset change | DTS supports modifying the consumption offset. | [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535) |


