With the automatic read/write separation feature of TDSQL-C for MySQL, a connection will be established between TDSQL-C for MySQL and the application to parse every incoming SQL statement. If it is a statement such as `CREATE`, `ALTER`, `DROP`, or `RENAME`, the statement is directly sent to the read-write instance. If it is a non-transactional read (`SELECT`) statement, the statement is sent to a read-only instance, thereby implementing read/write separation. However, when the database load is high, for example, when a large batch of data is inserted, the delay will be long, resulting in a failure to read the latest data from the read-only instance.

When there is data update in the read-write instance, the related update will be applied to the read-only instance. The delay time of data sync is subject to the write workload. TDSQL-C for MySQL provides different consistency levels to ensure data consistency requirements when the business accesses the database.

The consistency levels are as follows:
- Eventual consistency
- Session consistency
- Global consistency

## Eventual Consistency
**Feature overview**
The database proxy of TDSQL-C for MySQL implements the automatic read/write separation feature. In the automatic read/write separation scenario, the eventual consistency is provided by default to ensure that the read-only instance can read the newly written data and eventually obtain all of them. However, the database proxy does not ensure that the updated data is immediately available. Delays in source/replica replication of the updated data will cause inconsistent results queried from different nodes.

**Use cases**
If you need to reduce the pressure on the read-write instance and route as many read requests as possible to the read-only instance, you can choose eventual consistency in scenarios that do not require high consistency.


## Session Consistency
**Feature overview**
Some scenarios require high consistency, but eventual consistency causes incosistent query results. Usually, the business needs to be split, that is, requests with high consistency requirements are directly sent to the read-write instance while requests that can accept eventual consistency are sent to the read-only instance through read/write separation. However, this will increase the pressure on the read-write instance, reduce the effect of read/write separation, and increase the burden of application development.

To solve the above problems, TDSQL-C for MySQL provides session consistency to guarantee monotonic reads within the same session, and data that has been updated before the read requests are executed can be queried.

While the middle layer of the linkage of TDSQL-C for MySQL performs read/write separation, the middle layer traces log time points (that is, log sequence number, LSN for short) that have been applied by each node. When data is updated each time, TDSQL-C for MySQL records the updated time point as session LSN. When a new request arrives, TDSQL-C for MySQL compares the session LSN with the LSN of each current instance, and sends the request only to the instance whose LSN is greater than or equal to the session LSN, thereby ensuring session consistency.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/aZ6c370_15e0e63c8fdd6993a81761f4064b1de2.png)
In the above scenario, when the update is completed, replication is also synchronously performed while the result is returned to the client. When the next read request arrives, data replication between the read-write instance and the read-only instance may have been completed. In addition, most application scenarios feature more reads and less writes, so session consistency is guaranteed under this mechanism.

**Use cases**
It is suitable for scenarios with high consistency requirements. A higher consistency level of TDSQL-C for MySQL indicates greater pressure on the primary database and lower cluster performance. Session consistency is recommended because it has little impact on performance and can meet the needs of most application scenarios.

>!After session consistency is enabled, if the replication delay between the read-write instance and the read-only instance is large, and the LSN of each read node is smaller than the session LSN, SELECT requests will be sent to the read-write instance. This will increase the pressure on the read-write instance and reduce the read/write performance of the entire cluster to a certain extent.

## Global Consistency
**Feature overview**
Some scenarios have extremely high consistency requirements. In addition to logical causal dependencies within sessions, there are dependencies between sessions. For example, in scenarios where connection pools are used, requests from the same thread may be sent through different connections. For the database, these requests belong to different sessions. However, in terms of business logic, these requests have pre- and post-dependencies. In this case, session consistency cannot ensure consistency of query results. Therefore, TDSQL-C for MySQL provides global consistency to solve this problem.

**Use cases**
It is suitable for scenarios with extremely high consistency requirements. When the source-replica delay is high, global consistency may cause more requests to be routed to the read-write instance, thereby increasing the pressure on the read-write instance and prolonging the business delay. Therefore, it is recommended to choose global consistency in scenarios that feature more read requests and less write requests.

## Setting a Consistency Level
>?Before setting a consistency level, enable the read/write separation feature. You can set the session consistency level in the step of enabling read/write separation. If the feature has been enabled, but the consistency level needs to be modified, refer to the following steps.
>
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. In the cluster list, click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
3. On the cluster management page, select **Database Proxy** > **Read/Write Separation** > **Adjust Configurations*.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cvMX553_2.png)
4. In the configuration window, select a consistency level and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GadS489_3.png)

