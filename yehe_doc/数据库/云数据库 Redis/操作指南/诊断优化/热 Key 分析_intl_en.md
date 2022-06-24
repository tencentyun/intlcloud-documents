## Feature Description
In Redis, frequently accessed keys are called hot keys. When a Redis database has a high number of requests, if most requests access a specific key, the traffic will become too concentrated and reach the upper limit of the physical ENI, which will cause problems or even downtime of the Redis service.
Through DBbrain's hot key analysis feature, you can find frequently accessed hot keys quickly to optimize the database performance accordingly.

## Viewing Hot Key Analysis Data

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Performance Optimization**.
3. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/e8c526d5dc440af9cf0daf7180cb354b.png)
4. Select the **Latency Analysis** > **Hot Key Analysis** tab and set the collection granularity to **5s**, **15s**, or **30s** as needed in the drop-down list next to **Auto-Refresh** in the top-right corner.
![img](https://qcloudimg.tencent-cloud.cn/raw/d385c21ad2a0ef6c8cb772ff90845b9b.png)
5. View the statistics of hot keys. You can switch between the real-time and historical views.
 - **Real-time view**
   By default, the access frequency of the current database's hot keys is displayed in real time.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/eb7046c76fc89d3968bf735460605b92.png)
 - **Historical view**
   Click **Historical** to view the statistics in the last 1, 3, or 24 hours or last 7 days. You can also click <img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" /> in the time selection box to query the statistics in a period of up to 7 days in the last month.
	 ![img](https://qcloudimg.tencent-cloud.cn/raw/dfb35f711729054df0cdfe27c3754afb.png)
   
