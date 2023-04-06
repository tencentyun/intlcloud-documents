### Does TencentDB for SQL Server support publish/subscribe?
The publish/subscribe feature is available only when both the publishing and subscribing instances are TencentDB for SQL Server instances. In addition, this feature is supported only for TencentDB for SQL Server two-node (formerly High Availability/Cluster Edition) but not single-node (formerly Basic Edition) instances.

### Does a TencentDB for SQL Server single-node (formerly Basic Edition) instance support publish/subscribe?
No.

### How do I implement publish/subscribe between a self-built SQL Server database in my local IDC and a TencentDB for SQL Server instance?
The publish/subscribe feature is not supported between a self-built SQL Server database in a local IDC and a TencentDB for SQL Server instance. It is available only when both the publishing and subscribing instances are TencentDB for SQL Server instances.

### What are the use cases of the publish/subscribe feature of TencentDB for SQL Server?
TencentDB for SQL Server supports the native publish/subscribe-based replication feature of Microsoft SQL Server. You can create, change, and delete publishing and subscribing servers in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) for data replication and sync in your business. For more information, see [Publish/Subscribe Overview](https://www.tencentcloud.com/document/product/238/48063).

### What are the prerequisites for using the publish/subscribe feature of TencentDB for SQL Server?
- This feature is available only when both the publishing and subscribing instances are TencentDB for SQL Server instances.
- This feature is supported only for TencentDB for SQL Server two-node (formerly High Availability/Cluster Edition) but not single-node (formerly Basic Edition) instances.
- The publishing and subscribing instances must be on the same edition, such as 2017 Enterprise Edition.
- The publishing and subscribing instances must be in the same region (but they can be in different AZs). For example, if the publishing instance is in Beijing Zone 5, the subscribing instance can be in Beijing Zone 7.
- A read-only instance cannot be used as a publishing or subscribing server.
- If the publishing and subscribing instances have a database with the same name, the database cannot be subscribed to.
- Data tables without a primary key cannot be subscribed to. You can use the following code to check whether the database to be published contains this type of tables:
```
use dbname
select name from sys.sysobjects where xtype='U' and id not in(select parent_obj from sys.sysobjects where xtype='PK')
```
- After a publish/subscribe linkage is created, if a database in the linkage is deleted, the linkage will also be deleted.
- If either the publishing or subscribing instance is terminated, the publish/subscribe linkage will also be deleted.
- You can configure up to 80 databases to be published/subscribed to in each publish/subscribe task.

[](id:FBDYCZ)
### How do I create a publish/subscribe task in TencentDB for SQL Server?
Log in to the [SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list to enter the instance management page, select the **Publish/Subscribe** tab, and click **Create** to create a publish/subscribe task. For more information, see [Managing Publish/Subscribe](https://www.tencentcloud.com/document/product/238/48062).

### How do I delete the publish/subscribe relationship between two TencentDB for SQL Server instances?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list to enter the instance management page, select the **Publish/Subscribe** tab, select the task to be deleted, and click **Delete**. You can also batch delete multiple tasks. For more information, see [Managing Publish/Subscribe](https://www.tencentcloud.com/document/product/238/48062).

