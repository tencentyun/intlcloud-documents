## Instance List Page
You can log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql) and enter the instance list page to view instance information and manage your instances.

### Upgrading an instance
On the **Instance List** page, click **Upgrade** in the "Operation" column to upgrade the configuration of a database instance, including its specification and disk capacity.

### Restarting an instance
On the **Instance List** page, select the desired instance and click **Restart**. You can also select multiple instances and restart them in batches.
>
> - During the restart, the instance cannot be accessed, and existing connections to it will be closed. Please back up your data timely.
> - Restart will fail if there are a large number of business writes and dirty pages. In this case, the instance will return to the status before the restart and can still be accessed.
> - Be sure to restart the instance during off-hours so as to ensure success and reduce potential impact on your business.

## Instance Management Page
After a TencentDB for PostgreSQL instance is initialized, click its name in the [instance list](https://console.cloud.tencent.com/pgsql) or click **Manage** in the "Operation" column to enter the instance management page, where you can view its details, monitor it, and manage databases.
![](https://main.qcloudimg.com/raw/33b2f22f24deddd1d9602e064c7b1a9a.png)

### Instance details
On the **Instance Details** page, you can view and manage the basic information of the databases. The public network address is disabled by default. If you need to use it, please enable it manually.

### System monitoring
On the **System Monitoring** page, you can view the monitoring data of various core metrics of the current database, including access, load, cache hit rate, SQL execution latency, and XLOG sync delay.
For more information on instance monitoring and alarming, please see [Monitoring Feature](https://cloud.tencent.com/document/product/409/7564) and [Alarm Feature](https://cloud.tencent.com/document/product/409/7563).

### Account management
On the **Account Management** page, you can manage your account, such as modifying remarks and resetting the password.

### Backup management
On the **Backup Management** page, you can view and download backup and xlog files. For more information, please see [Backing up Data](https://cloud.tencent.com/document/product/409/33945).

### Performance optimization
On the **Performance Optimization** page, you can view and download slow logs and error logs.

