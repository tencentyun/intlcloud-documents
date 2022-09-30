
A good monitoring environment is the key to ensuring high availability of cloud disks. You can use [Cloud Monitor](https://www.tencentcloud.com/document/product/248) (CM) to monitor cloud disks **[attached](https://intl.cloud.tencent.com/document/product/362/32401) to CVM instances**, view cloud disk metrics, and analyze and configure cloud disk alarms. CM collects raw data of the cloud disk from running CVM instances and displays data through easy-to-read charts. By default, the data is retained for one month, during which you can view the disk conditions in different time periods to better know its usage and read/write operations.
You can get data in the [CM console](https://console.cloud.tencent.com/monitor/cvm) or via [API](https://www.tencentcloud.com/document/product/248/7239). For more information, see [Getting the Monitoring Data of Specified Metrics](https://intl.cloud.tencent.com/document/product/248/6141) and Getting Monitoring View and Chart.
Currently, CM provides the following metrics to monitor cloud disks:

<table>
<thead>

</thead>
<tr>
<th>Metric</th>
<th width="16%">Name</th>
<th width="19%">Calculation</th>
<th width="29%">Description</th>
<th>Unit</th>
<th>Statistical Granularity (Period)</th>
</tr><tbody>
<tr>
<td>DiskReadIops</td>
<td>Disk Read IOPS</td>
<td>Average of read IOPS of the disk during the statistical period</td>
<td>Number of I/O reads from the disk to the memory every second</td>
<td>Count</td>
<td>10s, 60s, 300s</td>
</tr>
<tr>
<td>DiskReadTraffic</td>
<td>Disk Read Traffic</td>
<td>Average of read throughput of the disk during the statistical period</td>
<td>Speed of data reads from the disk to the memory</td>
<td>KB/s</td>
<td>10s, 60s, 300s</td>
</tr>
<tr>
<td>DiskWriteIops</td>
<td>Disk Write IOPS</td>
<td>Average of write IOPS of the disk during the statistical period</td>
<td>Number of I/O writes from the memory to the disk every second</td>
<td>Count</td>
<td>10s, 60s, 300s</td>
</tr>
<tr>
<td>DiskWriteTraffic</td>
<td>Disk Write Traffic</td>
<td>Average of write throughput of the disk during the statistical period</td>
<td>Speed of data writes from the memory to the disk</td>
<td>KB/s</td>
<td>10s, 60s, 300s</td>
</tr>
<tr>
<td>DiskAwait</td>
<td>Disk I/O Wait Time</td>
<td>Average of I/O wait time of the disk during the statistical period</td>
<td>Percentage of time during which the CPU is free and there are unfinished I/O requests during the statistical period</td>
<td>ms</td>
<td>10s, 60s, 300s</td>
</tr>
<tr>
<td>DiskSvctm</td>
<td>Disk I/O Service Time</td>
<td>Average of service time of the disk during the statistical period</td>
<td>I/O service time</td>
<td>ms</td>
<td>10s, 60s, 300s</td>
</tr>
<tr>
<td>DiskUtil</td>
<td>Disk I/O Utilization</td>
<td>Average of I/O utilization of the disk during the statistical period</td>
<td>Percentage of time during which the disk has I/O operations (i.e., non-idle time)</td>
<td>%</td>
<td>10s, 60s, 300s</td>
</tr>
</tbody>
</table>

For more information on monitoring metrics, see [Cloud Monitor](https://www.tencentcloud.com/document/product/248).



