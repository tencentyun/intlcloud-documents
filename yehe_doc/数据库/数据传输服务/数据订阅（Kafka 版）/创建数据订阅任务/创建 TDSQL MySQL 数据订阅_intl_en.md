This document describes how to create a data subscription task in DTS for TDSQL for MySQL.

## Prerequisites
- You have prepared a TencentDB instance to be subscribed to, and the database version meets the requirements. For more information, see [Databases Supported by Data Subscription](https://intl.cloud.tencent.com/document/product/571/42663).
- You have enabled the binlog in the source instance.
- You have created a subscription account in the source instance and granted it the following permissions: REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, and SELECT for all objects.
Authorization statements are as follows:
```
create user 'migration account' IDENTIFIED BY 'account password';
grant SELECT, REPLICATION CLIENT,REPLICATION SLAVE,PROCESS on *.* to 'migration account'@'%';
flush privileges;
```

## Restrictions
- Currently, the subscribed message content is retained for 1 day by default. Once expired, the data will be cleared. Therefore, you need to consume the data promptly.
- The region where the data is consumed should be the same as that of the subscribed instance.
- Geometry data types are not supported currently. 
- If the data subscription source is TDSQL for MySQL, it is not supported to directly run the authorization statement. Instead, you need to go to the [TDSQL console](https://console.cloud.tencent.com/tdsqld), click the target instance ID, and enter the account management page to authorize.
  The permissions required by the subscription account are those listed in the above authorization statement. To perform `__tencentdb__` authorization to the subscription account, select **Object-Level Privilege** in the **Modify Permissions** pop-up window and then select all permissions.
- If the data subscription source is TDSQL for MySQL, two-level partitioned tables as described in [Subpartitioning](https://intl.cloud.tencent.com/document/product/1042/33361) cannot be subscribed to.
   - If a two-level partitioned table is created in the source database before the subscription task is started, the verification task will fail.
   - If a two-level partitioned table is created in the source database when the subscription task is running, the subscribed data in the two-level partitioned table will be the data in the child table (if the selected subscription object is the entire database or entire instance, a two-level partitioned table created in the source database after the subscription task is started will also be subscribed to; in this way, data in the two-level partitioned table will also be included in the subscription). As the underlying layer of the two-level partitioned table is implemented by child tables, we recommend you not create two-level partitioned tables during the subscription task execution; otherwise, differences in the subscribed data will occur. 
For example, if the source database table "test_a" is a two-level partitioned table, then the table name of the DML that DTS subscribes to this table is "test_a_tdsql_subp0/test_a_tdsql_subp1".
- The delivery semantics of subscription to Kafka messages in DTS is to deliver a message at least once; therefore, the consumed data may be duplicated in special cases. For example, if the subscription task is restarted, the source binlog will be pulled before the interruption offset after the restart, resulting in repeated delivery of messages. Operations in the console such as modifying subscribed objects and restoring abnormal tasks may cause duplicate messages. If your business is sensitive to duplicate data, you need to add deduplication logic based on the business data in the consumption demo.

   
## Notes
- If the data subscription source is TDSQL for MySQL, DDL operations in each shard will be subscribed to and delivered to Kafka. Therefore, there will be duplicate DDL statements for DDL operations in a sharded table; for example, instance A has three shards and subscribes to a sharded table A, then three DDL statements for the same DDL operation will be delivered to table A.

- The header of each message in Kafka carries the shard information in `key/value` form. Here, the key is `ShardId`, and the value is the SQL passthrough ID. You can identify the shard where the message comes from based on the SQL passthrough ID, which can be viewed in **[TDSQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) > Instance List > Shard Management**.
![](https://qcloudimg.tencent-cloud.cn/raw/cb5c7823105f2cd6837c2cdaf1cd29b9.png)

## SQL operations for subscription
| Operation Type | Supported SQL Operations |
| ------ | --------------------------- |
| DML | INSERT, UPDATE, and DELETE |
| DDL | CREATE DATABASE, DROP DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, and RENAME TABLE |

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the **Create Subscription** page, select appropriate configuration items and click **Buy Now**.
 - Billing Mode: Monthly subscription and pay-as-you-go billing are supported.
 - Region: The region must be the same as that of the database instance to be subscribed to.
 - Database: Select your actual database type.
 - Version: Select **Kafka Edition**. You can directly consume data on a Kafka client.
 - Subscription Name: Edit the name of the current data subscription instance.
3. After successful purchase, return to the data subscription list. You need to click **Configure Subscription** in the **Operation** column to configure the newly purchased subscription before you can use it.
4. On the **Subscription Configuration** page, select the appropriate configuration items and click **Next**.
 - Instance: Select a database instance. Currently, read-only and disaster recovery instances do not support data subscription.
 - Database Account: Add the account and password of the instance to be subscribed to. The account must have the permissions required by the subscription task, including REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, and SELECT of all objects.
 - Number of Kafka Partitions: Set the number of Kafka partitions. Increasing the number can improve the speed of data write and consumption. A single partition can guarantee the order of messages, while multiple partitions cannot. If you have strict requirements for the order of messages during consumption, set this value to 1.
5. On the **Subscription Type and Object** page, select a subscription type and click **Save**.
Subscription Type: Options include **Data Update**, **Structure Update**, and **Full**.
   - Data Update: Data updates of the selected objects are subscribed to, including INSERT, UPDATE, and DELETE operations.
   - Structure Update: Creation, modification, and deletion of the structures of all objects in the instance are subscribed to.
   - Full: Data and structure updates of all objects in the instance are subscribed to.
6. On the **Pre-verification** page, a pre-verification task will run for 2–3 minutes. After the pre-verification is passed, click **Start** to complete data subscription task configuration.
>?If the verification fails, fix the problem as instructed in [Check Item Overview](https://intl.cloud.tencent.com/document/product/571/42551) and initiate the verification again.
>
7. After you click **Start**, the subscription task will be initialized, which will take 3–4 minutes. After successful initialization, the task will enter the **Running** status.
8. [Add a consumer group](https://intl.cloud.tencent.com/document/product/571/39534). Data subscription (Kafka Edition) allows you to create multiple consumer groups for multi-point consumption. The consumption depends on the consumer groups of Kafka; therefore, you must create a consumer group first before data can be consumed. 
9. After the subscription instance enters the **Running** status, you can start consuming data. For consumption in Kafka, you need to verify the password. We provide demo code in multiple programming languages and descriptions of main consumption processes and key data structures.

