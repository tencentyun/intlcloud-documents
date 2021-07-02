TDSQL-A for PostgreSQL is Tencent's proprietary distributed analytic database system based on a shared-nothing architecture. It is compatible with SQL:2011 standards, PostgreSQL syntax, and Oracle syntax. Its proprietary column storage engine supports row storage and column storage as well as hybrid storage with a high compression ratio. Its new-generation vectorized execution engine can provide high-performance and efficient real-time query and analysis capabilities for massive amounts of data.
In addition, as a competitive enterprise-grade data warehouse service, TDSQL-A for PostgreSQL supports complete distributed transaction processing, multi-level disaster recovery, and multidimensional resource isolation and provides a powerful multi-level security system, auto scaling capabilities, and comprehensive enterprise-grade management capabilities. It offers a complete set of solutions covering disaster recovery, backup and restoration, monitoring, security, and audit, making it ideal for online analytical processing (OLAP) scenarios containing gigabytes to petabytes of data.

## Features
### Hybrid row/column storage
To better provide OLAP capabilities, on the basis of compatibility with row storage of the PostgreSQL ecosystem, TDSQL-A for PostgreSQL uses a proprietary column storage engine to provide complete column storage capabilities. You can select an appropriate storage format for the data to be written to the database based on your actual business needs so as to enjoy efficient hybrid row/column query capabilities.
Column storage provides powerful compression capabilities, including transparent compression and lightweight compression. The former supports compression algorithms such as zlib and zstd, and the latter supports delta, RLE, and bitpack algorithms. The algorithms can be automatically adjusted and optimized according to the data characteristics for more efficient compression with a compression ratio of up to 400:1.

### Efficient processing of complex queries
The proprietary new-generation vectorized execution engine of TDSQL-A for PostgreSQL has efficient processing capabilities for complex queries. It can return results for trillions of correlated subqueries within seconds, with a performance several times to even hundreds of times higher than that of open-source and traditional data warehouses. 

### Smooth business migration
TDSQL-A for PostgreSQL is compatible with SQL:2011 syntax specifications, PostgreSQL syntax, and Oracle syntax and is equipped with the Tencent DBbridge migration tool, helping you migrate your business system to TDSQL-A for PostgreSQL as smoothly as possible.

### Enterprise-Grade data security
TDSQL-A for PostgreSQL has a permission division mechanism of three roles (security admin, audit admin, and data admin) and provides multi-level policies such as data storage encryption, data masking, forced access control, and data audit to ensure data security comprehensively.

### Complete distributed transactions
TDSQL-A for PostgreSQL has complete transaction ACID capabilities to guarantee the global transaction consistency. It uses GTM to manage distributed transactions and uses the proprietary patented distributed transaction consistency technology to ensure the data consistency and efficiency in the distributed architecture.

### Rich ecosystem support
TDSQL-A for PostgreSQL has a comprehensive peripheral ecosystem:
- It supports powerful geographic information system (GIS). The clusterized PostGIS extension makes it a spatial database that can store spatial and geographic data and support efficient spatial data management, quantitative measurement, and geometric topology analysis through SQL statements.
- It not only is a distributed relational database but also supports JSON, a non-relational data type.
- It supports the foreign data wrapper (FDW) feature, which implements a part of the SQL/MED specifications and allows you to access data that resides outside PostgreSQL by using regular SQL queries.
The FDW feature provides a set of programming APIs, with which you can perform extension-based secondary development and establish a data channel between external data sources and databases. In most cases, you can use `oracle_fdw`, `mysql_fdw`, `postgres_fdw`, `redis_fdw` and `mongodb_fdw` of non-relational databases, and `hive_fdw` and `hdfs_fdw` of big data databases. Based on FDW and existing extensions, TDSQL-A for PostgreSQL provides powerful database federation capabilities, enabling you to access data from multiple existing data sources.
- It offers data migration and sync services and tools to help you easily sync source data in different deployment modes to it, such as Tencent Cloud, self-built database, and other cloud databases. The high stability and performance of this sync feature ensure an integrated data experience. 
