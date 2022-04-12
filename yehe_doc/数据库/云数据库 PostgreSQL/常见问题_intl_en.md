### Why does the used storage space increase while no data is inserted? 
This is because of PostgreSQL's Multi-Version Concurrency Control (MVCC) mechanism:
1. `DELETE` will not physically delete rows.
2. `UPDATE` is implemented by inserting new rows, and expired data will not be physically deleted. Therefore, the used storage capacity can increase even if there is no data inserted.

The `autovacuum` parameter is enabled by default for TencentDB, and expired data will be automatically repossessed by the kernel, so after the repossession, the used storage space will be released automatically. You can also run the `VACUUM` command to repossess expired data (in this case, the value of used storage capacity will not decrease immediately; instead, the expired data will be repossessed, and the used storage capacity will be marked reusable). To clear the data completely, you may use the `VACUUM FULL` command with parameters (this command will lock tables, so we strongly recommend you only use it during maintenance). 
For more information on the `VACUUM` command, see [VACUUM](https://www.postgresql.org/docs/current/static/sql-vacuum.html).

### Why does my CPU utilization exceed 100%?
By default, PostgreSQL adopts the policy of overuse of idle resources that allows your business to preempt some idle CPU resources. Therefore, when the number of CPU cores of your instance exceeds the default value, your CPU utilization may appear to exceed 100% in the monitoring view, which is normal.
However, if your CPU load always exceeds 60%, we recommend you upgrade your instance as soon as possible.

### Why is the used disk capacity larger than the actual data volume?
An update can lead to a sharp increase of xlog files, which cannot be archived and deleted in time and hence take up disk capacity. Or, query operations contain `ORDER BY` and `JOIN` operations involving massive amounts of data, and during the process, temp tables are generated and overflow to the disk, resulting in a surge in used capacity in a short period of time.

### How do I enable or use extensions?
TencentDB for PostgreSQL supports most common extensions for direct use. However, some extensions may require superuser privileges. You can enable them in the Tencent Cloud console or contact us with the instance ID and extension name.

### What should I pay attention to when restarting a PostgreSQL instance?	
- Exercise great caution when restarting a database, which plays a vital role in the business. Before the restart, we recommend you disconnect the database from the server and stop writing data.
- Restarting an instance does not change its physical attributes, so the public IP, private IP, and any data stored on the instance will remain unchanged.
- After the restart, reconnection to the database is needed. Make sure that your business has a reconnection mechanism.
- Restart the instance during off-peak hours to ensure success and minimize the impact on your business.
- Generally, it takes tens of seconds to a few minutes to restart an instance, during which the instance cannot be accessed and existing connections to it will be closed.
- Restart will fail if there are a large number of writes and dirty pages during the restart. In this case, the instance will roll back to the status before the restart and can still be accessed.
- There is a chance of failure in restarting a database. If it takes more than ten minutes to restart, you can [contact us](https://intl.cloud.tencent.com/contact-us) for help.

### How do I terminate an instance?
You can log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres) and manually terminate an instance from the instance list.

### How do I upgrade the PostgreSQL version?
TencentDB for PostgreSQL currently does not support version upgrades. If you need to upgrade the major version, do so by migrating the instance data with [DTS](https://intl.cloud.tencent.com/document/product/571/42640).


