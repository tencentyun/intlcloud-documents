
In Redis, frequently accessed keys are called hot keys. When a Redis database receives a lot of requests to access a hot key, the traffic gets too concentrated and reaches the upper limit of the physical ENI, which will cause problems or even downtime of the Redis service.

With DBbrain's hot key analysis feature, you can find hot keys quickly to optimize the service accordingly.


## Viewing hot key analysis
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Latency Analysis** > **Hot Key Analysis** tab.
2. On the **Hot Key Analysis** tab, you can switch between the real-time and historical views.
 - Real-time view: Displays the analysis results at each time point in real time.
 - Historical view: Displays the analysis results in the last hour, last 3 hours, last 24 hours, last 7 days, or a custom time range.
![](https://qcloudimg.tencent-cloud.cn/raw/f576bf79260a671483d0b4be83da4e5d.png)
