This document describes operations on the instance list and management pages in the TencentDB for MySQL console.

## Instance List Page
You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and enter the instance list page to view instance information and manage your instances.
![](https://main.qcloudimg.com/raw/51001a389fec3fc1d62d45ff0f0895f9.png)

| Feature | Description |
|---------|---------|
| Configuration adjustment | In the instance list, you can adjust the configuration (i.e., scaling) of your database instance. Both instance upgrade and downgrade are supported. For more information, please see [Adjusting Database Instance Specification](https://intl.cloud.tencent.com/document/product/236/19707). |
| Rollback | In the instance list, select the instance to be rolled back and click **More** > **Rollback** at the top to roll it back to a specified time point based on cold backup and binlog. For more information, please see [Database Rollback](https://intl.cloud.tencent.com/document/product/236/7276).|
| Restart | In the instance list, select an instance and click **Restart** at the top to restart it. You can also select multiple instances for batch restart. <li>During the restart, the instance will be inaccessible, and existing connections to it will be closed. <li>During the restart, if the number of business writes is high and there are too many dirty pages, the restart will fail. In this case, the instance will go back to the state before the restart and become accessible. <li>Please restart instances during off-peak hours to ensure the restart success rate and reduce the impact on your business. |

## Instance Management Page
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). After an instance is initialized, click its ID/name in the instance list or click **Manage** in the **Operation** column to enter the instance management page, where you can view its details, monitor it, and manage databases.
![](https://main.qcloudimg.com/raw/167ee41bc241ef2e5a68c5fc160112d4.png)

| Feature | Description |
|---------|---------|
| Instance details | On the [Instance Details](https://console.cloud.tencent.com/cdb) tab, you can view and manipulate various information of the database. Click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> to modify the basic information of the instance, where the public network address is disabled by default. If needed, click **Enable** after **Public Network Address** to enable it. |
| Instance monitoring | On the **Instance Monitoring** tab, you can view the monitoring data of various core metrics of the current database in various dimensions such as access, load, query cache, table, InnoDB, and MyISAM. For more information, please see [Monitoring Feature](https://intl.cloud.tencent.com/document/product/236/8455) and [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457). |
| Database management | <li> **Database List** <br>On this tab, you can import SQL files into a specified database. For more information, please see [Importing SQL File](https://intl.cloud.tencent.com/document/product/236/8466). <li>**Parameter Settings**<br>On this tab, you can set and view the history of customizable database parameters. Click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> in the **Current Value** column to modify the parameter value. For more information, please see [Managing Parameter Templates](https://intl.cloud.tencent.com/document/product/236/31906). <li>**Manage Account**<br>On this tab, you can manage the system's default root account, such as modifying permissions and resetting password. You can also create and delete account. For more information, please see [Account Management](https://intl.cloud.tencent.com/document/product/236/31900). |
| Security group | On the **Security Group** tab, you can configure security groups for your databases. For more information, please see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).|
| Backup and restoration | On the **Backup and Restore** tab, you can download binlogs and perform cold backup. For more information, please see [Backing up Databases](https://intl.cloud.tencent.com/document/product/236/37796).|
| Operation log | On the **Operation Log** tab, you can view and download slow query logs, error log, and rollback logs. For more information, please see [Operation Logs](https://intl.cloud.tencent.com/document/product/236/34588). |
| Read-only replicas | On the **Read-only Replica** tab, you can create one or more read-only (RO) replicas, which can be applied to read/write separation and one-source-multiple-replica application scenarios to boost the read load capacity of your databases. For more information, see [Creating Read-only Replicas](https://intl.cloud.tencent.com/document/product/236/7270).|
| Connection Check | On the **Connection Check** tab, you can check for potential connectivity and access problems and address them using the solutions provided so as to ensure that your databases can be accessed normally. For more information, please see [One-Click Connectivity Checker](https://intl.cloud.tencent.com/document/product/236/31927).|

