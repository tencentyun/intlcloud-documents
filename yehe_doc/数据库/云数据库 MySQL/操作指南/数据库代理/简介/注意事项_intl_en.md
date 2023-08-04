This document describes the use limits for the TencentDB for MySQL database proxy.

- When using the proxy connection address, if you don't enable transaction split, transaction requests will be routed to the source instance.

- The database proxy supports cross-AZ configuration. The number of selectable AZs depends on how many AZs are available in the current region. You can select up to three AZs. If only one AZ can be selected, there is only one available AZ in the region.

- You can create multiple database proxy addresses, the number of which is the same as that of proxy nodes.

- When a proxy connection address is used to implement read/write separation, the consistency of non-transactional reads is not guaranteed. If your business requires read consistency, you can encapsulate it into transactions or use the hint syntax.

- When a proxy connection address is used, `show processlist` will merge the results of all nodes before returning them.

- For the `PREPARE` statement, the database proxy will first send `PREPARE` to all nodes. When a subsequent `EXECUTE` request comes in, it will determine the execution route according to the prepared statement type. For example, if a write statement is prepared, it will send the statement to the source database during execution, and if a non-transactional read statement is prepared, it will send the statement to a read-only instance.

 - After a business connection arrives at the database proxy, the proxy will connect to the source instance and all configured read-only instances. The proxy itself does not have a limit on the maximum number of connections, which is mainly subject to the maximum number of connections of the backend database instance. The smallest value of this parameter of the source and read-only instances will affect the business performance.

- After the database proxy is enabled, when a read-only instance is added or restarted, only new connection requests will be routed to it. You can view the performance metrics of each proxy node through the overview or performance monitoring as described in [Viewing Database Proxy Monitoring Data](https://www.tencentcloud.com/document/product/236/42055). If you find that the numbers of connections on the nodes are unbalanced, you can distribute the connections through rebalancing.

- Versions supported for different database proxy capabilities:
 - Cross-AZ configuration: Proxy v1.3.1 or later.
 - Connection persistence timeout: Proxy v1.2.1 or later.
 - Connection pool: Proxy v1.2.1 or later.
 - Transaction split: Proxy v1.3.1 or later.
 - Connection address adding: Proxy v1.3.1 or later.
 >?For more information on how to upgrade the proxy, see [Upgrading Kernel Minor Version of Database Proxy](https://www.tencentcloud.com/document/product/236/45627).

