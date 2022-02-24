The table engine (i.e., table type) determines the following:
- Data storage method and location, and where to write the data to or read the data from
- Supported queries and how they are supported
- Concurrent data access
- Use of indexes (if any)
- Whether multi-threaded requests can be executed
- Data replication parameters

## Engine Type
### MergeTree
`MergeTree` engines are the most universal and powerful table engines for high-load tasks. A common feature among them is quick data insertion with subsequent backend data processing. They support data replication (with `Replicated*` versions of engines), partitioning, and some features not supported by other engines.

Engines in this family:
- MergeTree
- ReplacingMergeTree
- SummingMergeTree
- AggregatingMergeTree
- CollapsingMergeTree
- VersionedCollapsingMergeTree
- GraphiteMergeTree

### Log
Log engines are lightweight engines with minimum functionality. They are most effective when you need to quickly write many small tables (up to around 1 million rows) and read them later as a whole.

Engines in this family:
- TinyLog
- StripeLog
- Log

### Integration engine 
Integration engines are for integration with other data storage and processing systems.

Engines in this family:
- Kafka
- MySQL
- ODBC
- JDBC
- HDFS

### Special engines 
Engines in this family:
- Distributed
- MaterializedView
- Dictionary
- Merge
- File
- Null
- Set
- Join
- URL
- View
- Memory
- Buffer

## Virtual Column
- Virtual column is an integral table engine attribute that is defined in the engine source code.
- You should not specify virtual columns in the `CREATE TABLE` query and you cannot see them in `SHOW CREATE TABLE` and `DESCRIBE TABLE` query results. Virtual columns are also read-only, so you can't insert data into virtual columns.
- To select data from a virtual column, you must specify its name in the `SELECT` query. `SELECT *` does not return data from virtual columns.
- If you create a table with a column that has the same name as one of the table virtual columns, the virtual column becomes inaccessible. To help avoid conflicts, virtual column names are usually prefixed with an underscore.
