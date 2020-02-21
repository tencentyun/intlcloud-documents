### Why does the used storage capacity increase while no data is inserted? 
This is because of PostgreSQL's Multi-Version Concurrency Control (MVCC) mechanism:
1. `DELETE` will not physically delete rows.
2. `UPDATE` is implemented by inserting new rows, and expired data will not be physically deleted. Therefore, the used storage capacity can increase even if there is no data inserted.

The `autovacuum` parameter is enabled by default for TencentDB, and expired data will be automatically repossessed by the kernel, so after the repossession, the used storage capacity will be released automatically. You can also run the `VACUUM` command to repossess expired data (in this case, the value of used storage capacity will not decrease immediately; instead, the expired data will be repossessed, and the used storage capacity will be marked reusable). To clear the data completely, you may use the `VACUUM FULL` command with parameters (this command will lock tables, so you are strongly recommended to only use it during maintenance). 
For more information on the `VACUUM` command, please see [PostgreSQL's official documentation](https://www.postgresql.org/docs/current/static/sql-vacuum.html).

### Why does my CPU utilization exceed 100%?
By default, PostgreSQL adopts the policy of overuse of idle resources that allows your business to preempt some idle CPU resources. Therefore, when the number of CPU cores of your instance exceeds the default value, your CPU utilization may appear to exceed 100% in the monitoring view, which is normal.
However, if your CPU load always exceeds 60%, you are recommended to upgrade your database as soon as possible.

### Why is the used disk capacity larger than the actual data volume?
An update can lead to a sharp increase of xlog files, which cannot be archived and deleted in time and hence take up disk capacity. Or, query operations contain sort by and join operations involving massive amounts of data, and during the process, temporary files are generated and overflow to the disk, resulting in a surge in used capacity in a short period of time.

### How to enable or use extensions?
TencentDB for PostgreSQL supports most common extensions for direct use. However, some extensions may require superuser privileges. You can enable them in the Tencent Cloud Console or contact us with the instance ID and extension name.

### What should I pay attention to when restarting a PostgreSQL instance?	
- Given the importance of databases to your business, please be cautious about restart. Before a restart, you are recommended to disconnect your database from the server and stop data writes.
2. Generally, it takes a dozen seconds to a few minutes for the restart to complete. The instance cannot provide any service during this process.
3. There is a chance of failure in restarting a database, which is normal. If it takes more than 10 minutes to restart, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.
4. Restarting an instance will not change any of its physical attributes, so the public and private IPs of the instance and any data stored in it will remain unchanged.
5. After the restart, reconnection to the database is required. Please make sure that your business has a reconnection mechanism.
