The system monitoring of TencentDB for SQL Server supports 25 common parameters of SQL Sever. You can collect statistics of other parameters by configuring the counters of SSMS.
## Currently Supported Parameters
<body>
### Common Parameters

| Metric | Description (unit) | Five-minute value | Optimization suggestion |
|:----:|----|:-----:|--------|
| CPU utilization <br>(Total Processor Time) | Actual CPU utilization (%) | max | < 30% Good <br>< 60% Good <br>> 60% Attention required |
| Number of transactions <br>(Transaction/sec) | Average transactions per second (times/second) | max | Dependent on business needs |
| Number of connections <br>(User Connection) | Average users connections to the database per second (-) | max | Dependent on business needs |
| Number of requests <br>(Batch Requests/sec) | - (times/second) | max | Dependent on business needs |
| Number of logins per second <br>(Logins/sec) | Logins per second (times/second) | max | Dependent on business needs |
| Number of logouts per second <br>(Logouts/sec) | Logouts per second (times/second) | max | Dependent on business needs |
| Used storage space <br>(Storage Space) | Sum of space occupied by instance database files and log files (GB) | max | <30% Good <br><60% Good <br>>60% Attention required |
| Incoming network traffic <br>(Network Receive Throughput) | Sum of all incoming packets of all connections (MB/s) | max | Dependent on business needs |
| Outgoing network traffic <br>(Network Transmit Throughput) | Sum of all outgoing packets of all connections (MB/s) | max | Dependent on business needs |
| Disk IOPS <br>(IPOS) | Disk reads/writes (times/second) | max | Follow the suggestions for IOPS in the instance specs center <br>< 30% Good <br>< 60% Good <br>> 60% Attention required |
| Number of disk reads <br>(Read IOPS) | Disk reads per second (times/second) | max | Dependent on business needs |
| Number of disk writes <br>(Write IOPS) | Disk writes per second (times/second) | max | Dependent on business needs |
</body>
<body>
### Performance Optimization Parameters

| Metric | Description (unit) | Five-minute value | Optimization suggestion |
|:----:|----|:-----:|--------|
| Slow queries <br>(SlowQuery) | Number of queries running for more than one second (-) | avg | < 1 Good <br>< 10 Normal <br>> 10 Attention required |
| Blocking processes <br>(Processes blocked) | Current number of blocking processes (-) | avg | Dependent on business needs |
| Number of locked requests <br>(Lock Requests/sec) | Average locked requests per second (times/second) | avg | Dependent on business needs|
| Number of user errors <br>(User Error/sec) | Average errors per second (times/second) | avg | 0 Good <br>> 0 Attention required |
| Number of lock waits <br>(Lock waits) | Lock requests requiring caller to wait per second (times/second) | avg | Dependent on business needs |
| Number of SQL compilations <br>(SQL Compilation/sec) | Average SQL compilations per second (times/second) | avg | Dependent on business needs |
| Number of SQL recompilations <br>(SQL Re-Compilation/sec) | Average SQL recompilations per second (times/second) | avg | Dependent on business needs |
| Incoming network traffic <br>(Network Receive Throughput) | Sum of all incoming packets of all connections (MB/s) | avg | Dependent on business needs |
| Outgoing network traffic <br>(Network Transmit Throughput) | Sum of all outgoing packets of all connections (MB/s) | avg | Dependent on business needs |
| Number of full-table scans by SQL per second <br>(Full Scans/sec) | Disk reads/writes (times/second) | avg | Follow the suggestions for IOPS in the instance specs center <br>< 30% Good <br>< 60% Good <br>> 60% Attention required |
| Buffer cache hit rate <br>(Buffer cache hit ratio) | Data cache (memory) hit rate (%) | avg | >= 95% Good <br>>= 90% Normal <br>< 90% Attention required |
| Number of latch waits per second <br>(Latch Waits/sec) | Latch waits per second (times/sec) | avg | Dependent on business needs |
| Average lock wait delay <br>(Average Wait Time) | Average wait time for each lock request that causes a wait (ms) | max | Dependent on business needs |
| Average network IO delay <br>(Network IO waits) | Average network IO delay time (ms) | max | Dependent on business needs |
| Plan cache hit rate <br>(Plan Cache: Cache Hit Ratio) | Hit rate of the execution plan of each SQL (%) | max | >= 95% Good <br>>= 90% Normal <br>< 90% Attention required |
</body>
>As SQL Server adopts a full-use mechanism for the memory, there is no need to monitor the direct memory space metric. You can check the memory usage by viewing the cache hit rate.

## Currently Supported Alarm Metrics
Currently, alarming is supported for key system performance metrics. Alarming from Tencent Cloud Monitor isn't available for other metrics for the time being. You can configure alarm capabilities in "Tencent Cloud Console > Cloud Monitor > My Alarms > Alarm Policies".
![](//mccdn.qcloud.com/static/img/b5912eec83886f728ea2dadf596551d5/image.png)
At present, alarming is supported for the following monitoring metrics. The recommended alarm thresholds are as detailed above (in Table 1).
- CPU utilization
- Number of connections
- Incoming traffic
- Outgoing traffic
- IOPS
- Storage space
