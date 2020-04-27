ECDN usage statistics allows you to query historical statistics and monitoring data. You can view metrics such as the number of requests, access traffic, and response time.
You can log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Statistics Analysis** on the left sidebar to enter the [Usage Statistics](https://console.cloud.tencent.com/dsa/statistics/amount) page and try out this feature.

## Query Condition Description
+ Time Period: you can query data in the last 12 calendar months with a maximum time span of 31 days.
+ Project: you can query usage by project.
+ Domain Name: you can query usage of the specified domain name.
+ Granularity: it indicates the granularity of queried data and is related to the selected time period.
	1. If the selected time period is 1 day, you can query data at a granularity of 5 minutes, 15 minutes, 30 minutes, 1 hour, 2 hours, and 4 hours.
	2. If the selected time period is 2–3 days, you can query data at a granularity of 15 minutes, 30 minutes, 1 hour, 2 hours, and 4 hours.
	3. If the selected time period is 4–7 days, you can query data at a granularity of 30 minutes, 1 hour, 2 hours, and 4 hours.
	4. If the selected time period is 8–30 days, you can query data at a granularity of 1 hour, 2 hours, and 4 hours.

## Notes on Usage Data Display
The usage data is displayed in three statistics modules:  
- Query overview data: it displays the total usage statistics
- Monitoring details data: it displays detailed historical usage in curves.
- Domain name statistics: it displays usage of each domain name in a list.

### Query details overview
As shown below, the query details overview page displays statistics by account. You can quickly know the total usage in the specified query time period.

### Access statistics
Access statistics displays curves of historical monitoring data, and you can view data of metrics in different categories.
+ Domain names that are connected in 30 days, including deleted ones, will all be added to the **All Domain Names** drop-down list.
+ The real-time monitoring data on the current day is delayed for about 5 minutes. If you perform a query at 14:26:00, the query result will generally be data between 00:00:00 and 14:21:00 on that day.
+ Monitoring statistics are grouped based on granularity. For example, if the query granularity is 5 minutes, statistics data between 10:00:00 and 10:04:59 will be grouped to the `10:00:00` sample point.
+ If the specified query time period is longer than that during which the domain name has been connected, only the statistics of the time period for the connected domain name will be displayed, excluding the time period during which the domain name has not been connected or deleted.
+ To query monitoring data of multiple domain names or metrics, you can use the [monitoring data query API](https://intl.cloud.tencent.com/document/product/570/17942).

### Detailed domain name statistics
As shown below, the list of detailed domain name statistics displays the domain name usage details, and you can sort different metrics to view the data.
