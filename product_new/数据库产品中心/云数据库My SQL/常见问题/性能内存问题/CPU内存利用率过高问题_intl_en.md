### High CPU Utilization
#### Cause
During the use of MySQL, the CPU utilization reaches or even exceeds 100%. This issue is mainly caused by a high number of inefficient SQL statements (most likely) or row locking conflicts (unlikely) in the database.

#### Risk
If MySQL's CPU utilization remains at 100% for a prolonged time, the overall performance of the database will be severely compromised. Under extreme circumstances, instances may be hung. When the HA monitor detects such an issue, it will trigger the master/slave switchover to help maintain the high availability of your business. During the switch, your business will be unavailable for a very short period of time (generally less than 60 seconds). If the switch occurs during peak hours, business stability and continuity may be seriously affected.
To protect your business from being affected by CPU resource shortage, you are recommended to perform business optimization on the instances with high CPU utilization or upgrade the CPU resources. The master/slave switchover in an instance is accompanied by an interruption lasting for just seconds; therefore, for persistent connections, your application should have a reconnection mechanism.

#### Solution
High CPU utilization in MySQL is generally related to the presence of inefficient SQL statements. Therefore, targeted optimization of such statements can work out in most cases.
In MySQL, slow query time (long_query_time) is set to 10s by default. After a performance issue occurs, if no slow query is found, it is recommended to adjust the parameter value to 1s and then observe whether there are slow queries in a business cycle, and if yes, optimize the slow queries accordingly. After the parameter is adjusted, if still no slow queries are found but the CPU utilization remains high, you are recommended to upgrade the CPU configuration so as to improve the overall performance of the database.

### High Memory Utilization
#### Cause
Memory is an important performance parameter for TencentDB for MySQL. It is not uncommon to see the memory utilization reach or even exceed 100% due to the presence of inefficient SQL statements and lack of database optimization.

#### Risk
If your high availability edition MySQL database encounters the above problem, it may even trigger an OOM event which will trigger the master/slave switchover. During the switch, your business will be unavailable for a very short period of time (generally less than 60 seconds). If the switch occurs during peak hours, business stability and continuity may be seriously affected.
To protect your business from being affected by high memory utilization, you are recommended to perform business optimization on the instances with high memory utilization or increase the memory size. The master/slave switch in an instance is accompanied by an interruption lasting for just seconds; therefore, for persistent connections, your application should have a reconnection mechanism.

#### Solution
In MySQL, memory can be roughly divided into two parts: globally shared memory and session-level private memory.
- Shared memory is allocated upon the creation of an instance and shared by all connections.
- Private memory is allocated by the system upon connection to the MySQL server.
In some special SQL statements or field types, cache may be allocated to a single thread repeatedly. Therefore, all OOM exceptions are caused by the private memory of each connection. The risk of high memory utilization can be mitigated by limiting database connections and optimizing inefficient SQL statements. If this doesn't work, you can upgrade the memory configuration so as to improve the overall concurrence and stability of the database. For more information on memory parameters, see [Memory Allocation Issues](https://intl.cloud.tencent.com/document/product/236/31922).

>
>- During the upgrade, your business can operate normally. After the upgrade, there will be a switchover accompanied by an interruption lasting for just seconds. Please make sure that your business has a reconnection mechanism.
>- Currently, you cannot modify the memory parameter in the TencentDB for MySQL Console. If the innodb_buffer_pool_size is set too small, the disk write load may be high which will compromise the overall performance of your database.
>- To protect your business from being affected by insufficient MySQL memory or CPU resources, please configure an appropriate resource alarm policy for your instance. By doing so, you can identify potential resource shortage in advance. For more information, see [Alarming Service](http://intl.cloud.tencent.com/document/product/248/6126).
