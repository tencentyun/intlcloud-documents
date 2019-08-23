## Scenario
TencentDB for Redis provides a full range of monitoring and custom alarming capabilities, including metrics such as load monitoring, access statistics, and network traffic.
The monitoring data is collected by the agents deployed on each host and then reported to the data relay node where it is checked, summarized, and reported to the Cloud Monitor system in batches. Cloud Monitor provides data views, data query APIs, and custom alarms.


## Directions
1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance name in the instance list to enter the instance details page.
2. On the **System Monitoring** page, you can view various data entries of the instance and click **Export Data** to save the data to the local file system.
 - The monitored metrics include private network inbound traffic, private network outbound traffic, connections, Get count, Set count, keys, used capacity, capacity utilization, QPS, and CPU load.
 - You can select real time, last 24 hours, last 7 days, or a custom time period to view the monitoring data.
![](https://main.qcloudimg.com/raw/0c5493149b865ccf94088187ca0963cb.png)


