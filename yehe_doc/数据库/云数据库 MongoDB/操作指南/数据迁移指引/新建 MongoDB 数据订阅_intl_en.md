This document describes how to create a data subscription task in DTS for TencentDB for MongoDB.

## Version description
- Currently, data subscription is supported only for TencentDB for MongoDB 3.6, 4.0, 4.2, and 4.4.
- TencentDB for MongoDB 3.6 only supports collection-level subscription.

## Prerequisites
- You have prepared a TencentDB instance to be subscribed to, and the database version meets the requirements. For more information, see [Databases Supported by Data Subscription](https://intl.cloud.tencent.com/document/product/571/42663).
- We recommend you create a read-only account in the source instance by referring to the following syntax. You can also do this in the [TencentDB for MongoDB console](https://intl.cloud.tencent.com/document/product/240/44183).
```
# Create an instance-level read-only account
use admin
db.createUser({
  user: "username",  
  pwd: "password",  
  roles:[    
         {role: "readAnyDatabase",db: "admin"}  
        ]
})

# Create a database-specific read-only account
use admin
db.createUser({
  user: "username",  
  pwd: "password",  
  roles:[    
         {role: "read",db: "Name of the specified database"}
        ]
})
```

## Notes
- Currently, the subscribed message content is retained for 1 day by default. Once expired, the data will be cleared. Therefore, you need to consume the data promptly.
- The region where the data is consumed should be the same as that of the subscribed instance. 
- The Kafka built in DTS has a certain upper limit for processing individual messages. When a single row of data in the source database exceeds 10 MB, this row may be discarded in the consumer.
- After the database or collection specified for the selected subscription object is deleted from the source database, the subscription data (change stream) of the database or collection will be invalidated. Even if the database or collection is rebuilt in the source database, the subscription data cannot be resubscribed. In this case, you need to reset the subscription task and select the subscription object again.

## SQL operations for subscription

| Operation Type | Supported SQL Operations                                              |
| -------- | ------------------------------------------------------------ |
| DML      | INSERT, UPDATE, and DELETE                                       |
| DDL      | INDEX: createIndexes, createIndex, dropIndex, dropIndexes; COLLECTION: createCollection, drop, collMod, renameCollection; DATABASE: dropDatabase, copyDatabase |

## Subscription configuration
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the **Create Subscription** page, select appropriate configuration items and click **Buy Now**.
 - Billing Mode: **Pay-as-you-go** is supported.
 - Region: The region must be the same as that of the database instance to be subscribed to.
 - Database: Select **MongoDB**.
 - Version: Select **Kafka Edition**. You can directly consume data on a Kafka client.
 - Subscription Name: Edit the name of the current data subscription instance.
 - Quantity: You can purchase up to 10 tasks at a time.
3. After successful purchase, return to the data subscription list, select the purchased task, and click **Configure Subscription** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WzBL873_34-en.png)
4. On the subscription configuration page, select the source database information, click **Test Connectivity**, and click **Next**.
 - Access Type: Currently, only **Database** is supported.
 - Instance Name: Select the TencentDB instance ID.
 - Database Account/Password: Add the account and password of the instance to be subscribed to. The account has the read-only permission.
 - Number of Kafka Partitions: Set the number of Kafka partitions. Increasing the number can improve the speed of data write and consumption. A single partition can guarantee the order of messages, while multiple partitions cannot. If you have strict requirements for the order of messages during consumption, set this value to 1.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/bw9s273_35-en.png"  style="zoom:40%;">
5. On the **Subscription Type and Object** page, select the subscription parameters and click **Save**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Data Subscription Type</td>
<td>It is change stream by default and cannot be modified.</td></tr>
<tr>
<td>Subscription Object Level</td>
<td>Select **Full instance**, **Database**, or **Collection**. <ul><li>Full instance: Subscribes to the full instance data. </li><li>Database: Subscribes to data at the database level. If this option is selected, only one database can be selected in the **Task Configuration** below. </li><li>Collection: Subscribes to data at the collection level. If this option is selected, only one collection can be selected in the **Task Configuration** below.</li></ul></td></tr>
<tr>
<td>Task Configuration</td>
<td>Select the database or collection to be subscribed to. You can select only one database or collection.</td></tr>
<tr>
<td>Output Aggregation Settings</td>
<td>If this option is selected, the aggregation pipeline will be executed based on the order configured on the page. For more information, see <a href="https://www.mongodb.com/docs/manual/changeStreams/#modify-change-stream-output">Modify Change Stream Output</a>.</td></tr>
<tr>
<td>Kafka Partitioning Policy</td>
<td><ul><li>By Collection Name: Partitions the subscribed data from the source database by collection name. With this policy, data with the same collection name is written to the same Kafka partition. </li><li>Custom Partitioning Policy: Database and collection names of the subscribed data are matched through a regex first. Then, matched data is partitioned by collection name or collection name + `objectid`.</li></ul></td></tr>
</tbody></table>
6. On the **Pre-verification** page, a pre-verification task will run for 2–3 minutes. After the pre-verification is passed, click **Start** to complete data subscription task configuration.
>?If the verification fails, fix the problem as instructed in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552) and initiate the verification again.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WQTU262_36-en.png)
7. The subscription task will be initialized, which will take 3–4 minutes. After successful initialization, the task will enter the **Running** status.

## Subsequent operations
1. [Add a consumer group](https://intl.cloud.tencent.com/document/product/571/39534).
The consumption in data subscription (Kafka Edition) depends on the consumer groups of Kafka; therefore, you must create a consumer group first before data can be consumed. Data subscription (Kafka Edition) allows you to create multiple consumer groups for multi-point consumption.
2. [Consume the subscripted data](https://www.tencentcloud.com/document/product/571/48488).
After the subscription task enters the **Running** status, you can start consuming data. For consumption in Kafka, you need to verify the password. For specific examples, see the demo in [Consuming Subscribed Data with Kafka Client (ProtoBuf)](https://www.tencentcloud.com/document/product/571/48488). We provide demo code in multiple programming languages and descriptions of main consumption processes and key data structures.

