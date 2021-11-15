
## Overview
TencentDB for CTSDB (CTSDB) is Tencent Cloud's proprietary distributed and scalable time series database that supports near real-time data search and analysis. It is a non-relational database and provides efficient read/write, cost-effective storage, powerful aggregate analysis capabilities, and convenient features such as instance monitoring and data query result visualization. Its entire system adopts a multi-node multi-replica deployment architecture, effectively ensuring high service availability and data reliability.

## Strengths
CTSDB has the following strengths in processing massive amounts of time series data:
 - Highly concurrent writes: CTSDB adopts the policy where data is written into the memory first and then periodically dumped as immutable files for storage. It can also write data in bulk to reduce network overheads.
 - Cost-Effective storage: CTSDB aggregates historical data through data rollup to save storage space. Plus, it uses appropriate encoding and compression algorithms to increase the data compression ratio.
 - Powerful aggregate analysis capabilities: CTSDB not only supports basic aggregate analysis functions such as Min, Max, Sum, and Avg but also supports complex ones such as Group By, Interval, Geo, and Nesting.

## Service Architecture
#### Cluster without master nodes
![](https://main.qcloudimg.com/raw/a9dfb160f503484ddaafbe8083dfc8f6.png)
A cluster without master nodes is a distributed cluster consisting of multiple data nodes.

- All data nodes receive external requests, interconnect and collaborate with each other to provide services such as data storage and indexing (client requests can be distributed to appropriate nodes), and are master-eligible.
- You won't need dedicated master nodes if your cluster has less than 30 nodes, because the cluster without master nodes will suffice.
>?You can add dedicated master nodes to a CTSDB cluster to upgrade it from the cluster without master nodes to the one with master nodes.

#### Cluster with master nodes
![](https://main.qcloudimg.com/raw/7f773d8cd79f2af937f066b32584e5d9.png)
A cluster with master nodes is a distributed cluster consisting of dedicated master-eligible nodes and data nodes.
- The dedicated master nodes are responsible for guaranteeing the health and stability of the entire cluster and doesn't provide services such as data storage. Data nodes provide services such as data storage and indexing.
- As the business grows and the data volume increases, when the number of nodes exceeds 30, we recommend you add dedicated master nodes to upgrade the cluster without master nodes to the one with master nodes, so as to fully exert the performance of the large multi-node cluster.
>?A CTSDB cluster with master nodes added cannot be changed back to the one without any.

