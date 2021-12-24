DTS provides a binlog-based incremental data subscription feature that allows you to subscribe to incrementally updated data in TencentDB in just a few steps:

Data subscription (Kafka Edition) allows you to directly consume data through a Kafka client. With this feature, you can easily subscribe to the incremental data changes in the source database and build data sync features between TencentDB databases and heterogeneous systems, such as cache update, real-time ETL (data warehousing technology) sync, and async business decoupling.

## Prerequisites
- You have prepared a TencentDB for MySQL or MariaDB or TDSQL for MySQL instance to be subscribed to, and the database version meets the requirements. For more information, see [Databases Supported by Data Subscription](https://intl.cloud.tencent.com/document/product/571/42663).
- You have enabled the binlog in the source database.
- You have created a subscription account in the source database and granted it the following permissions: REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, and SELECT for all objects.
Below is the specific authorization syntax:
```
create user 'subscription account' IDENTIFIED BY 'account password';
grant SELECT, REPLICATION CLIENT,REPLICATION SLAVE,PROCESS on *.* to 'subscription account'@'%';
flush privileges;
```

## Restrictions
- Currently, the subscribed message content is retained for 1 day by default. Once expired, the data will be cleared. Therefore, you need to consume the data promptly.
- The region where the data is consumed should be the same as that of the subscribed database.
- Data subscription to MySQL, MariaDB, and TDSQL for MySQL does not support geometry data types. 

## Overview of Data Subscription to TDSQL for MySQL

- If the data subscription source is TDSQL for MySQL, it is not supported to directly run the authorization statement. Instead, you need to go to the [TDSQL console](https://console.cloud.tencent.com/tdsqld), click the target instance name, and enter the account management page to authorize.
The permissions required by the subscription account are those listed in the above authorization statement. To perform `__tencentdb__` authorization to the subscription account, select **Object-Level Privilege** in the **Modify Permissions** pop-up window and then select all permissions.
- If the data subscription source is TDSQL for MySQL, you cannot create two-level partitioned tables in the instance. If such a table already exists in the instance before the subscription task is initiated, task verification will fail. If you create such a table in the instance during the subscription task, the task will report an error and pause.
For more information on two-level partitioning, see [Overview](https://intl.cloud.tencent.com/document/product/1042/38142).
- If the data subscription source is TDSQL for MySQL, DDL operations in each shard will be subscribed to and delivered to Kafka. Therefore, there will be duplicate DDL statements for DDL operations in a sharded table; for example, instance A has three shards and subscribes to a sharded table A, then three DDL statements for the same DDL operation will be delivered to table A.
- The header of each message in Kafka carries the shard information in `key/value` form. Here, the key is `ShardId`, and the value is the SQL passthrough ID. You can identify the shard where the message comes from based on the SQL passthrough ID.

## Subscribable SQL Operations
|  Type      | Data Change                    | Structure Change                                                    | Data + Structure Change |
| ------ | --------------------------- | ----------------------------------------------------------- | ------------- |
| Full instance | DML: INSERT, UPDATE, and DELETE | DDL: CREATE DATABASE, CREATE TABLE, ALTER TABLE, and DROP TABLE | DML + DDL       |
| Database | DML: INSERT, UPDATE, and DELETE | DDL: CREATE TABLE, ALTER TABLE, and DROP TABLE    | DML + DDL       |
| Table | DML: INSERT, UPDATE, and DELETE | DDL: ALTER TABLE and DROP TABLE             | DML + DDL       |

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the **Create Subscription** page, select the corresponding configuration and click **Buy Now**.
 - Billing Mode: monthly subscription and pay-as-you-go billing are supported.
 - Region: the region must be the same as that of the database instance to be subscribed to.
 - Database: currently, TencentDB for MySQL, Percona, and MariaDB are supported. Select your actual database type.
 - Version: select **Kafka Edition**. You can directly consume data on a Kafka client.
 - Subscription Name: edit the name of the current data subscription instance.
3. After successful purchase, return to the data subscription list. You need to click **Configure Subscription** in the **Operation** column to configure the newly purchased subscription before you can use it.
![](https://qcloudimg.tencent-cloud.cn/raw/06b74af952a12f7e60a7df707c957d0c.png)
4. On the **Subscription Configuration** page, select the appropriate configuration items and click **Next**.
 - Instance: select a data instance. Currently, read-only and disaster recovery instances do not support data subscription.
 - Database Account: add the account and password of the instance to be subscribed to. The account must have the permissions required by the subscription task, including REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, and SELECT of all objects.
![](https://qcloudimg.tencent-cloud.cn/raw/c1bbe02a47a94a2955a30e0c53bb61cb.png)
5. On the **Subscription Type and Object** page, select a subscription type and click **Save**.
 - Subscription Type: options include **Data Update**, **Structure Update**, and **Full**.
    - Data Update: data updates of the selected objects are subscribed to, including INSERT, UPDATE, and DELETE operations.
    - Structure Update: creation, modification, and deletion of the structures of all objects in the instance are subscribed to.
    - Full: data and structure updates of all objects in the instance are subscribed to.
 - Kafka Partitioning Strategy: select **By Table Name** or **By Table Name + Primary Key**.
 - Custom Partitioning Strategy: customize partitions as needed.
>?Subscription objects exclude the system tables and databases named `test`, as DTS does not support subscription to system tables, and `test` databases are recognized as test data by DTS.
>
![](https://qcloudimg.tencent-cloud.cn/raw/2965c8182bd59e73e4a54dbfc7b5e1ca.png)
6. On the **Pre-verification** page, a pre-verification task will run for 2–3 minutes. After the pre-verification is passed, click **Start** to complete data subscription task configuration.
>?If verification fails, modify the task in the instance to be subscribed to as prompted and initiate the verification again.
>
![](https://qcloudimg.tencent-cloud.cn/raw/43d8d91b937eccd3d65312ed9f4ed0d2.png)
7. After you click **Start**, the subscription task will be initialized, which will take 3–4 minutes. After successful initialization, the task will enter the **Running** status.
8. [Add a consumer group](https://intl.cloud.tencent.com/document/product/571/39534). Data subscription (Kafka Edition) allows you to create multiple consumer groups for multi-point consumption. The consumption depends on the consumer groups of Kafka; therefore, you must create a consumer group first before data can be consumed. 
9. After the subscription instance enters the **Running** status, you can start consuming data. For consumption in Kafka, you need to verify the password. For specific examples, see [Data Consumption Demo](https://intl.cloud.tencent.com/document/product/571/39538). We provide demo code in multiple programming languages and descriptions of main consumption processes and key data structures.
