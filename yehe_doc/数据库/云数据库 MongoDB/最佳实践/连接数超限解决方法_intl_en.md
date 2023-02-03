

## Problem Description
If the number of connections exceeds the upper limit, you can use the connection management and restart features in the [console](https://console.cloud.tencent.com/mongodb) and optimize the service for troubleshooting.

## Cause
-  There are connection leaks, improper client coding, unreasonable connection pool configuration, or many unreleased connections.
-  There is a large number of concurrent application requests, and the configured upper limit of connections is insufficient, so the current database specification cannot sustain such requests.

## Troubleshooting
### Option 1. Increase the connections
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) and click an instance ID to enter the instance management page.
2. Select **Database Management** > **Manage Connection** and view the source IPs and number of connections for service troubleshooting.
>?
>-  If the number of connections reaches or exceeds 80% of the upper limit and affects the establishment of new connections, you can click **Increase Connections** in the console to increase the maximum number of connections to 150% of the original limit for the next 6 hours.
>- If the problem persists, contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ri5n110_44-en.png)

### Option 2. Restart the instance
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) and click an instance ID to enter the instance management page.
2. Select **Database Management** > **Manage Connection**. You can click **Restart** on the right to restart mongos to fix the problem.
>?
>- Replica sets on v4.0 don't have mongos.
>- Restarting the mongod is highly risky and will cause a momentary disconnection, during which if data is written, rollback may be triggered, leading to data loss. Therefore, the restart feature is not enabled by default. If you need to enable it, contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vBAW555_45-en.png)

### Option 3. Optimize the business
You can troubleshoot the business for optimization.

