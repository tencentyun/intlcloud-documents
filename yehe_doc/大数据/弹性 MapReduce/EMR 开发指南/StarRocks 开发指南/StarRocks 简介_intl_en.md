## StarRocks Overview
- StarRocks is a new-gen super fast MPP database for nearly all data analysis scenarios.
- StarRocks leverages the strengths of relational Online Analytical Processing (OLAP) databases and distributed storage systems. Through architectural upgrades and functional optimizations, it has been developed into an enterprise-level product.
- StarRocks is committed to creating a super fast and unified analysis experience to meet your needs in diversified data analysis scenarios. It supports multiple data models (detail, aggregation, and update) and various data import methods (batch and streaming) for up to 10,000 columns of data. It can be integrated with and connected to different existing systems, such as Spark, Flink, Hive, and Elasticsearch.
- StarRocks is compatible with the MySQL protocol, so you can use the MySQL client and common BI tools to connect to it for data analysis.
- StarRocks uses a distributed architecture to shard data tables horizontally and store them in multiple replicas. The cluster is elastically scalable and supports 10 PB-level data analysis, MPP frameworks, concurrently accelerated computing, multi-replica, and elastic fault tolerance.
- StarRocks adopts a relational model, strong data typing, and columnar storage engine, which help reduce read-write amplification through encoding and compression technologies. It uses vectorized query execution to fully unleash the power of parallel computing on multi-core CPUs and greatly improve the query performance.

## StarRocks Features
StarRocks integrates the design ideas of MPP databases and distributed systems into its architecture and has the following features:
### Simplified architecture
StarRocks performs the specific execution of SQL through the MPP computing framework. The framework itself can make full use of the computing power of multiple nodes and execute the entire query in parallel, so as to deliver an excellent interactive analysis experience. StarRocks does not rely on any external systems. Its simple architecture makes it easier to deploy, maintain, and scale out. Its minimalist architectural design reduces its complexity and maintenance cost and increases its reliability and scalability. Admins only need to focus on the StarRocks system itself, with no need to learn and manage other external systems.

### Native vectorized SQL engine
The computing layer of StarRocks fully adopts the vectorization technology to systematically optimize all operators, functions, scanning, filtering, and import and export modules. Through the columnar memory layout and the SIMD instruction set adapted to CPU, it makes full use of the parallel computing power of CPU, achieving sub-second query returns in multidimensional analyses.

### Query optimization
StarRocks can optimize complex queries through cost-based optimizer (CBO). The execution costs can be reasonably estimated based on the statistical information with no human intervention required. With a better execution plan, the data analysis efficiency in ad hoc and ETL scenarios can be greatly improved.

### Query federation
StarRocks enables you to perform federated queries by using external tables. Currently, it supports tables from Hive, MySQL, and Elasticsearch. In this way, you can quickly query data without importing data.

### Efficient update
StarRocks supports multiple data models. Among them, the update model can perform UPSERT/DELETE operations according to the primary key and achieve efficient query during concurrent updates through storage and indexing optimization. This better serves real-time data warehouses.
### Smart materialized view
StarRocks supports smart materialized views. You can create views and generate preaggregated tables to speed up aggregate queries. Such views automatically run the aggregation when data is imported, keeping it consistent with the original table. When querying, you don't need to specify a materialized view, because StarRocks can automatically select the best one to satisfy the query.
### Standard SQL
StarRocks supports standard SQL syntax, including aggregation, join, sorting, window functions, and custom functions. It also fully supports 22 SQL queries from TPC-H and 99 SQL queries from TPC-DS. In addition, it is compatible with the MySQL protocol, so you can use various existing client tools and BI software programs to access StarRocks and perform data analysis with simple drag-and-drops in StarRocks.
### Unified batch processing and streaming
StarRocks supports batch and streaming import of up to 10,000 columns of data in ORC, Parquet, and CSV formats from Kafka, HDFS, and local files. It can consume real-time Kafka data to import the data, which avoids data loss or duplication (i.e., exactly once). It can also import data in batches from local or remote (HDFS) data sources.
### High availability and scalability
StarRocks metadata and data are stored in multiple replicas. A StarRocks cluster provides hot standby services and can be deployed as multiple instances, eliminating single points of failure. It has the ability of self-healing and elastic recovery. Therefore, the overall stability of the cluster service will not be affected by node failures, disconnections, or exceptions. StarRocks adopts a distributed architecture that makes possible to horizontally scale the storage capacity and computing power. Specifically, a cluster can be expanded to hundreds of nodes to support up to 10 PB data storage. It can normally provide the query service during scaling. In addition, the table schema of StarRocks supports hot changes, so you can use a simple SQL command to dynamically modify the table definition, for example, adding or deleting a column or creating a materialized view. You can also import data into or query data from tables during schema changes.

## Use Cases
StarRocks can meet a variety of analysis needs, including OLAP analysis, custom reporting, real-time data analysis, and ad hoc data analysis. Specific business scenarios include:
- Multidimensional OLAP. User behavior analysis.
	- User profiling, tag analysis, and user tagging.
	- High-dimensional business metric reporting.
	- Self-service reporting.
	- Business problem identification and analysis.
	- Cross-topic business analysis.
	- Financial reporting.
	- System monitoring analysis.
- Real-time data analysis. Ecommerce promotion data analysis.
	- Education live streaming quality analysis.
	- Waybill analysis.
	- Finance performance analysis and metric calculation.
	- Ad placement analysis.
	- Management cockpit.
	- Application performance management (APM).
- High-concurrency queries. Advertiser report analysis.
	- Retail channel personnel analysis.
	- User-oriented analysis reporting in the SaaS industry.
	- Multi-page dashboard analysis.
- Unified analysis. The same system is used to address the needs in different scenarios, such as multidimensional analysis, high-concurrency queries, precomputing, real-time analysis, and ad hoc query, simplifying the system and reducing the cost of multi-technology stack development and maintenance.

