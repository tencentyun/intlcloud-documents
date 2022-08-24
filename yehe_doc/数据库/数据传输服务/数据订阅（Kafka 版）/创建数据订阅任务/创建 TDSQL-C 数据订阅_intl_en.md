This document describes how to create a data subscription task in DTS for TDSQL-C for MySQL.

## Prerequisites
- You have created a [TDSQL-C for MySQL](https://intl.cloud.tencent.com/document/product/1098/40626) instance, and the database version meets the requirements. For more information, see [Databases Supported by Data Subscription](https://intl.cloud.tencent.com/document/product/571/42663).
- You have enabled the binlog in the source instance.
- You have created a subscription account in the source instance and granted it the following permissions: REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, and SELECT for all objects.
Below is the specific authorization syntax:
```
create user 'account' IDENTIFIED BY 'password';
grant SELECT, REPLICATION CLIENT,REPLICATION SLAVE,PROCESS on *.* to 'account'@'%';
flush privileges;
```

## Restrictions
- Currently, the subscribed message content is retained for 1 day by default. Once expired, the data will be cleared. Therefore, you need to consume the data promptly.
- The region where the data is consumed should be the same as that of the subscribed database.
- Geometry data types are not supported currently. 

## Subscribable SQL Operations
| Operation Type | Supported SQL Operations |
| ------ | --------------------------- |
| DML | INSERT, UPDATE, and DELETE |
| DDL | CREATE DATABASE, DROP DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, and RENAME TABLE |

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the **Create Subscription** page, select the corresponding configuration and click **Buy Now**.
 - Billing Mode: Monthly subscription and pay-as-you-go billing are supported.
 - Region: The region must be the same as that of the database instance to be subscribed to.
 - Database: Select the database type.
 - Version: Select **Kafka Edition**. You can directly consume data on a Kafka client.
 - Subscription Name: Edit the name of the current data subscription instance.
3. After successful purchase, return to the data subscription list. You need to click **Configure Subscription** in the **Operation** column to configure the newly purchased subscription before you can use it.
![](https://qcloudimg.tencent-cloud.cn/raw/8623becce21e9354eeb6d4a03da4c9a7.png)
4. On the **Subscription Configuration** page, select the appropriate configuration items and click **Next**.
 - Instance: Select a data instance. Currently, read-only and disaster recovery instances do not support data subscription.
 - Database Account: Add the account and password of the instance to be subscribed to. The account must have the permissions required by the subscription task, including REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, and SELECT of all objects.
 - Number of Kafka Partitions: Set the number of Kafka partitions. Increasing the number can improve the speed of data write and consumption. A single partition can guarantee the order of messages, while multiple partitions cannot. If you have strict requirements for the order of messages during consumption, set this value to 1.
![](https://qcloudimg.tencent-cloud.cn/raw/216614929a8760cf248619c3f7e831ce.png)
5. On the **Subscription Type and Object** page, select a subscription type and click **Save**.
 - Subscription Type: Options include **Data Update**, **Structure Update**, and **Full**.
    - Data Update: Data updates of the selected objects are subscribed to, including INSERT, UPDATE, and DELETE operations.
    - Structure Update: Creation, modification, and deletion of the structures of all objects in the instance are subscribed to.
    - Full: Data and structure updates of all objects in the instance are subscribed to.
 - Kafka Partitioning Strategy: Select **By Table Name** or **By Table Name + Primary Key**.
 - Custom Partitioning Strategy: Customize partitions as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/cb293149e9a6dd0ae62e0e9aba996042.png)
6. On the **Pre-verification** page, a pre-verification task will run for 2–3 minutes. After the pre-verification is passed, click **Start** to complete data subscription task configuration.
>?If the verification fails, fix the problem as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification again.
>
![](https://main.qcloudimg.com/raw/c47a857b65b6d3244b985e01492aff9f.png)
7. After you click **Start**, the subscription task will be initialized, which will take 3–4 minutes. After successful initialization, the task will enter the **Running** status.
8. [Add a consumer group](https://intl.cloud.tencent.com/document/product/571/39534). Data subscription (Kafka Edition) allows you to create multiple consumer groups for multi-point consumption. The consumption depends on the consumer groups of Kafka; therefore, you must create a consumer group first before data can be consumed. 
9. After the subscription instance enters the **Running** status, you can start consuming data. For consumption in Kafka, you need to verify the password. For specific examples, see [Data Consumption Demo](https://intl.cloud.tencent.com/document/product/571/39538). We provide demo code in multiple programming languages and descriptions of main consumption processes and key data structures.
