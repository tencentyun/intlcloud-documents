DTS provides a binlog-based incremental data subscription feature that allows you to subscribe to incrementally updated data in TencentDB with just a few steps.

Data Subscription Kafka Edition supports direct consumption of data through the Kafka client. With the data subscription feature, you can easily subscribe to incrementally updated data of the source database, which is convenient for you to realize data synchronization between TencentDB and heterogeneous systems, such as cache update, ETL (data warehouse technology) real-time sync, business async decoupling, etc.
>?The data subscription messages of Data Subscription Kafka Edition can be retained in the Kafka client for 1 day (24 hours) by default. Please consume these messages in time to avoid the loss of subscribed data.
>
## Prerequisites
- TencentDB for MySQL, TencentDB for MariaDB, or TDSQL for MySQL is ready to be subscribed to.
 - TencentDB for MySQL versions that support sync: MySQL 5.6 and MySQL 5.7.
 - TencentDB for MariaDB versions that support sync: MariaDB 10.0.10, MariaDB 10.1.9, and Percona 5.7.17.
 - TDSQL for MySQL versions that support sync: Percona 5.7.17.
- binlog has been enabled in the source instance.
- The database `__tencentdb__` has been created in the source database.
- A subscription account has been created in the source instance. Account permissions required include REPLICATION CLIENT, REPLICATION SLAVE, and PROCESS, as well as the SELECT permission for all objects 
Authorization statements are as follows:
```
create user ‘migration account’ IDENTIFIED BY 'account password';
grant SELECT, REPLICATION CLIENT,REPLICATION SLAVE,PROCESS on *.* to 'migration account'@'%';
grant ALL PRIVILEGES on `__tencentdb__`.* to 'migration account'@'%';
flush privileges;
```

## Data Subscription Description for TDSQL for MySQL
- If the database for data subscription is a TDSQL for MySQL instance, you cannot grant permissions with authorization statements. Therefore, you need to click the instance name on the [TDSQL console](https://console.cloud.tencent.com/tdsqld) to enter the account management page and add subscription permissions there.
Permissions required by the subscription account are mentioned in the authorization statements above. To grant the `__tencentdb__` permission for the subscription account, you can select “Object Level Privilege” in the permission modification pop-up window and select all permissions.
If the database for data subscription is a TDSQL for MySQL instance, you cannot create two-level partitioned tables on the instance. If two-level partitioned tables already exist on the instance before the subscription task is started, the verification will fail. If you create two-level partitioned tables when the subscription task is running, the task will be paused and report an error.
For more information on two-level partitioning, please see [Subpartitioning](https://intl.cloud.tencent.com/document/product/1042/33361).
For a subscription task whose database for subscription is TDSQL for MySQL, the DDL operations of each shard will be subscribed to and be published to Kafka. Therefore, DDL operations of a sharded table will lead to duplicate DDL statements. For example, if instance A has 3 shards and you subscribe to a sharded table A, you will subscribe to 3 DDL statements of table A.
- The message header of each message in Kafka contains shard information in the form of key/value. Key refers to ShardId, and value refers to SQL passthrough ID. You can know which shard a message comes from according to the SQL passthrough ID. For more information, see [Shard Management](https://console.cloud.tencent.com/tdsqld).

## SQL Operations for Subscription
| Type | Data Changes | Structure Changes | Data + Structure Changes |
| ------ | --------------------------- | ----------------------------------------------------------- | ------------- |
| Full instance | DML: INSERT, UPDATE, DELETE | DDL: CREATE DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE | DML + DDL |
| Database | DML: INSERT, UPDATE, DELETE | DDL: CREATE TABLE, ALTER TABLE， DROP TABLE | DML + DDL |
| Table | DML: INSERT, UPDATE, DELETE | ALTER TABLE, DROP TABLE | DML + DDL |

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the “Create Subscription” page, select the corresponding configurations and click **Buy Now**.
 - Billing Mode: monthly subscription and pay-as-you-go.
 - Region: select the region of the database instance to be subscribed.
 - Database: MySQL, Percona, and MariaDB are supported now. Please select the database type as needed.
 - Version: select **Kafka Edition**, which means you can directly consume through the Kafka client.
 - Subscription Name: set the name of the current data subscription instance.
3. After the purchase is successful, return to the data subscription list, click **Configure Subscription** in the “Operation" column to configure the subscription you just purchased, and you can use it after the configuration is completed.
![](https://main.qcloudimg.com/raw/d45bbff5e702281fdc57984720999e6c.png)
4. On the **Configure data subscription** page, select the corresponding configurations and click **Next**.
 - Instance: select the corresponding database instance. TencentDB for MySQL currently supports the high-availability editions of MySQL 5.6 and MySQL 5.7 primary instances. Read-only instances and disaster recovery instances do not support data subscription.
 - Database Account: add the account and password of the subscription instance. The account has the permissions required for the subscription task, including REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, as well as the SELECT permission for all objects. Note that according to the principle of least privilege, any unnecessary permissions should not be granted, otherwise the verification will fail.
![](https://main.qcloudimg.com/raw/5d4cb75fcadd6e33233781d09da10433.png)
5. On the **Subscription Type and Object** page, select the subscription type and click **Save**.
Subscription types include data update, structure update and all instances. After selecting the subscription type, you need to select the data objects to be subscribed to, including databases and tables.
  - Data Update: the data update of the subscription object, including INSERT, UPDATE, and DELETE operations.
  - Structure Update: the structure creation, modification, and deletion of all objects in the subscribed instance.
  - All: including the data updates and structure updates for all objects of the subscribed instance.
![](https://main.qcloudimg.com/raw/edf52681e7fc00588697d1d7ccf7328f.png)
6. On the **Pre-verification** page, the pre-verification task will run for 2-3 minutes. After the pre-verification is passed, click **Start** to complete the data subscription task configuration.
>?If the verification fails, please fix it in the instance to be subscribed to according to the failure prompt and perform verification again.
>
![](https://main.qcloudimg.com/raw/c47a857b65b6d3244b985e01492aff9f.png)
7. Click **Start**, and the subscription task will run for 3-4 minutes for initialization. After the initialization is successful, it will enter the "Running" status.

## Data Consumption
You can consume data after the subscribed instance enters the “Running” status. For more information on the consumption logic, see [Data Consumption Demo](https://intl.cloud.tencent.com/document/product/571/39538). We provide Demo codes in multiple languages for your reference, and also describe the main consumption processes and key data structures

## Subsequent Operation
Data Subscription Kafka Edition allows you to create multiple consumer groups for multi-point consumption. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/zh/document/product/571/39534).
