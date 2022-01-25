## Error Description
Slow query is the most common performance problem of MongoDB. You can use the slow query management and slow log query features in the [console](https://console.cloud.tencent.com/mongodb) for troubleshooting.

## Cause
- The query is performed with the `$lookup` operator but doesn't use indexes or uses indexes that don't support the query; therefore, it is necessary to traverse the entire database for a complete scan, which eventually leads to a very low search efficiency.
- Some documents in your collection have many large array fields that are time-consuming to search and index, causing a high system load.

## Troubleshooting Procedure
Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) and click an instance ID to enter the instance management page.
- Method 1: select **Database Management** > **Slow Query Management**, and the list will display the requests being executed by the current instance (including requests of secondary nodes). You can click **Batch Kill** to kill slow query statements.
![](https://qcloudimg.tencent-cloud.cn/raw/e6734d302050b074d871c7dca0272f92.png)
- Method 2: select the **Slow Log Query** tab to view and analyze slow logs. The system logs operations executed for more than 100 milliseconds and retains slow logs for 7 days. Currently, slow logs cannot be exported. If needed, contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
If slow queries are heaping too fast, you are recommended to optimize your business based on the slow query analysis result. If the problem persists, contact the aftersales service or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
![](https://qcloudimg.tencent-cloud.cn/raw/90d602dcf863392cb065cb79e5ddc29f.png)

