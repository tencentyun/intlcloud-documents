The performance trends feature of DBbrain not only supports the selection of multiple performance metrics such as key metrics, all metrics, and custom metrics, but also supports multiple ways to view performance trends, such as fine-grained view of one single performance metric trend, link comparison view of multiple performance metric trends, and time comparison view of multiple performance metric trends.

>?Currently, the performance trends feature is supported only for TencentDB for MySQL (excluding the basic single-node instance).
>
![](https://main.qcloudimg.com/raw/21d421be543c040140dd7a6a86226ef0.png)

## Viewing Performance Trend Metrics
The performance trends feature supports selection of multiple performance metrics, including 4 categories (Resource Monitoring, MySQL Server, InnoDB Engine, and MySQL Replication) and 15 subcategories. You can select different metrics based on different OPS needs to view the performance trends of the selected instance against the selected metrics.

1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **Performance Trends** tab.
2. On the performance trends page, click the **Select performance metrics** drop-down list.
3. On the performance metrics selection page, check performance metrics or select **Key Metrics**, **Select all** or **Deselect all** in the top-right corner, and click **OK**.
>?Click **Apply to all instances** to apply the selected metrics to all database instances.
>
![](https://main.qcloudimg.com/raw/11d33834252e836eebc908ac9c18cb07.png)

The performance trends feature currently supports the following performance metrics:
<table>
<tr>
<td rowspan=7>Resource Monitoring</th>
<td>CPU</th><td>CPU</th></tr>
<tr>
<td rowspan=2 >Memory</td><td>Memory</td></tr>
<tr>
<td>Memory usage</td></tr>
<tr>
<td rowspan=2>Storage space</td><td>Disk utilization</td></tr>
<tr>
<td>Occupied disk space</td></tr>
<tr>
<td rowspan=2>Traffic</td><td>Outbound traffic</td></tr>
<tr>
<td>Inbound traffic</td></tr>
<tr>
<td rowspan=13>MySQL Server</td>
<td>TPS/QPS</td><td>TPS/QPS</td></tr>
<tr>
<td rowspan=4>Connection</td>
<td>Max connections</td></tr>
<tr>
<td>Connected threads</td></tr>
<tr>
<td>Running threads</td></tr>
<tr>
<td>Created threads</td>
<tr>
<td rowspan=6>Requests</td>
<td>Select</td></tr>
<tr>
<td>Update</td></tr>
<tr>
<td>Delete</td></tr>
<tr>
<td>Insert</td></tr>
<tr>
<td>Replace</td></tr>
<tr>
<td>Total requests</td></tr>
<tr>
<td rowspan=2>Slow query</td>
<td>Slow queries</td></tr>
<tr>
<td>Full-table scans</td></tr>
<tr>
<td rowspan=14>InnoDB Engine</td>
<td rowspan=4>InnoDB buffer pool pages</td>
<td>InnoDB empty pages</td>
<tr>
<td>Total InnoDB pages</td>
<tr>
<td>InnoDB logical reads</td>
<tr>
<td>InnoDB physical reads</td>
<tr>
<td rowspan=2>Read/Written InnoDB data</td>
<td>InnoDB reads</td>
<tr>
<td>InnoDB writes</td>
<tr>
<td rowspan=2>InnoDB data reads/writes</td>
<td>Total InnoDB reads</td></tr>
<tr>
<td>Total InnoDB writes</td></tr>
<tr>
<td rowspan=4>InnoDB row operations</td>
<td>InnoDB rows deleted</td></tr>
<tr>
<td>InnoDB rows inserted</td></tr>
<tr>
<td>InnoDB rows updated</td></tr>
<tr>
<td>InnoDB rows updated</td></tr>
<tr>
<td rowspan=2>InnoDB row lock</td>
<td>InnoDB row lock waits</td></tr>
<td>Average InnoDB row lock acquiring time</td></tr>
<tr>
<td rowspan=4>MySQL Replication</td>
<td rowspan=2>Replication status</td>
<td>Source-replica delay distance</td></tr>
<tr>
<td>Source-replica delay time</td>
<tr>
<td rowspan=2>Replication delay</td>
<td>IO thread status</td></tr>
<tr>
<td>SQL thread status</td></tr>
</tbody></table>


## Enabling Chart Interaction
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **Performance Trends** tab.
2. On the performance trends page, toggle on the **Chart Interaction** switch in the top-right corner to view the link comparison of multiple performance metric trends.
![](https://main.qcloudimg.com/raw/8f0143e681567f928b115fae7ddf23ca.png)
Drag on the view for fine-grained display of one single performance metric trend.
![](https://main.qcloudimg.com/raw/54b877aeee9d5ae2495b4496489caa2d.png)

## Switching Between Real-Time/Historical Views
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **Performance Trends** tab.
2. Click **Real-Time** or **Historical** to view the corresponding real-time or historical performance trends.
 - The real-time performance trends view allows you to view the performance trends of the instance over the last 3 minutes and is automatically refreshed by default. Click **Disable refresh** to stop refreshing the trends in real time.
![](https://main.qcloudimg.com/raw/81e13852a0356469df194eb685f2a12a.png)
 - In the historical performance trends view, you can select a time period to display the view of performance trends over the selected time period, and you can switch among the last hour, last 3 hours, last 24 hours, last 7 days, and custom time period.
![](https://main.qcloudimg.com/raw/8883b09c4f7b2b28b60299ba61c6b5d7.png)
Click **Add Time Comparison** and select the desired time period for comparison to view the time comparison of multiple performance metric trends.
![](https://main.qcloudimg.com/raw/696f8ccd768423e1aefaed587e8da3c2.png)
