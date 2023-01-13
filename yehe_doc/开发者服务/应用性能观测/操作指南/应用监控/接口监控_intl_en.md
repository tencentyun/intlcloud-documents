The API monitoring module displays the APIs in client, server, and local calls as well as the call traces in the upstream and downstream services, allowing you to check the key metrics like the number of requests, average response time, error rate, and throughput.

## Prerequisites
Go to the [**API monitoring**](https://console.cloud.tencent.com/apm/monitor/interface) page in the APM console.

### API overview
On the **API monitoring** page, select the target API on the left to display **API analysis** and **Exception analysis** on the right. You can select the target caller to view its details.

### API analysis
API analysis allows you to select the target API service and view its total throughput, top 5 callers, average response time (99, 90, or 50 pct), error rate, and error code breakdown.

| Metric | Description |
|---------|---------|
|Top 5 callers |	The top 5 upstream applications/components calling the selected application API most frequently |
| Error code breakdown | The distribution trend of error codes returned by the current API |

>?
>- 99 pct: Data in the 99th percentile in ascending order.
>- 90 pct: Data in the 90th percentile in ascending order.
>- 50 pct: Data in the 50th percentile in ascending order.

### Exception statistics
Besides basic metrics, you can also view top 5 APIs in the current application in terms of average response time and error rate, which are intelligently filtered by the exception analysis module. You can click **View details** above the curve to view the call trace of the target API in the last 15 minutes, so you can drill down to the issue to troubleshoot it quickly. 

### Upstream and downstream analysis
You can switch between the **Upstream analysis** and **Downstream analysis** tabs to analyze upstream and downstream calls and quickly identify performance bottlenecks.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/uSFu051_1.png)

