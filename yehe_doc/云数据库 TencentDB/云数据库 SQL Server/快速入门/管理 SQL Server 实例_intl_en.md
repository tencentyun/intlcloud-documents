## Instance List Page
You can log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) and enter the instance list page to view instance information and manage your instances.


| Feature | Description |
| --------- | ------------------------------------------------------------ |
| Upgrade | In the instance list, you can adjust the configuration of your database instance. Instance upgrade and disaster recovery mode adjustment are supported. For more information, please see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783). |
| Restart | In the instance list, select an instance and click **Restart** to restart it. You can also select multiple instances for batch restart. <li>During the restart, the instance will be inaccessible, and existing connections to it will be closed. Please be prepared for the restart to avoid business interruption. <li>During the restart, if the number of business writes is high, the restart will fail. In this case, the instance will go back to the state before the restart and become accessible. <li>Please restart instances during off-peak hours to ensure the restart success rate and reduce the impact on your business. |
| Termination/return | In the instance list, you can select **More** > **Terminate/Return** to terminate/return a database instance. For more information, please see [Terminating Instance](https://intl.cloud.tencent.com/document/product/238/35787). |

## Instance Management Page
Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver). On the instance list page, click the instance ID or click **Manage** in the "Operation" column and enter the instance management page, where you can view its details, monitor it, and manage databases.


| Feature | Description |
| ---------- | ------------------------------------------------------------ |
| Instance details | On the "Instance Details" tab, you can view and manipulate various information of your databases, including setting maintenance information and adding "read-only instances" in the instance architecture diagram. |
| System monitoring | On the "Instance Monitoring" tab, you can view the monitoring data of various core metrics of the current database. For more information, please see [Monitoring Feature](https://intl.cloud.tencent.com/document/product/238/7524) and [Alarming Feature](https://intl.cloud.tencent.com/document/product/238/35791). |
| Publishing/Subscription   | On the "Publish/Subscribe" tab, you can create or delete one or more pub/sub linkage services. |
| Security group | On the "Security Group" tab, you can configure security groups for your databases. For more information, please see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789). |
| Account management | On the "Manage Account" tab, you can manage the administrator account, such as modifying permissions and resetting password. You can also create and delete accounts. For more information, please see [Account Management](https://intl.cloud.tencent.com/document/product/238/7521). |
| Database management | On the "Manage Database" tab, you can create, set permissions of, and delete databases. For more information, please see [Database Management](https://intl.cloud.tencent.com/document/product/238/35780). |
| Read-only instance | On the "Read-only Instance" tab, you can create one or more read-only (RO) instances, which can be applied to read/write separation and one-master-multiple-slave application scenarios to boost the read load capacity of your databases. |
| Backup management | On the "Backup and Restore" tab, you can manually create backups, download backups, set scheduled backups, restore backups, and perform rollbacks. For more information, please see [Backup Management](https://intl.cloud.tencent.com/document/product/238/35790). |
| Slow query log | On the "Operation Log" tab, you can download slow query logs. |

