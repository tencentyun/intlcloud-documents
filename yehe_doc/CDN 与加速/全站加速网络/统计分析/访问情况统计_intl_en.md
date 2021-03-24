ECDN usage statistics allow you to query historical statistics and monitoring data. You can view metrics such as the number of requests, access traffic, and response time.
You can log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Statistics** on the left sidebar to enter the [Usage Statistics](https://console.cloud.tencent.com/dsa/statistics/amount) page and try out this feature.

## Query Condition Description
+ Time Period: you can query data in the last 12 calendar months with a maximum time span of 31 days.
+ Project: you can query usage by project.
+ Domain Name: you can query usage of the specified domain name.
+ Granularity: it indicates the granularity of queried data and is subject to the selected time period.
	1. If the selected time period is 1 day, you can query data at a granularity of 5 minutes, 15 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, or 24 hours.
	2. If the selected time period is 2–3 days, you can query data at a granularity of 15 minutes, 30 minutes, 1 hour, 2 hours, or 4 hours.
	3. If the selected time period is 4–7 days, you can query data at a granularity of 30 minutes, 1 hour, 2 hours, or 4 hours.
	4. If the selected time period is 8–30 days, you can query data at a granularity of 1 hour, 2 hours, 4 hours, or 24 hours.

![](https://main.qcloudimg.com/raw/f8374efc34eae11696d1b129561cfc70.png)

## Notes on Usage Data Display
The usage data is displayed in three statistics modules:  
- Query overview data: it displays the total usage statistics.
- Monitoring details: it displays detailed historical usage in curves.
- Domain name statistics: it displays usage of each domain name in a list.

### Query details overview
As shown below, the query details overview page displays statistics by account. You can quickly view the total usage in the specified query time period.
![](https://main.qcloudimg.com/raw/3a05573f6f28a299e04626f52e1bb365.png)

### Access statistics
The access statistics section displays curves of historical monitoring data. You can view data of metrics in different categories.
+ All domain names that were connected in the last 30 days, including deleted ones, will be included in the **All Domain Names** drop-down list.
+ The real-time monitoring data on the current day is delayed for about 5 minutes. If you perform a query at 14:26:00, the query result will generally include data between 00:00:00 and 14:21:00 on the day.
+ Monitoring statistics are grouped by granularity. For example, if the query granularity is 5-minute, statistics between 10:00:00 and 10:04:59 will be grouped to the `10:00:00` sample point.
+ If the specified query time period is longer than the domain name connection period, only the statistics of the connection period will be displayed, while the time period during which the domain name has not been connected or has been deleted will be excluded.
+ To query monitoring data of multiple domain names or metrics, you can use the GetDsaStatistics API.

![](https://main.qcloudimg.com/raw/6831a48251c2aa8adf03aa23b4b18f95.png)

### Detailed domain name statistics
As shown below, the list of detailed domain name statistics displays the domain name usage details. You can sort different metrics to view the data.
![](https://main.qcloudimg.com/raw/4b3ab927cd139581edb7c594e88078a0.png) 
