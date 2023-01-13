The database overview page displays the overall call conditions of the current database, including call topology, database response time, throughput, top 5 slow calls, top 5 callers, and exception list.

## Prerequisites
Go to the [**Database overview**](https://console.cloud.tencent.com/apm/monitor/database) page in the APM console.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/FhwS043_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230113113206.png)

### Database call topology
Database call relationships can be displayed in a topology, making it easier for you to view the details of calls between the application and database.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wUg9246_1.png)

**Health:**
**Healthy**: Your application is assessed as healthy based on the response time and error rate.
**Warning**: The current average response time of your application exceeds the satisfaction threshold, but the average error rate does not exceed the alarm threshold.
**Abnormal**: The average error rate of your application exceeds the alarm threshold.

- The satisfaction threshold for the average response time is 500 ms by default.
- The alarm threshold for the average error rate is 5% by default.


### Exception statistics
The list of database exceptions displays the exception type, caller, number of exceptions, first occurrence time, and last occurrence time. You can click **View details** to view specific database exceptions or click **Trace** to view trace details.

### Metric description
| Metric             | Description                                                         |
| :------------------ | :----------------------------------------------------------- |
| Throughput | The average throughput of the current database |
| Avg response time        | The average response time of all calls of the selected database and instance at the 1-minute granularity |
| Top 5 callers | The top 5 upstream applications calling the selected database most frequently |
