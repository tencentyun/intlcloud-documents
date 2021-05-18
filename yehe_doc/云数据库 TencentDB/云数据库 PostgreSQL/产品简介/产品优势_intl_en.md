
## Powerful Features
Over the recent years, PostgreSQL has become the go-to open-source relational database for commercial use.

- PostgreSQL is released under a BSD-style license, which means there are no restrictions on using PostgreSQL.
- PostgreSQL supports C, C++, Java, PHP, Python, Perl and so on, making the development of your business easier and faster.
- PostgreSQL is the best open-source alternative to Oracle in terms of architecture, syntax and data types.
- PostgreSQL is compatible with the SQL standard SQL2003 and supports the main features of SQL2011.
- PostgreSQL supports the traditional SQL LIKE operator, the more recent SQL99 SIMILAR TO operator, and POSIX-style regular expressions.
- PostgreSQL supports rich data types including geometry, network address, XML, JSON, RANGE, array, etc.
- PostgreSQL supports complex types (custom data types).
- PostgreSQL supports complex multi-table joins and join algorithms such as hash joins, merge joins, etc.
- PostgreSQL supports window functions or complex analytic functions (the latter include window functions).
- PostgreSQL supports function indexes, partial (row) indexes, custom indexes, and full-text indexes.
- PostgreSQL features a multi-process architecture that makes it more stable, and even a standalone PostgreSQL database can achieve a high throughput.
- PostgreSQL supports powerful, high-performance extensions. For example, PostGIS is a database extension for geo-spatial data and provides additional support for geographic objects, allowing you to run location queries with SQL.
- PostgreSQL provides strong data consistency required for commercial use. With synchronous replication, PostgreSQL guarantees zero data loss, and is even suitable for financial trading systems.

## High Performance
PostgreSQL achieves high performance in OLAP or OLTP scenarios.
- PostgreSQL provides query optimizers comparable to those of commercial databases. It also supports common multi-table join queries (such as nested loop joins, hash joins, sort-merge joins, etc.). For example, the performance of joining two tables, each with 100,000 rows, is 100 times faster than that of MySQL. With the capability of obtaining query results faster from more tables, you can make your analysis more accurate.
- PostgreSQL uses NVMe SSDs as the storage media with a QPS as high as 230,000. You can support more concurrent business requests with fewer databases.
- PostgreSQL supports a large number of performance profiles. You can view performance data such as the ongoing SQL queries, current lock waits, table scans, and index scans to help you quickly and accurately locate the performance problems.
- TencentDB for PostgreSQL improves the performance of built-in operators by optimizing the PostgreSQL kernel, and provides a QPS at least 10 times that of SATA by using super-high-performance NVMe SSDs. It features a primary/standby deployment mode and enables sync replication by default; this enables you to avoid business interruptions and problems such as data corruption and loss.

## Convenient Management
You can launch a TencentDB for PostgreSQL instance and connect it to applications in minutes with no additional configuration required. The default configuration has universal parameters that can be modified at any time in the console. This eliminates laborious and complicated installation and configuration processes and improves your OPS efficiency.

## Convenient Monitoring
TencentDB for PostgreSQL provides key operational metrics for PostgreSQL databases for free, including performance monitoring data such as CPU utilization, storage utilization, and I/O. You can view them in the console to quickly locate and resolve issues. In addition, customizable metric alarms are also available to allow you to stay on top of exceptions via email and SMS without needing to monitor your databases round the clock.

## Strong Scalability
TencentDB for PostgreSQL instances can be scaled in the Tencent Cloud console to meet your elastic business needs with no additional configuration needed. The scaling process won't change the IPs and settings of the original instances, and your business will be interrupted just for a second. If the existing instances cannot sustain your business, their capacity can be easily expanded to serve more end users with minor or no changes made to your business.

## High Availability
The cluster scheduler of TencentDB for PostgreSQL will automatically restore a node when it fails to a previous point in time for failover and disaster recovery. Moreover, it provides multiple default layers of security protection for each database that does not need to be purchased separately.


