## Feature description

DBbrain's performance trends feature not only supports the selection of multiple performance metrics such as key metrics, all metrics, and custom metrics, but also supports multiple ways to view performance trends, such as fine-grained view of one single performance metric trend, as well as link comparison view and time comparison view of multiple performance metric trends.

## Supported performance metrics

**TencentDB for MySQL**

<table>
<tr><th>Category</th><th>Subcategory</th><th>Metric</th></tr>
<tr>
<td rowspan=7>Resource Monitoring</td>
<td>CPU</th><td>CPU</td></tr>
<tr>
<td rowspan=2 >Memory</td>
<td>Memory</td></tr>
<tr><td>Memory Usage</td></tr>
<tr>
<td rowspan=2>Storage Space</td>
<td>Disk Utilization</td></tr>
<tr><td>Occupied Disk Space</td></tr>
<tr>
<td rowspan=2>Traffic</td>
<td>Outbound Traffic</td></tr>
<tr><td>Inbound Traffic</td></tr>
<tr>
<td rowspan=13>MySQL Server</td>
<td>TPS/QPS</td>
<td>TPS/QPS</td></tr>
<tr>
<td rowspan=4>Connection</td>
<td>Max Connections</td></tr>
<tr><td>Connected Threads</td></tr>
<tr><td>Running Threads</td></tr>
<tr><td>Created Threads</td></tr>
<tr>
<td rowspan=6>Requests</td>
<td>Select</td></tr>
<tr><td>Update</td></tr>
<tr><td>Delete</td></tr>
<tr><td>Insert</td></tr>
<tr><td>Replace</td></tr>
<tr><td>Total Requests</td></tr>
<tr>
<td rowspan=2>Slow Query</td>
<td>Slow Queries</td></tr>
<tr><td>Full-Table Scans</td></tr>
<tr>
<td rowspan=14>InnoDB Engine</td>
<td rowspan=4>InnoDB Buffer Pool Pages</td>
<td>InnoDB Empty Pages</td></tr>
<tr><td>Total InnoDB Pages</td></tr>
<tr><td>InnoDB Logical Reads</td></tr>
<tr><td>InnoDB Physical Reads</td></tr>
<tr>
<td rowspan=2>Read/Written InnoDB Data</td>
<td>InnoDB Reads</td></tr>
<tr><td>InnoDB Writes</td></tr>
<tr>
<td rowspan=2>InnoDB Data Reads/Writes</td>
<td>Total InnoDB Reads</td></tr>
<tr><td>Total InnoDB Writes</td></tr>
<tr>
<td rowspan=4>InnoDB Row Operations</td>
<td>InnoDB Rows Deleted</td></tr>
<tr><td>InnoDB Rows Inserted</td></tr>
<tr><td>InnoDB Rows Updated</td></tr>
<tr><td>InnoDB Rows Read</td></tr>
<tr>
<td rowspan=2>InnoDB Row Lock</td>
<td>InnoDB Row Lock Waits</td></tr>
<td>Average InnoDB Row Lock Acquiring Time</td></tr>
<tr>
<td rowspan=4>MySQL Replication</td>
<td rowspan=2>Replication Status</td>
<td>Source-Replica Delay Distance</td></tr>
<tr><td>Source-Replica Delay Time</td></tr>
<tr>
<td rowspan=2>Replication Delay</td>
<td>IO Thread Status</td></tr>
<tr><td>SQL Thread Status</td></tr>
</tbody></table>

**Self-built MySQL**

<table>
<thead><th colspan=3>Monitoring Metric</th><th>Agent Access</th><th>Direct Access</th></th></thead>
<tr>
<td rowspan=7>Resource Monitoring</td>
<td>CPU</td><td>CPU</td><td>&#10003;</td><td>×</td></tr>
<tr>
<td rowspan=2 >Memory</td>
<td>Memory</td><td>&#10003;</td><td>×</td></tr>
<tr>
<td>Memory Usage</td><td>&#10003;</td><td>×</td></tr>
<tr>
<td rowspan=2>Storage Space</td>
<td>Storage Utilization</td><td>&#10003;</td><td>×</td></tr>
<tr>
<td>Used Storage Space</td><td>&#10003;</td><td>×</td></tr>
<tr>
<td rowspan=2>Traffic</td>
<td>Outbound Traffic</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Inbound Traffic</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=13>MySQL Server</td>
<td>TPS/QPS</td><td>TPS/QPS</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=4>Connection</td>
<td>Max Connections</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Connected Threads</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Running Threads</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Created Threads</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=6>Requests</td>
<td>Select</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Update</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Delete</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Insert</td><td>&#10003;</td><td>&#10003;</td></tr>
</tr>
<tr>
<td>Replace</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Total Requests</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=2>Slow Query</td>
<td>Slow Queries</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Full-Table Scans</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=14>InnoDB Engine</td>
<td rowspan=4>InnoDB Buffer Pool Pages</td>
<td>InnoDB Empty Pages</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Total InnoDB Pages</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>InnoDB Logical Reads</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>InnoDB Physical Reads</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=2>Read/Written InnoDB Data</td>
<td>InnoDB Reads</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>InnoDB Writes</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=2>InnoDB Data Reads/Writes</td>
<td>Total InnoDB Reads</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Total InnoDB Writes</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=4>InnoDB Row Operations</td>
<td>InnoDB Rows Deleted</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>InnoDB Rows Inserted</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>InnoDB Rows Updated</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>InnoDB Rows Read</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan=2>InnoDB Row Lock</td>
<td>InnoDB Row Lock Waits</td><td>&#10003;</td><td>&#10003;</td></tr>
<td>Average InnoDB Row Lock Acquiring Time</td><td>&#10003;</td><td>&#10003;</td></tr>
</tbody></table>

**TDSQL-C for MySQL**

<table>
<tr><th>Category</th><th>Subcategory</th><th>Metric</th></tr>
<tr><td rowspan=7>Resource Monitoring</td>
<td>CPU</th><td>CPU</td></tr>
<tr>
<td rowspan=2 >Memory</td>
<td>Memory</td></tr>
<tr><td>Memory Usage</td></tr>
<tr>
<td rowspan=2>Storage Space</td>
<td>Storage Utilization</td></tr>
<tr><td>Used Storage Space</td></tr>
<tr>
<td rowspan=2>Traffic</td>
<td>Outbound Traffic</td></tr>
<tr><td>Inbound Traffic</td></tr>
<tr>
<td rowspan=13>MySQL Server</td>
<td>TPS/QPS</td><td>TPS/QPS</td></tr>
<tr>
<td rowspan=4>Connection</td>
<td>Max Connections</td></tr>
<tr><td>Connected Threads</td></tr>
<tr><td>Running Threads</td></tr>
<tr><td>Created Threads</td></tr>
<tr>
<td rowspan=6>Requests</td>
<td>Select</td></tr>
<tr><td>Update</td></tr>
<tr><td>Delete</td></tr>
<tr><td>Insert</td></tr>
<tr><td>Replace</td></tr>
<tr><td>Total Requests</td></tr>
<tr>
<td rowspan=2>Slow Query</td>
<td>Slow Queries</td></tr>
<tr><td>Full-Table Scans</td></tr>
<tr>
<td rowspan=6>InnoDB Engine</td>
<td rowspan=4>InnoDB Row Operations</td>
<td>InnoDB Rows Deleted</td></tr>
<tr><td>InnoDB Rows Inserted</td></tr>
<tr><td>InnoDB Rows Updated</td></tr>
<tr><td>InnoDB Rows Read</td></tr>
<tr>
<td rowspan=2>InnoDB Buffer Pool Pages</td>
<td>InnoDB Logical Reads</td></tr>
<tr><td>InnoDB Logical Writes</td></tr>
<tr>
<td rowspan=3>MySQL Replication</td>
<td rowspan=1>Replication Status</td>
<td>Replication Status of Replica Instance</td></tr>
<tr>
<td rowspan=2>Replication Delay</td>
<td>Redo Log LSN Difference between Source and Replica Instances</td></tr>
<tr><td>Replica Instance Delay in Redo Log Based Replication</td></tr>
</tbody></table>

## Viewing performance trend metrics

1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Performance Trends** tab.
2. On the **Performance Trends** tab, select specific performance metrics or select **Key Metrics**, **Select All**, or **Deselect All** in the top-right corner, and click **Save**.
>?Click **Save** to apply the selected metrics to the current database instance, or click **Save and Apply to All Instances** to apply the selected metrics to all database instances.
>
![](https://main.qcloudimg.com/raw/11d33834252e836eebc908ac9c18cb07.png)
3. View metrics.
   - **Chart interaction**: Click **Chart Interaction** on the right to link and compare the monitoring views of multiple instances or metrics.
     When you hover over a data point in any monitoring view, the data at the same time point will be displayed in other monitoring views. Click the data point to pin it for display. To unpin it, click **Deselect the Time Point**.
![](https://qcloudimg.tencent-cloud.cn/raw/d8ff35464928227b8d5b237e3422b317.png)
   - **Switching between the one-column and two-column modes**: Click the button on the right of **Chart Interaction** in the top-right corner to switch.
![](https://qcloudimg.tencent-cloud.cn/raw/cc2ea12a1e76b53f3fdf4b170b293aba.png)
   - **Dragging a monitoring view**: Click the border of a monitoring view to drag it to the desired position.
   - **Zooming in a monitoring view**: Drag the icon in the bottom-right corner of a monitoring view to zoom it in for fine-grained display of the trend of one single performance metric.
![](https://qcloudimg.tencent-cloud.cn/raw/b0194330aea62733e7008eaed1edbe1d.png)
   - **Switching between the real-time and historical modes**: Click **Real-Time** or **Historical** to view the real-time or historical performance trends.
     - The real-time performance trends view displays the performance trends of the instance and is automatically refreshed by default. You can click **Disable refresh** to stop refreshing the trends in real time.
![](https://main.qcloudimg.com/raw/81e13852a0356469df194eb685f2a12a.png)
     - In the historical performance trends view, you can select a time range (**Last hour**, **Last 3 hours**, **Last 24 hours**, **Last 7 days**, or a custom time range) to display the performance trends over the selected time range.
![](https://main.qcloudimg.com/raw/696f8ccd768423e1aefaed587e8da3c2.png)
        Click **Add Time Comparison** and select the desired time range for comparison to view the time comparison of multiple performance metric trends.
![](https://main.qcloudimg.com/raw/8883b09c4f7b2b28b60299ba61c6b5d7.png)       
        
