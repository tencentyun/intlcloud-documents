## Issue Description
When the CPU utilization of a TencentDB for MySQL exceeds 80%, the service response may slow down or time out, or the database cannot be connected.

You can view the CPU utilization of a TencentDB for MySQL instance on the instance monitoring page in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) or in the [DBbrain console](https://console.cloud.tencent.com/dbbrain/event?product=mysql).

>?When the CPU utilization gets too high, we recommend you increase the CPU specification first as instructed in [Adjusting Database Instance Specification](https://intl.cloud.tencent.com/document/product/236/19707) to ensure normal business operations. Subsequently, you can refer to this document for troubleshooting and optimization.

## Impact
If MySQL's CPU utilization remains high for a prolonged time, the overall performance of the database will be severely compromised, and under extreme circumstances, instances may be hung.

When the HA system detects such an issue, it will trigger a source-replica switch to maintain the high availability of your business. During the switch, instances are usually unavailable for less than 60 seconds. If the switch occurs during peak hours, business stability and continuity will be seriously affected.

To protect your business from being affected by CPU resource shortage, we recommend that you optimize the application or upgrade the CPU resources for the instance with a high CPU utilization. A source-replica switch is accompanied by a disconnection lasting for just seconds; therefore, for persistent connections, your application should have a reconnection mechanism.

## Common Causes
MySQL's CPU resources are mainly used by system threads and user threads. Therefore, if CVMs are for exclusive use by your TencentDB for MySQL instances, you can solve most of the issues just by focusing on the two types of threads.

### User threads
In most cases, busy user threads are caused by slow queries, heavy computation, and high QPS (queries per second).

- **Slow queries**
Querying that involves ORDER BY, GROUP BY, temp tables, joins, etc. is so inefficient that the computation of a single SQL statement takes much longer CPU time.
- **Heavy computation**
Heavy computation is caused just by huge amounts of data.
- **High QPS**
CPU time is prolonged just by a high QPS. For example, if a four-core server sustains a high QPS of 20,000 to 30,000, the total CPU time can be very long even when the CPU time of a single SQL statement is short.

### System threads
In a production environment, system thread issues are less frequent. In general, the CPU utilizations of multiple system threads are rarely too high or close to 100% at the same time as long as the CVM has at least four available CPU cores. However, there are a few bugs that may affect the CPU utilization, as shown in the figure below:
![](https://main.qcloudimg.com/raw/e7c078a31b983fec2990801bfabde282.png)

## Solutions
As most CPU issues are caused by busy user threads, the following sections focus on the solutions to high CPU utilization caused by user threads.
- Slow queries: To identify and optimize slow queries, we recommend DBbrain. For more information, see [Slow queries](#mcx).
- Heavy computation: To solve the high CPU utilization issue caused by huge amounts of data, see [Heavy computation](#jsld).
- High QPS: To solve the high CPU utilization issue caused by too many access requests, see [High QPS](#gqps).

## Troubleshooting
### [Slow queries](id:mcx)
Use DBbrain to identify and optimize the SQL statements which cause a high CPU utilization:
- **Exception diagnosis (recommended)**: This feature detects and diagnoses exceptions 24/7 and provides optimization suggestions in real time. For more information, see [Method 1 (recommended). Use the exception diagnosis feature to troubleshoot database exceptions](https://intl.cloud.tencent.com/document/product/1035/36053).
- **Slow SQL analysis**: This feature analyzes slow SQL statements of the current instance and provides optimization suggestions. For more information, see [Method 2. Use the "slow SQL analysis" feature to troubleshoot SQL statements that lead to high CPU utilization](https://intl.cloud.tencent.com/document/product/1035/36053).
- **Audit log analysis**: This feature performs in-depth analysis on SQL statements and provides optimization suggestions based on TencentDB audit data (full SQL). For more information, see [Method 3. Use the "audit log analysis" feature to troubleshoot SQL statements that cause high CPU utilization](https://intl.cloud.tencent.com/document/product/1035/36053).

In MySQL, slow query time (`long_query_time`) is set to 10 seconds by default. After a performance issue occurs, if no slow query is found, we recommend you adjust the parameter value to 1 second and then observe whether there are slow queries in a business cycle, and if yes, optimize the slow queries accordingly. After the parameter is adjusted, if still no slow queries are found but the CPU utilization remains high, we recommend you upgrade the CPU configuration so as to improve the overall performance of the database.

### [Heavy computation](id:jsld)
When MySQL handles huge amounts of data, its CPU utilization can be high, even if the indexes and query execution plans work well. Moreover, such an issue can still occur at a low concurrency due to MySQL's one-thread-per-connection feature

Generally, there are two common solutions:
- Enable read/write separation. Run this type of queries on a read-only replica node where the business access pressure is low.
- Optimize your program to split a large SQL query into smaller ones.

### [High QPS](id:gqps)
- Upgrade CPU specification to improve the overall database performance.
- Use read-only instances to share the load of the source instance.
- Optimize query statements to enhance efficiency.


