Tencent Cloud Elastic MapReduce (EMR) ClickHouse provides cloud-hosted services for ClickHouse, a popular open-source column-oriented database management system (DBMS). With features such as convenient ClickHouse cluster deployment, configuration modification, and monitoring and alarming, it is a secure and stable OLAP solution for both individual and corporate users. Moreover, it has excellent query performance and is therefore ideal for online data query and analysis scenarios.

## ClickHouse Features

### Architecture

ClickHouse is available in single-node, multi-node, and multi-replica architectures for your choice according to your business needs.

### OPS

Out-of--the-box services such as monitoring, log search, and parameter modification are provided in the console.

### Data

EMR ClickHouse has complete data import and export capabilities. You can easily import data from data sources such as COS, HDFS, Kafka, and MySQL to the ClickHouse cluster or vice versa.

## ClickHouse Strengths

### High performance

By giving full play to multi-core concurrency (with the aid of high-efficiency SIMD instruction set and vectorized execution engine) and leveraging distributed technologies and accelerated computing, ClickHouse provides real-time analysis capabilities. As an open-source solution, ClickHouse's benchmark test shows that its processing is 100–1,000 times faster than that of traditional methods, with a 50–200 MB/s high throughput during real-time import.

### Low costs

Based on the well-designed column-oriented storage and efficient data compression algorithm, ClickHouse is an optimal scheme for building large-scale data warehouses, as it provides a compression ratio of up to 1,000%, greatly improving the data storage and computing capabilities of a single server and reducing the use costs.

### Ease of use

- ClickHouse comprehensively supports SQL, so that you can easily get started with it.
- It is compatible with various data types such as JSON, map, and array for quick adaption to ever-changing businesses.
- It supports cutting-edge technologies such as approximation calculation and probabilistic data structure to process massive amounts of data.

## EMR ClickHouse Table Engine Overview

### Table engine purposes

The table engine (i.e., table type) determines the following:
- Data storage method and location, and where to write the data to or read the data from.
- Supported queries and how they are supported.
- Concurrent data access.
- Use of indexes (if any).
- Whether multi-thread requests can be executed.
- Data replication parameters.

### Engine types

#### MergeTree family

`MergeTree` engines are the most universal and powerful table engines for high-load tasks. A common feature among them is quick data insertion with subsequent backend data processing. They support data replication (with Replicated\* versions of engines), partitioning, and some features not supported by other engines.

**Engines in this family:**
- [MergeTree](https://clickhouse.tech/docs/en/operations/table_engines/mergetree/): it is the most powerful table engine in ClickHouse.
- [ReplacingMergeTree](https://clickhouse.tech/docs/en/operations/table_engines/replacingmergetree/): it differs from `MergeTree` in that it removes duplicate entries with the same primary key value.
- [SummingMergeTree](https://clickhouse.tech/docs/en/operations/table_engines/summingmergetree/): it inherits from `MergeTree`. The difference is that when merging data parts for `SummingMergeTree` tables, ClickHouse replaces all the rows with the same primary key with one row which contains summarized values for the columns with the numeric data type. If the primary key is composed in a way that a single key value corresponds to a large number of rows, this significantly reduces storage volume and speeds up data query.
- [AggregatingMergeTree](https://clickhouse.tech/docs/en/operations/table_engines/aggregatingmergetree/): it inherits from `MergeTree` while changing the logic for data parts merging. ClickHouse replaces all rows with the same primary key (within one data part) with a single row that stores a combination of states of aggregate functions.
- [CollapsingMergeTree](https://clickhouse.tech/docs/en/operations/table_engines/collapsingmergetree/): it inherits from `MergeTree` and adds the logic of rows collapsing to data parts merge algorithm.
- [VersionedCollapsingMergeTree](https://clickhouse.tech/docs/en/operations/table_engines/versionedcollapsingmergetree/): as an upgrade from `CollapsingMergeTree`, it uses a different collapsing algorithm that allows inserting data in any order with multiple threads.
- [GraphiteMergeTree](https://clickhouse.tech/docs/en/operations/table_engines/graphitemergetree/): it is used for aggregating Graphite data. It reduces the used storage capacity and increases the efficiency of queries from Graphite.

#### Log family

Log engines are lightweight engines with minimum functionality. They are most effective when you need to quickly write many small tables (up to around 1 million rows) and read them later as a whole.

**Engines in this family:**
- [TinyLog](https://clickhouse.tech/docs/en/operations/table_engines/tinylog/): it is the simplest table engine and is used to store data on disks. Each column is stored in an independent compressed file. During writing, data will be added to the end of the file.
- [StripeLog](https://clickhouse.tech/docs/en/operations/table_engines/stripelog/): it belongs to the family of log engines and can be used in scenarios when you need to write many tables with a small amount of data (less than 1 million rows).
- [Log](https://clickhouse.tech/docs/en/operations/table_engines/log/): it differs from `TinyLog` in that a small file of "marks" resides with the column files. These marks are written on every data block and contain offsets that indicate where to start reading the file in order to skip the specified number of rows. This makes it possible to read table data in multiple threads. For concurrent data access, the read operations can be performed at the same time, while write operations block reads and one another. It does not support indexes. Similarly, if writing to a table failed, the table is broken, and reading from it returns an error. It is appropriate for temporary data, write-once tables, and testing or demonstration purposes. 

#### Integration engines

Integration engines are for integration with other data storage and processing systems.

- [Kafka](https://clickhouse.tech/docs/en/operations/table_engines/kafka/): it works with Apache Kafka.
- [MySQL](https://clickhouse.tech/docs/en/operations/table_engines/mysql/): it allows you to perform `SELECT` queries on data stored on remote MySQL servers.
- [ODBC](https://clickhouse.tech/docs/en/engines/table_engines/integrations/odbc/): it allows ClickHouse to connect to external databases through ODBC.
- [JDBC](https://clickhouse.tech/docs/en/operations/table_engines/jdbc/): it allows ClickHouse to connect to external databases through JDBC.
- [HDFS](https://clickhouse.tech/docs/en/operations/table_engines/hdfs/): it allows ClickHouse to access data on HDFS.

#### Special engines

- [Distributed](https://clickhouse.tech/docs/en/operations/table_engines/distributed/): tables with the Distributed engine do not store any data by themselves but allow distributed queries on multiple servers. Reading is automatically parallelized. During a read, the table indexes on remote servers are used, if there are any.
- [MaterializedView](https://clickhouse.tech/docs/en/operations/table_engines/materializedview/): it is used for implementing materialized views (for more information, please see "CREATE TABLE"). For storing data, it uses a different engine that was specified when the view was created. When reading from a table, it just uses this engine.
- [Dictionary](https://clickhouse.tech/docs/en/operations/table_engines/dictionary/): it displays the dictionary data as a ClickHouse table.
- [Merge](https://clickhouse.tech/docs/en/operations/table_engines/merge/): it (not to be confused with `MergeTree`) does not store data itself but allows reading from any number of other tables at the same time.
- [File](https://clickhouse.tech/docs/en/operations/table_engines/file/): a data source is a file used to store data in one of the file formats supported by ClickHouse (TabSeparated, Native, etc.).
- [Null](https://clickhouse.tech/docs/en/operations/table_engines/null/): when a `Null` table is written to, data is ignored. When a `Null` table is read from, the response is empty. However, you can create a materialized view on a `Null` table, so the data written to the table will be forwarded to the view.
- [Set](https://clickhouse.tech/docs/en/operations/table_engines/set/): it is a data set always in RAM.
- [Join](https://clickhouse.tech/docs/en/operations/table_engines/join/): loaded `Join` table data is permanently retained in the memory.
- [URL](https://clickhouse.tech/docs/en/operations/table_engines/url/): it manages data on a remote HTTP/HTTPS server and is similar to the `File` engine.
- [View](https://clickhouse.tech/docs/en/operations/table_engines/view/): it is used for implementing views (for more information, please see the `CREATE VIEW` query). It does not store data but only stores the specified `SELECT` query. When reading from a table, it runs this query (and deletes all unnecessary columns from the query).
- [Memory](https://clickhouse.tech/docs/en/operations/table_engines/memory/): it stores data in uncompressed form in RAM.
- [Buffer](https://clickhouse.tech/docs/en/operations/table_engines/buffer/): it buffers the data to write into the RAM, periodically flushing it to another table. During the read operation, data is read from the buffer and the other table simultaneously.

### Virtual column

Virtual column is an integral table engine attribute that is defined in the engine source code.

You should not specify virtual columns in the `CREATE TABLE` query and you cannot see them in `SHOW CREATE TABLE` and `DESCRIBE TABLE` query results. Virtual columns are also read-only, so you can't insert data into virtual columns.

To select data from a virtual column, you must specify its name in the `SELECT` query. `SELECT *` does not return values from virtual columns.

If you create a table with a column that has the same name as one of the table virtual columns, the virtual column becomes inaccessible. To help avoid conflicts, virtual column names are usually prefixed with an underscore.
