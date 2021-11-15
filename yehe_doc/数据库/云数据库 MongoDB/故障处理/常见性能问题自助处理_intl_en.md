TencentDB for MongoDB provides a self-service troubleshooting solution in the console to help you quickly and easily troubleshoot common MongoDB performance problems.

## Increased Slow Queries
### Problem description
Slow query is the most common performance problem of MongoDB. You can use the slow query management and slow log query features in the [console](https://console.cloud.tencent.com/mongodb) for troubleshooting.

### Solution
Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and click an instance name to enter the instance management page.
- Method 1: select **Manage database** > **Slow Query Management** and the list will display the requests being executed by the current instance (including requests of slave nodes). You can click **Batch Kill** to kill slow query statements.
![](https://main.qcloudimg.com/raw/2ad30ab71f422ab04f8d976d7141431e.png)
- Method 2: select the **Slow Log Query** tab to view and analyze slow logs. The system logs operations executed for more than 100 milliseconds and retains slow logs for 7 days. Currently, slow logs cannot be exported. If needed, please contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
If slow queries are heaping too fast, you are recommended to optimize your business based on the slow query analysis result. If the problem persists, please contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
![](https://main.qcloudimg.com/raw/bc23258b0b37fc4e5452d9a10d08b8b5.png)

## Number of Connections Exceeding Limit
### Problem description
If the number of connections exceeds the upper limit, you can use the connections management and restart features in the [console](https://console.cloud.tencent.com/mongodb) and optimize the service for troubleshooting.

### Solution
#### Method 1. Increase the upper limit
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and click an instance name to enter the instance management page.
2. Select **Manage Database** > **Manage Connection** and view the source IPs and number of connections for service troubleshooting.
>?
>-  If the number of connections reaches or exceeds 80% of the upper limit and affects the establishment of new connections, you can click **Increase Connections** in the console to increase the maximum number of connections to 150% of the original limit for the next 6 hours.
>- If the problem persists, please contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://main.qcloudimg.com/raw/5dcbb694ef6c6e93d772949ad954843b.png)

#### Method 2. Restart the instance
1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and click an instance name to enter the instance management page.
2. Select **Manage Database** > **Manage Connection**. You can click **Restart** on the right to restart the mongos instance to fix the problem.
>?
>- Replica sets on v4.0 do not have mongos instances.
>- Restarting the mongod instance is highly risky and will cause a momentary disconnection, during which if data is written, rollback may be triggered, leading to data loss. Therefore, the restart feature is not enabled by default. If you need to enable it, please contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://main.qcloudimg.com/raw/1957a425df76df5d731bef86767dd692.png)

#### Method 3. Optimize the service
You can troubleshoot the service for optimization.
