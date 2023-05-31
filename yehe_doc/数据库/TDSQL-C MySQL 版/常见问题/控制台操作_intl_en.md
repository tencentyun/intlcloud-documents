
## Version Upgrade
### How do I upgrade the version of TDSQL-C for MySQL?
- Currently, TDSQL-C for MySQL doesn't support database version upgrade, such as from MySQL 5.7 to 8.0. You can create a new instance on the target version and migrate the source data to it through DTS. For directions, see [Migrating to TDSQL-C for MySQL](https://intl.cloud.tencent.com/document/product/571/47364).
- For detailed directions on how to upgrade the kernel minor version, such as from v2.0.12 of MySQL 5.7 to v2.0.14, see [Upgrading Kernel Minor Version](https://www.tencentcloud.com/document/product/1098/44617).

### Will version upgrade affect the data?
No.
TDSQL-C for MySQL adopts quick in-place upgrade. It uses redo logs to store the data to implement super-fast upgrade. A momentary disconnection may occur in rare cases. Make sure that your business has an automatic reconnection mechanism.

### How do I view the differences between different kernel minor versions of TDSQL-C for MySQL?
TDSQL-C for MySQL releases kernel minor version updates from time to time, including new features, performance optimizations, and bug fixes. For more information on updates, see [Kernel Version Release Notes](https://www.tencentcloud.com/document/product/1098/44587).

## Data Import and Export
### How do I import data into TDSQL-C for MySQL?
TDSQL-C for MySQL allows you to import data in the following ways:
- Import incremental data continuously by using DTS to sync the data. For directions, see [Sync to TDSQL-C for MySQL](https://intl.cloud.tencent.com/document/product/571/47348).
- Import data through [DMC](https://dms.cloud.tencent.com/#/login?dbType=cynosdbmysql®ion=ap-beijing&instanceId=cynosdbmysql-d09g8oei). You can import existing local files or files stored in COS of up to 10 GB in size at a time. For import files from COS, you need to upload the data to COS first and get the COS file address as instructed in [Uploading Objects](https://www.tencentcloud.com/document/product/436/13321) and [Downloading Objects](https://www.tencentcloud.com/document/product/436/13322).

### How do I import a SQL file greater than 10 GB in size?
**You can upload a file greater than 10 GB in size in the following ways**:
- Split the SQL file into multiple files smaller than 10 GB and upload them in batches.
- Open the SQL file, directly copy the commands in it, and paste and run them in the database.

### How do I migrate data in TDSQL-C for MySQL?
TDSQL-C for MySQL allows you to migrate data through DTS or a command line tool.
For using DTS, see [Migrating to TDSQL-C for MySQL](https://www.tencentcloud.com/document/product/571/47363).
- For using a command line tool, see [Migrating with Command Line Tool](https://intl.cloud.tencent.com/document/product/1098/40638).

### How do I export data from TDSQL-C for MySQL?
You can export data from TDSQL-C for MySQL in the following two ways:
- Use DMC to export data.
TDSQL-C for MySQL is fully compatible with native MySQL at the computing layer, so you can use MySQL's native tools such as MySQLDumper. It also supports open-source data migration tools. For more information, see [Migrating with Command Line Tool](https://intl.cloud.tencent.com/document/product/1098/40638).

## Parameters/Metrics
### Can TDSQL-C for MySQL implement a feature similar to safe-updates?
safe-updates is a safe mode of the database that limits the update (UPDATE or DELETE) of an entire table when an application bug occurs or the database admin performs a maloperation. Similarly, TDSQL-C for MySQL provides the `sql_safe_updates` parameter to achieve this.

You can enable the `sql_safe_updates` parameter in **Parameter Settings** in the [console](https://console.cloud.tencent.com/cynosdb/mysql#/) as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GpCc656_8.png)

### Why does the value of `Threads_created` in TDSQL-C for MySQL keep increasing?
`Threads_created` indicates the number of running threads. If its value keeps increasing, a small amount of memory will be consumed, and more connections will be occupied. You can perform the following operations to observe and end unnecessary sessions.
- Observe how the value of `Threads_created` changes on the **Instance Monitoring** page.
- Run the `show processlist` command or use the real-time session feature of [DBbrain](https://console.cloud.tencent.com/dbbrain/performance/analysis?instId=cynosdbmysql-ins-qw43wuqj) to check the details of running threads.
- If the value of `Threads_created` keeps increasing, you can run the `Kill` command to end some sessions based on your actual business conditions. You can also click **Kill Session** or **Kill Sessions during a Period** on the **Real-Time Session** tab in the DBbrain console.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/u2CV486_9.png)

### How do I modify the `lower_case_table_names` parameter?
The `lower_case_table_names` parameter indicates the table name case sensitivity. You can set this parameter when purchasing a cluster or modify it in the console.

If `lower_case_table_names` is set to `0`, table names will be in the specified letter case and be case-sensitive during comparison. If it is set to `1`, table names will be stored in lowercase and be case-insensitive during comparison. For detailed directions on how to modify this parameter, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/1098/44602).
>!In MySQL 8.0, the table name case sensitivity can be set only during instance purchase but cannot be modified after the purchase.

### How do I modify the maximum number of connections?
You can modify the maximum number of connections in TDSQL-C for MySQL by modifying the `max_connections` parameter in the console. The value range of this parameter is 1–10240, indicating the maximum number of allowed concurrent client connections. For more information, see [Setting Instance Parameters](https://www.tencentcloud.com/document/product/1098/44602).

## Configuration Change
### How do I adjust the configuration of a TDSQL-C for MySQL instance?
TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data.  In cross-server configuration adjustment, no data migration is required; therefore, configuration upgrade/downgrade can be completed within seconds. When the current performance or storage capacity of an instance cannot meet the needs of business changes, or the instance performance is surplus and you want to reduce the costs, you can adjust the instance configuration accordingly.

TDSQL-C for MySQL configuration adjustment includes compute node adjustment and storage space adjustment.
- Compute node configuration adjustment: You can adjust the configuration of compute nodes in the **Instance List**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8JMc866_10.png)
- Storage space configuration adjustment: You can adjust the configuration of the storage space on the **Cluster Details** page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NvTd279_11.png)
>!
>- If the storage space billing mode is pay-as-you-go, you don't need to expand the disk capacity, and the maximum disk capacity you can use is the maximum disk space on the compute node of the source instance. To use a larger storage space, upgrade the compute node of the source instance. For more information on compute node specifications and corresponding maximum storage spaces, see [Product Specifications](https://www.tencentcloud.com/document/product/1098/46430).
>- If the storage space billing mode is monthly subscription, you can adjust the cluster storage space in the console. To use a storage space larger than the maximum storage space of the current compute specifications, upgrade the compute specifications of the read-write instance instance. For more information on compute node specifications and corresponding maximum storage spaces, see [Product Specifications](https://www.tencentcloud.com/document/product/1098/46430).
>- If the storage space billing mode is monthly subscription, the valid billing duration of the new storage capacity will start at the adjustment time and end at the cluster expiration time.
>
For directions, see [Adjusting Compute Configuration](https://www.tencentcloud.com/document/product/1098/50176).

### Does TDSQL-C for MySQL support automatic scaling?
TDSQL-C for MySQL supports automatic scaling for the storage space and computing specification.
- In serverless billing mode, the computing specification and storage space can be automatically scaled based on the actual usage, and you are charged by the used computing and storage resources.
- In non-serverless billing modes, for example, if the computing specification is monthly subscribed and the storage space is pay-as-you-go, then the storage space will be automatically scaled based on the actual usage.

The performance doesn't support automatic scaling. You can [create read-only instances](https://www.tencentcloud.com/document/product/1098/40631) to mitigate the pressure on the source instance.

## Backup and Restoration
### What backup types does TDSQL-C for MySQL support?
TDSQL-C for MySQL supports logical backup and snapshot backup. The former is a full backup, while the latter is a full + incremental backup. For more information, see [Backup and Rollback Overview](https://www.tencentcloud.com/document/product/1098/48391).

- **Logical backup**: It supports full backup only, where the logical structure and content of a database are stored as SQL statements. It backs up database objects, including tables, indexes, and stored procedures. This mode features a more refined backup granularity at the database or table level and a lower impact on the performance; however, it is slow and space-intensive.
- **Snapshot backup**: It uses the redirect-on-write (ROW) technology to take snapshots of the disks at the storage layer for backup. It features fast backup in seconds, imperceptibility to the computing layer, and low space usage.
 - **Full backup**: It copies all the data at a specific time point.
 - **Incremental backup**: It backs up only new or modified files based on the last backup.

### How do I restore data in TDSQL-C for MySQL?
- You can use the rollback feature to restore database tables to the original cluster.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/485r070_12.png)
- You can use the clone feature to restore data. This feature allows you to clone the data of the entire cluster to a new cluster. It can restore a cluster to any time point in the log backup retention period or from the specified backup file through clone.
- You can manually generate a logical backup file in the console and use it to restore data.

## Other Operations in the Console
### How long does it take to create a TDSQL-C for MySQL cluster?
Generally, a cluster can be created within five minutes.
In addition, a read-only instance generally can be created within 30 seconds. The creation time has nothing to do with the data volume.

### How do I modify the table name case sensitivity after initializing a TDSQL-C for MySQL instance?
You need to adjust the `lower_case_table_names` parameter of the database.
- If the compatible database version is MySQL 5.7, you can click the cluster ID in the **Cluster List** to enter the cluster management page, select the **Parameter Settings** tab, and modify the `lower_case_table_names` parameter (`0`: case-sensitive; `1`: case-insensitive).
- If the compatible database version is MySQL 8.0, you can only choose whether to enable case sensitivity for table names when creating an instance on the purchase page. You cannot modify the `lower_case_table_names` parameter after creating the instance.

### How do I return a database?
Select **More** > **Delete** in the **Operation** column in the [Cluster List](https://console.cloud.tencent.com/cynosdb) to return an instance. For more information, see [Deleting Instance](https://www.tencentcloud.com/document/product/1098/44628).

[](id:shilixiaohui)
### How do I restore a TDSQL-C for MySQL cluster?
After a cluster is returned, a monthly subscribed instance will be retained in the recycle bin for 7 days, and a pay-as-you-go instance for 1 day. During the retention period, terminated instances can be recovered from the recycle bin.

[](id:zhanghaomima)
### What do I do if I accidentally delete an account or forget the password?
- If you delete an account accidentally, you can click a cluster ID in the **Cluster List** to enter the instance management page, and then click **Account Management** > **Create Account** or use a SQL statement to create an account.
- If you forgot the root password, select the **Account Management** tab and click **Reset Password** in the **Operation** column.. For more information, see [Resetting Password](https://www.tencentcloud.com/document/product/1098/44611).
The above operations can also be performed through the [CreateAccounts](https://intl.cloud.tencent.com/document/product/1098/46319) API.

### What are the requirements for accounts and passwords in TDSQL-C for MySQL?
- The account name in TDSQL-C for MySQL can contain 1–16 letters, digits, and underscores (_) and must begin with a letter and end with a letter or digit.
- A password in TDSQL-C for MySQL can contain 8–64 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols `~!@#$%^&*_-+=|\\(){}[]:;'<>,.?/`.

### How do I set an alarm for the storage space usage?
The TencentDB storage space is monitored in the monitoring center. You can query the used storage space and utilization on the **Instance Monitoring** page.
When the disk utilization is over the percentage you set, SMS and email alarms will be triggered. You can configure alarm recipients in Tencent Cloud Observability Platform to receive such alarms. For more information on how to configure, see [Alarm Policies](https://intl.cloud.tencent.com/document/product/1098/44597).

### How do I query the task execution status?
You can click the ![](https://qcloudimg.tencent-cloud.cn/raw/afb9f424978974f06abf378c5087d4a6.png) icon on the right of the **Cluster List** to view running tasks. You can also click **Task List** on the left to view the details of all tasks.

