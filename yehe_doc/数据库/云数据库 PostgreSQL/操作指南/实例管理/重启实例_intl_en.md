Restart is indispensable to the maintenance of databases. Restarting a PostgreSQL instance is equivalent to restarting a database (service and process) on a local server.

## Notes
- Please exercise great caution when restarting a database, which plays a vital role in the business. Before the restart, it is recommended to disconnect the database from server and stop writing data.
- Restarting an instance does not change its physical attributes, so the public IP, private IP, and any data stored on the instance will remain unchanged.
- After the restart, reconnection to the database is needed. Please make sure your business has a reconnection mechanism.
- Be sure to restart the instance during off-hours so as to ensure success and reduce impact on your business.

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql), locate the desired instance in the instance list, and click **More** > **Restart** in the **Operation** column.
>?
>- Generally, it takes a few seconds to minutes to restart an instance, during which the instance cannot be accessed and existing connections to it will be closed.
>- Restart will fail if there are a large number of writes and dirty pages during the restart. In this case, the instance will roll back to the status before the restart and can still be accessed.
>- There is a chance of failure in restarting a database. If it takes more than 10 minutes to restart, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.
>
2. In the pop-up dialog box, indicate your consent and click **Confirm**.
![](https://main.qcloudimg.com/raw/2ef5507eba82d2e45f7b790113842d48.png)
