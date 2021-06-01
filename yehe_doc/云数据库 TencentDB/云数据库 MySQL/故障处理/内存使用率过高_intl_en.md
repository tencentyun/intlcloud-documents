
## Symptoms
A TencentDB for MySQL instance experiences a sudden surge or a continuous growth in memory utilization. You can view detailed memory utilization monitoring data in the following chart:
![](https://main.qcloudimg.com/raw/56d978df5b08cd8320bf36654df783ab.png)
After a sudden surge or a steady slow growth, the memory utilization reaches an unhealthy level of more than 96% and fluctuates slightly. In this case, the memory utilization may trigger custom Cloud Monitor memory alarms many times.

## Impact
Inefficient SQL statements or incorrect database parameters can cause the memory utilization to increase. An unexpected business peak may trigger OOM (out of memory) of two-node and three-node TencentDB for MySQL instances, resulting in a source-replica switch. During the switch, instances are usually unavailable for less than 60 seconds. If the switch occurs during peak hours, business stability and continuity will be seriously affected.

## Solutions
In MySQL, memory can be roughly divided into two parts: globally shared memory and session-level private memory.
- Shared memory is allocated upon the creation of an instance and shared by all connections.
- Private memory is allocated by the system upon connection to the MySQL server.
  Some special SQL statements or field types may cause cache to be allocated to a single thread repeatedly. Therefore, all OOM exceptions are caused by the private memory of each connection. The risk of high memory utilization can be mitigated by limiting database connections and optimizing inefficient SQL statements. If this doesn't work, you can upgrade the memory configuration so as to improve the overall concurrence and stability of the database. For more information on memory parameters, see [FAQs > Performance and Memory > Memory Allocation](https://intl.cloud.tencent.com/document/product/236/31922).

## Troubleshooting Procedure
1. Optimize slow SQL statements to reduce session-level private memory usage.
2. Reduce invalid persistent connections and lower the connection pooling configuration and concurrency of the application without affecting the business.
3. Monitor memory utilization (optional and only applicable to MySQL 8.0): enable the performance schema feature, and query memory information from tables whose name starts with "memory_summary" in the performance_schema database. For example, the memory_summary_global_by_event_name table records global memory utilization.
4. If the preceding steps don't work, [upgrade the configuration of your TencentDB for MySQL instance](https://intl.cloud.tencent.com/document/product/236/19707).

>?
>- During the upgrade, your business can operate normally. After the upgrade, there will be a switchover accompanied by an interruption lasting for just seconds. Please make sure that your business has a reconnection mechanism.
>- To protect your business from being affected by insufficient memory or CPU resources, configure alarm policies for instance resources which help you identify potential resource shortage in advance. For more information, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
