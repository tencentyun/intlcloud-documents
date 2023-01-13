
## Prerequisites
Go to the [**Application list**](https://console.cloud.tencent.com/apm/monitor/system) page in the APM console.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/68SH080_1.png)

## System Overview
The system overview section displays the core performance metrics and call dependencies of all services and components in the selected region as a matrix, list, or topology.

### Application access
You can access a new service or add more services as follows.
1. At the top of the overview page, click **Access application**.
2. On the access guide page, select the programming language, access method, and reporting method and complete reporting as instructed in the console.

<dx-alert infotype="explain" title="">
APM supports multiple programming languages with different access methods. For more information, see [Access Guide](https://www.tencentcloud.com/document/product/1166/51700).
</dx-alert>


### System dashboard
The system dashboard displays the health, number of instances, throughput, average response time, average error rate, average number of errors, Apdex, and change rate of each metric of the accessed application as a list (default) or topology.
Below each metric, day-over-day comparison data is available to help you better monitor the fluctuations of the application performance. You can also click the target application to drill down on the **Application monitoring** page, where you can view more detailed monitoring data of the application.


![](https://staticintl.cloudcachetci.com/yehe/backend-news/sc6m403_2.png)

### Analysis order
By default, services are sorted by health so that you can focus on those with a high error rate and slow response. In the top-left corner of the dashboard, you can switch between sorting dimensions, such as average response time, average throughput, average error rate, Apdex, and health status. If you select **Avg response time**, the slower the response, the higher the order of the service in the system dashboard.

### Displaying top 5 healthy instances monitoring
After this option is enabled, sorting will be based on the health status, and top 5 instances will be displayed at the bottom of each module.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/L8PF727_3.png)

### Switching reporting roles
You can switch between the application data on the client and server for isolated data analysis.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/KmLY041_4.png)



### Global topology dependency
In addition to the list mode, you can also use the topology mode by clicking **Topology** in the top-right corner on the **Application list** page, which helps you organize the dependencies and call relationships between services.
Hover over the target node to view the total number of requests, average response time, and average error rate of the current application. You can also double-click the node to drill down on the **Application details** page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ie5W356_5.png)

### Metric description

| Metric | Description |
|---------|---------|
| Health status | Assesses whether your application is healthy based on the response time and error rate. <br><li>Healthy: Your application is assessed as healthy based on the response time and error rate. <li>Warning: The current average response time of your application exceeds the satisfaction threshold, but the average error rate does not exceed the alarm threshold. </li><li>Abnormal: The average error rate of your application exceeds the alarm threshold. By default, the satisfaction threshold for the average response time is 500 ms, and the alarm threshold for the average error rate is 5%.</li>|
| Response time | The average response time of all service APIs of the application. The percentage below shows the day-over-day change. |
| Throughput | The average number of requests at the 1-minute granularity. |
| Error rate | The average error rate of all APIs at the 1-minute granularity among the call relationships of the selected service. You can click a data point on the curve to drill down to typical requests in the selected time range. |
| Apdex | The user satisfaction metric calculated based on the response time of all APIs at the 1-minute granularity among the call relationships of the selected service. |
| Change rate | The rate of change between the current value and the value yesterday. |

### Health status description
**Healthy:** Your application is assessed as healthy based on the response time and error rate.
**Warning:** The current average response time of your application exceeds the satisfaction threshold, but the average error rate does not exceed the alarm threshold.
**Abnormal:** The average error rate of your application exceeds the alarm threshold.

- The satisfaction threshold for the average response time is 500 ms by default.
- The alarm threshold for the average error rate is 5% by default.
