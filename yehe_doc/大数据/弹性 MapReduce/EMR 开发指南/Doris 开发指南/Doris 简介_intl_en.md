Tencent Cloud EMR-Doris provides the cloud semi-hosting service of Doris, which is an MPP analytical database product. It features convenient Doris cluster deployment, configuration modification, monitoring and alarming, etc. Doris is compatible with the MySQL protocol, uses the standard SQL language, and supports highly concurrent queries on PB-scale data, making it suitable for offline data analysis, real-time data analysis, interactive data analysis, exploratory data analysis, and more.

## Features
### MySQL protocol compatibility
Doris provides a connection API compatible with the MySQL protocol. Users can directly use MySQL libraries or tools without the need to deploy new client libraries or tools separately. It also provides MySQL APIs for compatibility with upper-layer applications. All this reduces the learning costs and makes it easy to get started.

### High throughput
The MPP architecture allows the concurrent execution of queries on multiple nodes in a distributed manner, making full use of the overall compute resources of clusters and improving the throughput for large queries.

### High concurrence
Leveraging technologies such as partition pruning, pre-aggregation, predicate pushdown, vectorized execution, and asynchronous RPC, Doris supports highly concurrent query scenarios.

### Data update
Doris supports deleting and updating data by the primary key, making it easy to synchronize real-time data from transactional databases such as MySQL.

### High availability and reliability
Doris use three-replica storage for both data and metadata by default (three or more replicas for BE nodes). This ensures data reliability even when a small number of nodes are down. Doris will automatically identify and repair corrupted data, and route query requests to healthy nodes, ensuring data availability on a 24/7 basis.

### Horizontal scaling and data balancing
Both frontend (FE) nodes and backend (BE) nodes can be scaled horizontally. You can flexibly increase nodes based on compute and storage needs. After BE nodes are added, Doris will automatically balance the data partitions according to the load of the nodes without manual intervention.

### Materialized views and pre-aggregation engine
Doris supports storing the results of data pre-aggregation and compute in the form of materialized views or rollups, thereby improving the query efficiency of some aggregation scenarios. Doris also guarantees the data consistency between materialized views and underlying tables, making queries and imports via materialized views completely transparent. Doris automatically selects the appropriate materialized views for data ingestion based on your query statements.

### Efficient column-oriented storage engine
Doris uses proprietary column-oriented storage formats to improve the query efficiency in the OLAP field. Coupled with the characteristics of column-oriented storage, it adopts various encoding methods such as dictionary encoding and RLE for storage to provide a high data compression ratio and help save storage space. Meanwhile, it uses technologies such as smart min/max index, sparse index, Bloom filter, and bitmap inverted index to improve query efficiency.

### Online table structure modification
You can modify the table structure after data is imported, including adding columns, deleting columns, modifying column types, and changing the column order. These operations will not affect the current database queries and writes.

## Scenarios
### Big data analysis and statistics
There are mainly two types of data analysis scenarios: report analysis and multi-dimensional analysis.

### Report analysis
For report analysis scenarios, data analysis and query modes are relatively fixed, and the backend SQL mode is definite. In such cases, you are advised to use MySQL to store result data. You can choose to execute batch processing and send emails. In the Doris platform, the latency of a report query is generally within one second.

### Multi-dimensional analysis
Multi-dimensional analysis requires data to be structured and is suitable for scenarios where queries are relatively flexible, for example, data analysis criteria and aggregation dimensions are not definite.
![](https://main.qcloudimg.com/raw/0a06ad799372b6c7cde7d0b0ccb3eca5.png)

## Structure
Doris has three major components:
- FE refers to the frontend nodes of Doris, which are mainly responsible for receiving client requests and returning results, managing metadata and clusters, and generating query plans.
- BE refers to the backend nodes of Doris, which are mainly responsible for storing and managing data, and executing query plans.
- Broker is an optional process in a Doris cluster, which are mainly used to read and write files and directories on remote storage systems or services, such as HDFS and Tencent Cloud COS.

![](https://main.qcloudimg.com/raw/789b86faea8ee495d9470f402b115dcc.png)
 
