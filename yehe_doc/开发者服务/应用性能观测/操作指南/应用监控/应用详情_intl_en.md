This document describes how to view application details, such as the topology, number of requests, response time, number of errors, and throughput.

## Application Details
1. Go to the [**Application details**](https://console.cloud.tencent.com/apm/monitor/application) page in the APM console.
2. On the **Application details** page, you can view the total number of requests, average response time, average error rate, slow call, slow SQL, number of exceptions, and full GC of the service in the current time range.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/KGNY946_1.png)

### Performance monitoring

This module displays the trend of the average response time, average throughput, average error rate, and Apdex of the application on the selected server or client within the specified time range. You can click the clock icon in the top-right corner of each chart to compare the data of any day in the last 30 days with the current data.


### Call analysis
This module displays the upstream and downstream local topology centered on the current service. Hover over the target node to view the average throughput, response time, and error rate of the corresponding application.
APM uses topology icons in different colors for identification. Green indicates that the application is healthy, orange delayed, and red abnormal.



### JVM monitoring
This module displays the trend of critical JVM metrics, including average/maximum garbage collection (GC) count, CPU utilization, heap space, NoHeap space, heap space refinement, and number of JVM threads.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/LZCN299_2.png)

<table>
 <tr>
<th>Module</th>
<th>Monitoring Metric</th>
</tr>
 <tr>
        <td rowspan="2">GC count</td>
        <td>Full GC count</td>
    </tr>
    <tr>
        <td>Young GC count</td>
    </tr>
    <tr>
        <td rowspan="2">GC time</td>
        <td>Full GC time</td>
    </tr>
    <tr>
        <td>Young GC time</td>
    </tr>
    <tr>
        <td rowspan="3">Heap/NoHeap space</td>
        <td>Committed</td>
    </tr>
        <td>Max </td>
    </tr>
    <tr>
        <td>Used </td>
    </tr>
    <tr>
        <td rowspan="4">Heap space refinement</td>
        <td>Used young generation</td>
    </tr>
    <tr>
        <td>Eden space</td>
    </tr>
    <tr>
        <td>Survivor space</td>
    </tr>
    <tr>
        <td>Old generation</td>
    </tr>
    <tr>
        <td rowspan="6">JVM threads/minute</td>
        <td>Number of TIMED_WAITING threads</td>
    </tr>
    <tr>
        <td>Number of WAITING threads</td>
    </tr>
    <tr>
        <td>Number of RUNNABLE threads</td>
    </tr>
    <tr>
        <td>Number of created threads</td>
    </tr>
    <tr>
        <td>Number of terminated threads</td>
    </tr>
    <tr>
        <td>Number of blocked threads</td>
    </tr>
    </tr>
</table>

### Database monitoring
This module displays the information of database calls, including the average response time, throughput, and top 5 slow calls. You can also click **Overview** or **View SQL** for more details.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/excc642_3.png)


### Metric description

| Metric | Description |
|---------|---------|
| Throughput | The average throughput of the current application |
| Throughput status breakdown | The proportions of successful and failed requests |
| Slow call | The API calls that took more than 500 ms to execute |
| Slow SQL | The SQL queries that took more than 2,000 ms to execute |
| Full GC | The number of full GCs performed by JVM |
| Avg response time | The average response time of all APIs at the 1-minute granularity among the call relationships of the selected service |
| Avg error rate | The average error rate of all APIs at the 1-minute granularity among the call relationships of the selected service |
| Top 5 slow APIs | The top 5 slow APIs at the 1-minute granularity among the call relationships of the selected service |
|Top 5 erroneous APIs | The top 5 erroneous APIs at the 1-minute granularity among the call relationships of the selected service |
| Avg GC times | The average number of GCs executed by all JVM instances per minute |
| Max GC times | The maximum number of GCs executed by all JVM instances per minute |
| Avg GC time | The average duration of GC executions by all JVM instances per minute |
| Max GC time | The maximum duration of GC executions by all JVM instances per minute |
| CPU utilization | The CPU resource utilization of running programs per minute |
| Heap space | The status of the heap space per minute (committed, max, or used)|
| NoHeap space | The status of the NoHeap space per minute (committed, max, or used) |
| Thread pool | The number of active threads in the thread pool per minute |
| Throughput (database)              | The average throughput of the current database                                         |
| Average response time        | The average response time of all calls of the selected database and instance at the 1-minute granularity |
| Top 5 callers | The top 5 upstream applications/components calling the selected database most frequently       |
| Top 5 slow calls | The top 5 slow statements  |


