## Instance Management Page
After a TencentDB for MySQL instance is initialized, click the instance name in the instance list or click **Manage** in the "Operation" column to enter the instance management page, where you can view the instance details, monitor the instance, manage databases, or perform other operations.

### Instance details
On the **Instance Details** tab, you can view and manage the database information. Specifically, you can click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> to modify the basic information of the instance. The public network address is disabled by default and can be enabled manually if needed.
![](https://main.qcloudimg.com/raw/be7a1916b3cba0932a015b95fa857d2d.png)

### Instance monitoring
On the **Instance Monitoring** tab, you can view the monitoring data of various core database metrics at the levels of access, load, query cache, table, InnoDB, and MyISAM.
For more information on instance monitoring and alarming, see [Monitoring Feature](https://intl.cloud.tencent.com/document/product/236/8455) and [Alarm Feature](https://intl.cloud.tencent.com/document/product/236/8457).

### Database management
#### Database list
On the **Database Management** > **Database List** tab, you can import SQL files to the specified database.
1. Click **Import Data** to enter the data import page.
2. Click **Add File**, select a local SQL file, and click "OK" to upload it.

#### Parameter settings
On the **Database Management** > **Parameter Settings** tab, you can set modifiable parameters for databases and view the modification history, or click <img src="https://main.qcloudimg.com/raw/071659c8118f8c9b94d4ab90cebbd955.png"  style="margin:0;"> next to **Parameter Value** to modify it. For more information, see [Parameter Template Overview](https://intl.cloud.tencent.com/document/product/236/8461).

#### Account management
On the **Database Management** > **Account Management** tab, you can manage the default root account, such as modifying permissions, resetting password, and creating/deleting accounts.

### Security group
On the **Security Group** tab, you can configure security groups for your databases. For more information, see [Security Group](https://cloud.tencent.com/document/product/236/9537).

### Backup and restoration
On the **Backup and Restore** tab, you can download binlogs and perform cold backup. For more information, see [Backup Modes](https://intl.cloud.tencent.com/document/product/236/7513).

### Operation logs
on the **Operation Log** tab, you can view and download slow logs, error logs, and rollback logs.

### Read-only instances
On the **Read-only Instance** tab, you can create one or more read-only (RO) instances, which can be applied to read-write separation and one-master-multiple-slave application scenarios to boost the read load capacity of your databases. For more information, see [Read-only Instances](https://intl.cloud.tencent.com/document/product/236/7270).

### Connectivity check
On the **Connection Check** tab, you can check for potential connectivity and access problems and address them using the solutions provided so as to ensure that your databases can be accessed normally. For more information, see [One-Click Connection Check](https://cloud.tencent.com/document/product/236/33206).

## Instance List Page
In the TencentDB for MySQL Console, select **Instance List** on the left sidebar to view instance information and manage instances.
![](https://main.qcloudimg.com/raw/ad7eb840269b428dd044ddd45b08545e.png)

### Adjusting configuration
On the **Instance List** page, you can adjust the configuration of your database instance (i.e., scale-up or scale-down). For more information, see [Adjusting Database Instance Specification](https://intl.cloud.tencent.com/document/product/236/19707).

### Rollback
On the **Instance List** page, select the instance to be rolled back and select **More** > **Rollback** to roll it back to a specified time point based on cold backup and binlog. For more information, see [Data Rollback](https://intl.cloud.tencent.com/document/product/236/7276).

### Restart
On the **Instance List** page, select the instance to be restarted and click **Restart**. You can also select multiple instances and restart them in batches.
>
> - During restart, the instance will be inaccessible, and existing connections will be broken. Please back up your data timely.
> - Restart will fail if there are a large number of business writes and dirty pages. In that case, the instance will return to the status before the restart and can still be accessed.
> - Be sure to restart the instance during off-hours so as to ensure success and reduce impact on your business.
