DTS provides a binlog-based incremental data subscription feature that allows you to subscribe to incrementally updated data in TencentDB in just a few steps.

Data subscription Kafka edition supports direct consumption of data through the Kafka client. With the data subscription feature, you can easily implement incremental data subscriptions of the source database, which is convenient for you to build data synchronization between TencentDB and heterogeneous systems, such as cache update, ETL (data warehouse technology) real-time synchronization, business async decoupling, etc.
>?To use the data subscription Kafka edition, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
>
## Prerequisites
- The TencentDB for MySQL or TencentDB for MariaDB is ready to be subscribed. The synchronization versions supported by TencentDB for MySQL include MySQL 5.6 and MySQL 5.7. And the synchronization versions supported by TencentDB for MariaDB include MariaDB 10.0.10, MariaDB 10.1.9, and Percona 5.7.17.
- binlog has been enabled in instance of the source instance.
- A subscription account with the permission of REPLICATION CLIENT, REPLICATION SLAVE, PROCESS and SELECT permission for all objects has been created in the source instance.

## SQL for Subscription
| Type | Data Changes | Structure Changes | Data + Structure Changes |
| ------ | --------------------------- | ----------------------------------------------------------- | ------------- |
| Full instance | DML: INSERT, UPDATE, DELETE | DDL: CREATE DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE | DML + DDL |
| Database | DML: INSERT, UPDATE, DELETE | DDL: CREATE TABLE, ALTER TABLE， DROP TABLE | DML + DDL |
| Table | DML: INSERT, UPDATE, DELETE | ALTER TABLE, DROP TABLE | DML + DDL |

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the pop-up page, select the corresponding configurations and click **Buy Now**.
 - Billing Mode: pay-as-you-go
 - Region: the region needs to be the same as the region of the database instance to be subscribed.
 - Database: MySQL, Percona, and MariaDB are supported now. Please select the database type as needed.
 - Version: select **Kafka Edition**, which means to directly consume through Kafka client.
 - Subscription Name: set the name of the current data subscription instance.
3. After the purchase is successful, return to the data subscription list, click **Configure Subscription** in the “Operation" column to configure the subscription you just purchased, and you can use it after the configuration is completed.
4. In the **Configure data subscription** page, set the corresponding configuration and click **Next**.
 - Instance: select the corresponding database instance. TencentDB for MySQL currently supports the primary instance of MySQL 5.6 and MySQL 5.7 in high-availability editions. Read-only instances and disaster recovery instances do not support data subscription.
 - Database Account: add the account and password of the subscription instance. The account has the permissions required for the subscription task, including REPLICATION CLIENT, REPLICATION SLAVE, PROCESS, and SELECT permissions for all objects. Note that according to the principle of least privilege, you grant only the permissions required. Any additional unnecessary permissions should not be granted, otherwise the verification will fail.
5. In the **Subscription Type and Object** page, select the subscription type and click **Save**.
The subscription type includes data update, structure update and all instances. After selecting the subscription type, you need to select the data objects to be subscribed, including databases and tables.
  - Data Update: the data update of the subscription object includes INSERT, UPDATE, and DELETE operations.
  - Structure Update: includes the structure creation, modification, and deletion of all objects in the subscribed instance.
  - All: includes the data updates and structure updates for all objects of the subscribed instance.
6. In the **Pre-verification** page, the pre-verification task will run 2-3 minutes. After the pre-verification is passed, click **Start** to complete the data subscription task configuration.
>?If the verification fails, please fix it in the instance to be subscribed according to the failure prompt and perform verification again.
>
7. Click **Start**, and the subscription task will run 3-4 minutes for initialization. After the initialization is successful, it will enter the "running" state.

## Subsequent Operations
Data subscription Kafka Edition allows users to create multiple consumer groups for multi-point consumption. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
