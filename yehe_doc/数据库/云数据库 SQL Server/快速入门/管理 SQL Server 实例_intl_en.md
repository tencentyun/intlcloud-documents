
## Instance List Page
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), and enter the instance list page to view the instance information and manage your instances.
![](https://qcloudimg.tencent-cloud.cn/raw/cba6ded87c20defaa547fb61ebcf6b73.png)

| Feature | Description |
| --------- | ------------------------------------------------------------ |
| Restart | In the instance list, select an instance and click **Restart** at the top to restart it. You can also select multiple instances for batch restart. <li>The instance will be inaccessible during the restart, and existing connections to it will be closed. <li>If the number of business writes is high during the restart, the restart will fail. In this case, the instance will go back to the state before the restart and become accessible. <li>Restart the instance during off-peak hours to ensure success and minimize the impact on your business.</li> |
| Renewal | In the instance list, select one or more target instances, click ** Renew** to renew them by month or year. |
| Setting auto-renewal | In the instance list, select one or more target instances, and click **More** > **Enable Auto-Renewal** to set monthly auto-renewal for them. After you click *OK*, the instances will be automatically renewed monthly upon expiration if your Tencent Cloud account balance is sufficient. |
| Disabling auto-renewal | In the instance list, select one or more target instances marked with **Renew** before their name, click **More** > **Disable Auto-Renewal**, and click **OK**. |
| Tag editing | You can click **More** > **Edit Tag** above the instance list or in the **Operation** column of an instance to manage its tags. If you haven't created a tag, you can click **Tag Management** to create one. |
| Configuration adjustment | In the instance list, you can adjust the configuration of your database instance. Both instance upgrade and disaster recovery mode adjustment are supported. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/238/44352). |
| Publish/Subscribe | In the instance list, you can select **More** > **Publish/Subscribe** in the **Operation** column of an instance to perform publish/subscribe to meet the data replication and sync requirements of your business. |
| Termination/return | In the instance list, you can select **More** > **Terminate/Return** to terminate/return a database instance. For more information, see [Terminating Instance](https://intl.cloud.tencent.com/document/product/238/35787). |
| Pay-as-you-go to monthly subscription | You can switch the instances from pay-as-you-go to monthly subscription. In the instance list, click **More** > **Pay-as-You-Go to Monthly Subscription** in the **Operation** column, select renewal period, and click **OK** after reading the rules.
| Read-Only Instance | In the instance list, you can click **More** > **Read-Only Instance** in the **Operation** column of an instance to view its read-only instances and configure the RO group. If there are no read-only instances, you can click **Create** after redirection to add one or more read-only instances. |

## Instance Management Page
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click the instance ID or **Manage** in the **Operation** column to access the instance management page, where you can view its details, monitor it, and manage databases.
![](https://qcloudimg.tencent-cloud.cn/raw/4dfe4194f4ade5d6d17ee00f20e84f0e.png)

| Feature | Description |
| ---------- | ------------------------------------------------------------ |
| Instance details | On the**Instance Detail** tab, you can view and manage various information of your databases, including setting maintenance information and adding read-only instances in the instance architecture diagram. |
| System monitoring | On the**Instance Monitorin** tab, you can view the monitoring data of various core metrics of the current database. For more information, please see [Monitoring Feature](https://intl.cloud.tencent.com/document/product/238/46503) and [Alarming Feature](https://intl.cloud.tencent.com/document/product/238/46501). |
| Backup and restoration | On the **Backup and Restoration** tab, you can query the backup and restoration records and create a backup and restoration task. Supported backup upload methods include uploading file and downloading file from COS, and supported restoration modes include full backup file, full backups + logs, and full backups + differential backups. |
| Subscription publication | On the **Publish/Subscribe** tab, you can create or delete one or more publish/subscribe linkage services. For more information, see [Publish/Subscribe](https://www.tencentcloud.com/document/product/238/48062) |
| Security group | On the **Security Group** tab, you can configure security groups for your databases. For more information, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789).|
| Account management | On the **Account Management** tab, you can manage the administrator account, such as modifying permissions and resetting password. You can also create and delete accounts. For more information, see [Creating Account](https://intl.cloud.tencent.com/document/product/238/7521). |
| Database management | On the **Database Management** tab, you can create, delete, and set permissions of databases. For more information, see [Database Management](https://intl.cloud.tencent.com/document/product/238/35780). |
| Read-only instances | On the **Read-Only Instance** tab, you can create one or more read-only (RO) instances, which can be applied to read/write separation and one-primary-multiple-replica application scenarios to boost the read load capacity of your databases. For more information, see [Read-Only Instance Overview](https://intl.cloud.tencent.com/document/product/238/43142).|
| Backup management | On the **Backup and Restoration** tab, you can manually create, download, and restore backups. You can also set scheduled backups, and perform rollbacks. For more information, see [Backup Management](https://intl.cloud.tencent.com/document/product/238/45853). |
| Slow query log | On the **Operation Log** tab, you can download slow query logs. |
| Parameter settings | On the **Parameter Configuration** tab, you can view and modify certain parameters and query the parameter modification logs. For more information, see [Parameter Configuration](https://intl.cloud.tencent.com/document/product/238/41609). |

