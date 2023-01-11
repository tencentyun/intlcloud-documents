This document describes the common monitoring metrics supported by TencentDB for SQL Server.

## Monitoring metrics
The monitoring of TencentDB for SQL Server supports 37 common metrics of SQL Server. You can collect statistics of other metrics by configuring the performance counters of SQL Server Management Studio (SSMS).
>?To view monitoring metrics at the system level, [contact us](https://www.tencentcloud.com/zh/contact-us). 

<table>
<thead>
<tr><th>Category</th><th>Metric</th><th>Parameter</th><th>Unit</th><th>Description</th></tr></thead>
<tbody><tr>
<td>CPU</td>
<td>Total processor time</td><td>Total Processor Time</td><td>%</td><td>Actual CPU utilization</td></tr>
<tr>
<td rowspan=5>Memory</td>
<td>Memory usage</td><td>Server memory</td><td>MB</td><td>Used size of the total memory</td></tr>
<tr>
<td>Max memory</td><td>Max memory</td><td>KB</td><td>Maximum memory</td></tr>
<tr>
<td>Memory utilization</td><td>Memory Usage</td><td>%</td><td>Memory utilization</td></tr>
<tr>
<td>Internally locked memory</td><td>Total Allocated Memory</td><td>KBytes</td><td>Locked memory of internal systems<dx-alert infotype="notice" title="">
This metric is available only for version 2014 and later.
</dx-alert></td></tr>
<tr>
<td>Internally used memory</td><td>Total Used Memory</td><td>KBytes</td><td>Used memory of internal systems<dx-alert infotype="notice" title="">
This metric is available only for version 2014 and later.
</dx-alert></td></tr>
<tr>
<td rowspan=12>Storage</td>
<td>Disk IOPS</td><td>IOPS</td><td>counts/sec</td><td>Number of disk reads/writes</td></tr>
<tr>
<td>Disk reads</td><td>Read IOPS</td><td>counts/sec</td><td>Number of disk reads per second</td></tr>
<tr>
<td>Disk writes</td><td>Write IOPS</td><td>counts/sec</td><td>Number of disk writes per second</td></tr>
<tr>
<td>Used storage space</td><td>Storage Space</td><td>GB</td><td>Sum of space used by instance database files and log files</td></tr>
<tr>
<td>Free storage space</td><td>Free Storage</td><td>%</td><td>Percentage of free disk space calculated in the following way: (purchased disk space - used storage space) / purchased disk space</td></tr>
<tr>
<td>Avg read IO response time</td><td>Avg. Disk Sec/Read</td><td>ms</td><td>Average response time of each read IO (monitoring at the system level)</td></tr>
<tr>
<td>Avg write IO response time</td><td>Avg. Disk Sec/Write</td><td>ms</td><td>Average response time of each write IO (monitoring at the system level)</td></tr>
<tr>
<td>Avg IO response time</td><td>Avg. Disk sec/Transfer</td><td>ms</td><td>Average response time of each IO request (monitoring at the system level)</td></tr>
<tr>
<td>Disk read IO per sec</td><td>Disk Reads/sec</td><td>counts/sec</td><td>Number of disk read IO per second (monitoring at the system level)</td></tr>
<tr>
<td>Disk write IO per sec</td><td>Disk Writes/sec</td><td>counts/sec</td><td>Number of disk write IO per second (monitoring at the system level)</td></tr>
<tr>
<td>Total disk IOPS</td><td>Disk Transfers/sec</td><td>counts/sec</td><td>Number of total disk IOPS (monitoring at the system level)</td></tr>
<tr>
<td>Disk queue length</td><td>Disk Queue Length</td><td>-</td><td>Disk queue length (monitoring at the system level)</td></tr>
<tr>
<td rowspan=3>Network</td>
<td>Inbound traffic</td><td>Network Receive Throughput</td><td>KB/s</td><td>Sum of all inbound packets of all connections</td></tr>
<tr>
<td>Outbound traffic</td><td>Network Transmit Throughput</td><td>KB/s</td><td>Sum of all outbound packets of all connections</td></tr>
<tr>
<td>Network IO waits</td><td>Network IO waits</td><td>ms</td><td>Average network IO delay time</td></tr>
<tr>
<td rowspan=3>Connection</td>
<td>User connections</td><td>User Connections</td><td>-</td><td>Average number of user connections to database per second</td></tr>
<tr>
<td>Logins/sec</td><td>Logins/sec</td><td>counts/sec</td><td>Number of logins per second</td></tr>
<tr>
<td>Logouts/sec</td><td>Logouts/sec</td><td>counts/sec</td><td>Number of logouts per second</td></tr>
<tr>
<td rowspan=9>Access</td>
<td>Slow queries</td><td>SlowQuery</td><td>-</td><td>Number of queries running for more than one second</td></tr>
<tr>
<td>Requests</td><td>Batch Requests</td><td>counts/sec</td><td>Average number of requests per second</td></tr>
<tr>
<td>SQL compilations</td><td>SQL Compilations/sec</td><td>counts/sec</td><td>Average number of SQL compilations per second</td></tr>
<tr>
<td>SQL re-compilations</td><td>SQL Re-Compilations/sec</td><td>counts/sec</td><td>Average number of SQL re-compilations per second</td></tr>
<tr>
<td>Full scans/sec</td><td>Full Scans/sec</td><td>counts/sec</td><td>Number of full scans per second</td></tr>
<tr>
<td>Transactions</td><td>Transactions/sec</td><td>counts/sec</td><td>Number of transactions per second</td></tr>
<tr>
<td>Processes blocked</td><td>Processes blocked</td><td>-</td><td>Current number of processes blocked</td></tr>
<tr>
<td>Plan cache hit ratio</td><td>Plan Cache: Cache Hit Ratio</td><td>%</td><td>Hit ratio of the execution plan of each SQL</td></tr>
<tr>
<td>Buffer cache hit ratio</td><td>Buffer cache hit ratio</td><td>%</td><td>Buffer cache (memory) hit ratio</td></tr>
<tr>
<td rowspan=5>Lock</td>
<td>Lock requests</td><td>Lock Requests/sec</td><td>counts/sec</td><td>Average number of lock requests per second</td></tr>
<tr>
<td>Latch waits/sec</td><td>Latch Waits/sec</td><td>counts/sec</td><td>Number of latch waits per second</td></tr>
<tr>
<td>Average wait time</td><td>Average wait time</td><td>Ms</td><td>Average wait time for each lock request that causes a wait</td></tr>
<tr>
<td>Deadlocks</td><td>Number of deadlocks/sec</td><td>counts/sec</td><td>Number of lock requests that cause deadlocks per second</td></tr>
<tr>
<td>Blocked process threshold</td><td>Blocked process threshold</td><td>sec</td>
<td>This is the specified threshold for generating a blocked process report. If it is exceeded, a blocked process report will be generated. By default, no blocked process reports will be generated</td></tr>
<tr>
<td>Others</td>
<td>User errors</td><td>User Error/sec</td><td>counts/sec</td><td>Average number of errors per second</td></tr>
</tbody></table>

