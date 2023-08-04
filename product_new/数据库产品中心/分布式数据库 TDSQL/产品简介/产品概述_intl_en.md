## Overview
TDSQL for MySQL is a distributed database service deployed in Tencent Cloud that supports automatic sharding (horizontal splitting) and the Shared Nothing architecture. With a distributed database, your business obtains a complete logical database table which is split and distributed evenly across multiple physical shard nodes on the backend. TDSQL deploys the master-slave architecture by default and provides a full set of solutions for disaster recovery, backup, restoration, monitoring, and migration, making it ideal for storing terabytes to petabytes of data.

## Features
#### OLTP
TDSQL is a distributed database for OLTP businesses.

#### Sharding
TDSQL is a distributed database that supports sharding.

Sharding is to spread the data of a table into multiple independent physical database servers according to a defined rule to form an "independent" database "shard". Multiple shards together form a logically complete database instance.

#### Shared Nothing architecture
The traditional solution uses minicomputers and shared storage, which is more expensive and prone to capacity and performance bottlenecks. TDSQL adopts the Shared Nothing architecture, with each node computing and storing a portion of data. Therefore, no matter how quickly your business grows, you just need to keep adding servers in the distributed cluster to meet the growing computing and storage needs.
![](https://main.qcloudimg.com/raw/280276ed738586bc34b959c38346d01a.png)

#### Data splitting methods (sharding rules)
In principle, TDSQL uses a sharding scheme based on automatic horizontal splitting. Specifically, a modulo operation is executed on the shardkey, and then data is distributed into different databases through TProxy according to the specific range of values after modulo operation.

A relational database is a two-dimensional model. To shard data, it is usually necessary to find a **shardkey field** to determine the sharding dimension. Then, a rule needs to be defined to actually shard the database.

**Below are some common shardkey options:**
- Based on date order, such as sharding by year (one shard for 2015 and another for 2016).
	- Advantages: Simple and easy to find.
	- Disadvantages: The server performance for the current (e.g., 2016) hot data may be insufficient, while the storage performance for cold data is idle.
	
- Based on user ID modulo, where fields in the specific range after modulo operation are spread across different databases.
	- Advantages: The performance is relatively balanced and all data of the same user is in the same database.
	- Disadvantages: This may lead to data skew (for example, when a merchant system is designed, one merchant's data in an ecommerce mall may be more than that of thousands of small merchants).
	
- Based on primary key modulo, where fields in the specific range after modulo operation are spread across different databases.
	- Advantages: The performance is relatively balanced, data skew seldom occurs, and all data of the same primary key is in the same database.
	- Disadvantages: Data is randomly distributed, and some business logics may require cross-shard join that is not supported directly.

**Before sharding multiple tables, the following options are available:**
- Noshard: No sharding.
-tableshard: When each table is sharded, select shardkeys arbitrarily for sharding based on the actual needs regardless of inter-table relationships.
- groupshard: A few correlated tables are designed based on the same shardkey, so that the related data can be aggregated into one physical node.

**In terms of sharded data source management, there are currently two modes:**
- Client mode: The data sources of multiple shards are managed by the configuration in the business program module, and the reading, writing, and data integration of the shards are performed within the business program.
- Middleware proxy mode: A middleware proxy is built on the frontend of the sharding databases which are imperceptible to the frontend application.


## Problems TDSQL Can Help You Solve
### Performance bottlenecks in standalone databases
Faced with millions of users of the internet-based business, a standalone database will reach bottlenecks in data storage capacity, access capacity, and disaster recovery due to hardware and software limitations as the business grows.

### Heavy workload for application-layer sharding development
Application-layer sharding highly couples business logic with database logic, which incurs heavy development workload over rapid iteration of the current business. Based on the imperceptible sharding scheme of TDSQL, your developers only need to modify the code during initial access without having to care much about the database logic during subsequent iterations, which can greatly reduce the development workload.

### Problems with open-source solutions or NoSQL
Choosing open-source or NoSQL solutions can also break through database bottlenecks at no or relatively low costs. However, you need to pay attention to the following issues with such solutions:
1. Bug fixing of a product depends on the progress in the community. Can you wait if you encounter a serious bug?
2. Are there members in your team who are familiar with the product and can continuously maintain it without affecting the project in case of staffing changes?
3. Is the associated system ready?
4. What business do you focus on? Does your business metric system involve inputting resources to ensure the open-source product's resource and lifecycle management, distributed logic, high-availability deployment and switchover, disaster recovery and backup, self-service OPS, and troubleshooting?
