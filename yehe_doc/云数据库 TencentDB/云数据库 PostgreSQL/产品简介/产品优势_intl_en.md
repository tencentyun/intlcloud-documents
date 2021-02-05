## More Powerful
Over the past few years, PostgreSQL has become the preferred open source relational database for businesses.

- Follows the BSD protocol, which means there are no restrictions on using PostgreSQL.
- Supports most of the programming languages such as C, C++, Java, PHP, Python and Perl, thus making the development of your business applications easier and faster.
- PostgreSQL is the closest open source database to Oracle in terms of architecture, syntax and data types.
- It is compatible with SQL standard "SQL 2003", and supports the main features of SQL 2011.
- In addition to the traditional SQL LIKE operator, it also supports the new SIMILAR TO operator of SQL 99 and POSIX-style regular expressions.
- Rich data types: geometry, network address, XML, JSON, RANGE, Array, etc.
- Supports complex types (custom data types).
- Supports complex multi-table join SQL query, and join algorithms are supported such as hash join, merge join, etc.
- Supports window functions or complex analytic functions as the latter ones include window functions.
- Supports function index, partial (row) index, custom index and full-text index.
- Thanks to its multi-process architecture, it is more stable, and a high-throughput database can be implemented on a single machine.
- Includes powerful, high-performance built-in plug-ins, such as PostGIS, which is a database extension for geo-spatial data and provides additional support for geography location objects, allowing you to run location queries with SQL.
- Has strong data consistency required for commercial use. With synchronous replication, PostgreSQL guarantees zero data loss, and even suitable for financial trading systems.


## High performance

High-performance databases that can be used in OLAP or OLTP scenarios. 
 - Provides query optimizers comparable to commercial databases. It also supports common multi-table join query (such as nested loop, hash join, sort merge join, etc.). For example, the performance of joining two tables, each with 100000 rows, is 100 times faster than that of MySQL. With the capability of obtaining query results faster from more tables, you can make your analysis more accurate. 
 - Built on NVMe SSD storage, with QPS as high as 230000. You can support more concurrent business requests with fewer databases. 
 - Supports a large number of performance profiles. You can view performance data such as the running SQL queries, current lock waits, table scan and index scan to help you quickly and accurately locate the performance problems.
 - Tencent Cloud improves the performance of built-in operators by optimizing the PostgreSQL kernel, and provides super high performance NVMe SSD with QPS configuration at least 10 times higher than SATA. TencentDB for PostgreSQL uses one-primary-one-secondary architecture for deployment by default. Synchronous replication is enabled by default, protecting your business from being interrupted and preventing problems such as data corruption and data loss.

## Ease of Management

Tencent Cloud allows you to connect to Launch's PostgreSQL instance and connect to the application in a few minutes without the need for other configuration. The default configuration has universal parameters, and can be modified in real time in Console parameter settings. Help you get rid of the heavy and complex installation and configuration process and improve your OPS efficiency.

## Convenient monitoring

Provides key operation Metric of PostgreSQL, including performance monitoring data such as CPU utilization, storage capacity utilization, and IPostgreSQL O activities, which you can view in Console without extra charge to help you quickly locate and solve problems. Customize the Metric alarm threshold. You don't need to pay attention to monitoring all the time, but you can keep abreast of the current exception via email or SMS.

## Scalable

You can upgrade to the target specification with one click through Tencent Cloud and Console without the need for additional operations. The upgraded instance inherits the IP and all configurations of the original instance. During the upgrade process, only a flash break occurs in the switching process, without long downtime, to meet the needs of business elasticity at any time. If the existing PostgreSQL is still unable to carry your business development, it can support a large number of users with unlimited capacity and no bottlenecks with only a few changes or no changes to the business.

## High security

After the node failure, the cluster scheduling will start to automatically retry the Resume node immediately. When there is a serious problem with your data, you can quickly Resume to a normal point in time to deal with upgrade failures, disasters, Resume and other situations. By default, cloud databases provide multiple security protection for each database, and you can own them without having to purchase them separately.
