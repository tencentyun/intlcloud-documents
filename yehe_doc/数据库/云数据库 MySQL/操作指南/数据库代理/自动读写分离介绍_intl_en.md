This document describes the automatic read/write separation feature of the database proxy service in TencentDB for MySQL and its strengths and routing rules.

## [Automatic Read/Write Separation](id:zddxfl)
Currently, businesses of many users in the production environment have problems such as more reads and less writes and unpredictable business loads. In application scenarios with a large number of read requests, a single instance may not be able to withstand the pressure of read requests, which even may affect the businesses. To implement the auto scaling of read capabilities and mitigate the pressure on the database, you can create one or multiple read-only instances and use them to sustain high numbers of database reads. However, this solution requires that businesses can be transformed to support read/write separation, and the code robustness determines the quality of business read/write separation, which imposes high technical requirements and has low flexibility and scalability.

Therefore, after creating a read-only instance, you can purchase a database proxy, enable read/write separation, and configure the database proxy address in your application so as to automatically forward write requests to the source instance and read requests to the read-only instance. In addition, this method provides natural solutions to other business challenges as detailed below:
- **Applications with unpredictable workloads**
Applications supporting highly variable workloads may try to open new database connections to handle traffic surges. Connection management in the dedicated database proxy allows you to appropriately scale applications that process unpredictable workloads by effectively reusing database connections.
First, this feature allows multiple application connections to share the same database connection to effectively use database resources. Second, it allows you to adjust the number of open database connections to maintain a predictable database performance. Third, it allows you to delete unusable application requests to guarantee the overall application performance and availability.

- **Applications frequently opening/closing database connections**
Applications built based on technologies such as serverless, PHP, or Ruby on Rails may frequently open and close database connections to process application requests.
The dedicated database proxy can help you maintain a database connection pool to prevent unnecessary pressure on data computing and the memory used to establish new connections.

- **Applications with open but idle connections**
SaaS applications and traditional ecommerce applications may make database connections idle to minimize the response time when users reconnect. You can use the dedicated database proxy to retain idle connections and establish database connections for active requests as needed instead of excessively increasing the threshold or providing database services with higher specifications to support most idle connections.

- **Applications requiring highly smooth failover**
With the dedicated database proxy, you can build applications that can tolerate active and passive database failures in an imperceptible manner with no need to write complex failure processing code. The dedicated database proxy will automatically route read traffic to new database instances while retaining the application connections.

![](https://main.qcloudimg.com/raw/a5f23e2235bc918b1a7e816c8f2c947b.png)

## Strengths
- Read/Write requests are automatically separated with a unified access address.
- Native linkage support improves the performance and reduces the maintenance costs.
- You can flexibly set weights and thresholds.
- Failover is supported, so that even if the database proxy fails, requests can access the source database normally.
- If the source instance is switched, has configuration adjustment, or has read-only instances added or removed, the database proxy can dynamically hot load the configuration without causing network disconnections or restarts.

## Read/Write Separation Routing Rules
### Sending to source instance
- DDL statements such as `CREATE`, `ALTER`, `DROP`, and `RENAME`.
- DML statements such as `INSERT`, `UPDATE`, and `DELETE`.
- `SELECT FOR UPDATE` statement.
- Statements related to temp tables.
- Certain system function calls (such as `last_insert_id()`) and all custom function calls.
- Statements related to `LOCK`.
- Statements after transaction is enabled (including `set autocommit=0`)
- Stored procedures.
- Multiple statements concatenated by ";".
- `KILL` (SQL statement, not command)
- All queries and changes of user variables.

### Sending to read-only instance
- Read (`SELECT`) statements outside transactions.

### Sending to all instances
- `show processlist` statement.
- All changes of system variables (`SET` command).
- `USE` command.
