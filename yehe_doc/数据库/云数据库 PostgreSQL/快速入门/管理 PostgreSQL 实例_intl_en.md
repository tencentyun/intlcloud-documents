## Instance List Page
You can log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql) and enter the instance list page to view instance information and manage your instances.
![](https://main.qcloudimg.com/raw/2c9a75e6898fdd2b542aaaf3ee937a0b.png)

### Instance restart
>?
>- Exercise great caution when restarting a database, which plays a vital role in the business. Before the restart, we recommend you disconnect the database from server and stop writing data.
>- Restarting an instance does not change its physical attributes, so the public IP, private IP, and any data stored on the instance will remain unchanged.
>- After the restart, reconnection to the database is needed. Make sure your business has a reconnection mechanism.
>- Be sure to restart the instance during off-hours so as to ensure success and reduce impact on your business.

In the **Instance List**, find the instance to be restarted and click **More** > **Restart** in the **Operation** column. You can also select multiple instances and restart them in batches.
>?
>- Generally, it takes tens of seconds to a few minutes to restart an instance, during which the instance cannot be accessed and existing connections to it will be closed.
>- Restart will fail if there are a large number of writes and dirty pages during the restart. In this case, the instance will roll back to the status before the restart and can still be accessed.
>- There is a chance of failure in restarting a database. If it takes more than 10 minutes to restart, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.

## Instance Management Page
After a TencentDB for PostgreSQL instance is created, click its ID in the [instance list](https://console.cloud.tencent.com/pgsql) or click **Manage** in the **Operation** column to enter the instance management page, where you can view its details, monitor it, and manage its databases.
![](https://main.qcloudimg.com/raw/c938dee5a0cad0f4c8a4f2b1fafeb43c.png)

### Instance details
On the **Instance Details** page, you can view and manage the basic information of the instance. The public network address is disabled by default; to use it, enable it manually.

### System monitoring
On the **System Monitoring** page, you can view the monitoring data of various core metrics of the instance, including access, load, cache hit rate, SQL execution latency, XLOG sync delay, etc.
For more information on instance monitoring and alarming, see [Monitoring Feature](https://intl.cloud.tencent.com/document/product/409/7564) and [Alarming Feature](https://intl.cloud.tencent.com/document/product/409/7563).

### Parameter settings
On the **Parameter Settings** page, you can modify parameters in batches or individually and query modification records. For more information, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/409/43239) .

### Account management
On the **Account Management** page, you can manage your account, such as modifying remarks and resetting the password.

### Security group
On the **Security Group** page, you can query security group objects, configure security groups, and preview rules for instances. For more information, see [Managing Security Groups](https://intl.cloud.tencent.com/document/product/409/40112).
>?Security group outbound rules won't take effect for TencentDB for PostgreSQL, and inbound rules only apply to the private IP and port of TencentDB for PostgreSQL.


### Backup management
On the **Backup Management** page, you can view and download backups and xlogs. For more information, see [Backing up Data](https://intl.cloud.tencent.com/document/product/409/34628).

### Performance optimization
On the **Performance Optimization** page, you can view and download slow logs and error logs.

### Read-Only instance
On the **Read-Only Instance** page, you can query and create read-only instances. You can also specify or create an RO group when creating a read-only instance.
