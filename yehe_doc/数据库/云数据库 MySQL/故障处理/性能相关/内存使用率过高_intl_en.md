
## Issue Description
A TencentDB for MySQL instance experiences a sudden surge or a continuous growth in memory utilization. You can view specific memory utilization monitoring data in the following chart:
![](https://main.qcloudimg.com/raw/56d978df5b08cd8320bf36654df783ab.png)
After a sudden surge or a steady slow growth, the memory utilization reaches an unhealthy level of more than 96% and fluctuates slightly. In this case, the memory utilization may trigger custom TCOP memory alarms many times.

## Impact
Inefficient SQL statements or improper database parameters can cause the memory utilization to increase. An unexpected business peak may cause OOM (out of memory) of two-node and three-node TencentDB for MySQL instances, and when the instances are unavailable due to OOM, a source-replica switch will be triggered. During the switch, instances are usually unavailable for less than 60 seconds. If the switch occurs during peak hours, business stability and continuity will be seriously affected.

## Solutions
In MySQL, memory can be roughly divided into two parts: globally shared memory and session-level private memory.
- Shared memory is allocated upon the creation of an instance and shared by all connections.
- Private memory is allocated by the system upon connection to the MySQL server.
  Some special SQL statements or field types may cause the muliti-alloacation of cache to a single threadTherefore, all OOM exceptions are caused by the private memory of each connection. The risk of high memory utilization can be mitigated by limiting database connections and optimizing inefficient SQL statements. If this doesn't work, you can upgrade the memory configuration to improve the overall concurrency and stability of the database. For more information on memory parameters, see [Memory Allocation](https://intl.cloud.tencent.com/document/product/236/31922).

## Troubleshooting
1. Optimize slow SQL statements to reduce the session-level private memory usage. You can use DBbrain to [analyze slow SQL statements](https://intl.cloud.tencent.com/document/product/1035/36038).
2. Reduce invalid persistent connections by downgrading the connection pool configuration or concurrency level on the program side without affecting the business.You can use DBbrain to [view the current session information](https://intl.cloud.tencent.com/document/product/1035/36037).
3. Monitor memory utilization (optional and applicable to MySQL 5.7 and above): enable the performance schema feature, and query memory information from tables whose name starts with "memory_summary" in the performance_schema database. For example, the memory_summary_global_by_event_name table records global memory utilization.
4. After optimization, [upgrade the configuration of your TencentDB for MySQL instance](https://intl.cloud.tencent.com/document/product/236/19707).

>?
>- During the upgrade, your business can operate normally. After the upgrade, there will be a momentary disconnection. Make sure that your business has a reconnection mechanism.
>- To protect your business from being affected by insufficient memory or CPU resources, configure alarm policies for instance resources which help you identify potential resource shortage in advance. For more information, see [Alarm Policies (TCOP)](https://intl.cloud.tencent.com/document/product/236/8457).
