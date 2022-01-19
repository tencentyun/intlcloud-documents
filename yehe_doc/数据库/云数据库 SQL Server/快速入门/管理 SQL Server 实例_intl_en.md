## Instance List Page
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and enter the instance list page to view the instance information and manage your instances.
![](https://qcloudimg.tencent-cloud.cn/raw/cba6ded87c20defaa547fb61ebcf6b73.png)

| Feature | Description |
| --------- | ------------------------------------------------------------ |
| Restart | In the instance list, you can select an instance and click **Restart** at the top to restart it. You can also select multiple instances for batch restart. <li>During the restart, the instance will be inaccessible, and existing connections to it will be closed. <li>During the restart, if the number of business writes is high, the restart will fail. In this case, the instance will go back to the state before the restart and become accessible. <li>Restart instances during off-peak hours to ensure the restart success rate and reduce the impact on your business.</li> |
| Tag editing | You can click **More** > **Edit Tag** above the instance list or in the **Operation** column of an instance to manage its tags. If you haven't created a tag, you can click **Tag Management** to create one. |
| Upgrade | In the instance list, you can adjust the configuration of your database instance. Instance upgrade and disaster recovery mode adjustment are supported. For more information, see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783). |
| Publishing/Subscription | In the instance list, you can select **More** > **Publish/Subscribe** in the **Operation** column of an instance to perform publishing/subscription to meet the data replication and sync requirements of your business. |
| Termination/Return | In the instance list, you can select **More** > **Terminate/Return** to terminate/return a database instance. For more information, see [Terminating Instance](https://intl.cloud.tencent.com/document/product/238/35787). |
| Read-Only Instance | In the instance list, you can click **More** > **Read-Only Instance** in the **Operation** column of an instance to view its read-only instances and configure the RO group. If there are no read-only instances, you can click **Create** after redirection to add one or more read-only instances. |

## Instance Management Page
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page, where you can view the instance details and monitor and manage databases.
![](https://qcloudimg.tencent-cloud.cn/raw/4dfe4194f4ade5d6d17ee00f20e84f0e.png)

| Feature | Description |
| ---------- | ------------------------------------------------------------ |
| Instance details | On the **Instance Details** tab, you can view and manipulate various information of your databases, including setting maintenance information and adding "read-only instances" in the instance architecture diagram. |
| System monitoring | On the**Instance Monitoring** tab, you can view the monitoring data of various core metrics of the current database. For more information, see [Monitoring Feature](https://intl.cloud.tencent.com/document/product/238/7524) and [Alarming Feature](https://intl.cloud.tencent.com/document/product/238/35791). |
| Backup and restoration   | On the **Backup and Restoration** tab, you can query the backup and restoration records and create a backup and restoration task. Supported backup upload methods include uploading file and downloading file from COS, and supported restoration modes include full backup file, full backups + logs, and full backups + differential backups. |
| Publishing/Subscription   | On the **Publish/Subscribe** tab, you can create or delete one or more pub/sub linkage services. |
| Security group | On the **Security Group** tab, you can configure security groups for your databases. For more information, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789). |
| Account management | On the **Account Management** tab, you can manage the administrator account, such as modifying permissions and resetting password. You can also create and delete accounts. For more information, see [Account Management](https://intl.cloud.tencent.com/document/product/238/7521). |
| Database management | On the **Database Management** tab, you can create, set permissions of, and delete databases. For more information, see [Database Management](https://intl.cloud.tencent.com/document/product/238/35780). |
| Read-Only instances | On the **Read-Only Instance** tab, you can create one or more read-only instances, which can be applied to read/write separation and one-source-multiple-replica application scenarios to boost the read load capacity of your databases. For more information, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/238/43142).|
| Backup management | On the **Backup and Restoration** tab, you can manually create backups, download backups, set scheduled backups, restore backups, and perform rollbacks. For more information, see [Backup Management](https://intl.cloud.tencent.com/document/product/238/35790). |
| Slow query log | On the **Operation Log** tab, you can download slow query logs. |
| Parameter settings | On the **Parameter Configuration** tab, you can view and modify certain parameters and query parameter modification records. For more information, see [Parameter Configuration](https://intl.cloud.tencent.com/document/product/238/41609). |

