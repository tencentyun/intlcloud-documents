TDSQL for MySQL is highly compatible with MySQL protocols and syntax. However, due to architectural differences, TDSQL has certain restrictions on SQL. In order to better take advantage of the distributed architecture, we recommend that you follow the suggestions below.

The TDSQL instance is capable of horizontal scaling, making it suitable for scenarios with massive amounts of data. Its features are described as follows:
- Supports flexible read/write separation
- Supports global operations including ORDER BY, GROUP BY, and LIMIT
- Supports aggregate functions including SUM, COUNT, AVG, MIN, and MAX
- Supports cross-node (set) join operations and subqueries
- Supports pre-processing protocols
- Supports the global unique field and sequence
- Supports distributed transactions
- Supports two-level partitioning
- Provides specific SQL statements for querying configuration and status of the entire cluster


The TDSQL instance supports three different types of tables:
- **Sharded table**: this is a horizontally sharded table. It is a complete logical table from the business perspective, but the backend distributes the data to different node sets according to the hash value of the shardkey.
- **Non-sharded table**: this is also known as a noshard table, which does not need to be specifically sharded or processed. Currently, the TDSQL instance stores this type of table in the first physical node set by default.
- **Broadcast table**: this is based on small table broadcasting technology. After a table is set as a broadcast table, all operations of the table will be broadcast to all node sets, where each set has all the data of the table. This is often used as a configuration table of a business system.

>!
>- In a TDSQL instance, if two tables have the same **shardkey**, the rows corresponding to the same shardkey in the two tables are definitely stored in the same physical node set. This type of scenario is often called groupshard, which greatly improves the processing efficiency of statements such as join queries.
>- Since non-sharded tables are placed on the first set by default, if a large number of non-sharded tables are created in a TDSQL instance, the load of the first set will be too high.
>- In most cases, we recommend that you create sharded tables in a TDSQL instance.

