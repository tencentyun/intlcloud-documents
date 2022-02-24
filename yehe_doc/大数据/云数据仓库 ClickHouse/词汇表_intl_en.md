### High Availability
High availability (HA) is a service attribute of a Cloud Data Warehouse cluster and is enabled by default.
- If HA is enabled, the Cloud Data Warehouse cluster consists of an even number of (at least two) ClickHouse Server nodes and three ZooKeeper nodes, with data of a single server stored on two or more servers to ensure redundancy and service continuity in case of replica failures.
- If HA is disabled, the Cloud Data Warehouse cluster consists of one or more ClickHouse Server nodes and one ZooKeeper node. In this setup, data is stored in only one replica, so when a replica becomes unavailable, the entire cluster will fail.

### Shard
Cloud Data Warehouse stores massive amounts of data on multiple nodes, each of which only stores and processes a part of the data. Each node is called a shard.

### Replica
A replica is used to guarantee service HA. In Cloud Data Warehouse's replica mechanism, data of a single node is stored on two or more nodes in a redundant manner.	
### Table	
A table is the way of data organization, consisting of multiple rows and columns. Cloud Data Warehouse tables can be local or distributed in terms of data distribution and can be non-replicated or replicated in terms of storage engine.	

### Local Table	
The data in a local table is stored only on the node where it is currently written to.	

### Distributed Table	
A distributed table abstracts multiple local tables into one with write and query features. When you write data to a distributed table, the data will be automatically distributed to the local tables it contains; when you query data in it, all its local tables will be queried to return an aggregated result. You can leverage the storage and computing resources of multiple servers for writes and queries in a distributed table and perform on-demand horizontal scaling.	

### Non-Replicated Table	
The data in a non-replicated table is stored only on the current node but not replicated to other nodes.	

### Replicated Table	
The data in a replicated table is automatically replicated to multiple nodes to create multiple replicas. As long as one replica is normal, the service of the replicated table will not be interrupted.	
