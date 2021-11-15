
## Overview
TencentDB for MongoDB is a high-performance distributed data storage service created by Tencent Cloud based on MongoDB, the open source non-relational database. It is fully compatible with MongoDB protocol, and applicable to non-relational database-oriented scenarios.

>?MongoDB® is a registered trademark of MongoDB, Inc. TencentDB for MongoDB is not authorized by or affiliated with MongoDB, Inc. Tencent's use of MongoDB software is based on open-source licenses.



## Features
- It provides cloud storage service, which is the data storage service provided for the Internet applications by Tencent Cloud platform.
- It is fully compatible with MongoDB protocol, and suitable for scenarios with traditional table structure, cache, non-relational data, as well as parallel large-scale data set computation using MapReduce.
- It provides a high-performance, reliable, easy-to-use, and convenient MongoDB cluster service. Each instance is at least a one-primary-two-secondary replica set or a sharded cluster that contains multiple replica sets.
- It is integrated with backup, capacity expansion and other features to ensure user data security and dynamic scalability to the largest extent.

## Instance Types
### Replica set instance
In TencentDB for MongoDB, a replica set is a cluster that contains a primary node and one or more secondary nodes. Data is synced between clusters through replication, which creates redundant backups on multiple servers, improving data availability and ensuring data security.
The architecture diagram of a replica set instance is as follows:
![](https://main.qcloudimg.com/raw/a711f69354ab4c61295b5dbe1edb57a9.png)
Replica set v4.0 is different from other versions in architecture. It has no proxy set component, so you can directly access each node:
![](https://main.qcloudimg.com/raw/ae87f544b36226d0081ef8e11299b7a4.png)

### Sharded cluster instance
In TencentDB for MongoDB, a sharded cluster consists of components such as shards, proxy sets, and config servers. Each shard contains a subset of sharded data and is deployed as a replica set.

Sharded clusters support horizontal expansion of data based on a combination of multiple replica sets. The components in a sharded cluster are described as follows:
- **mongos**: the mongos acts as a query router, which receives connections and query requests from the client applications and routes them to shards in the cluster. A cluster can contain one or more mongos.
- **config server**: the config server provides configuration service. It stores metadata information of the cluster, such as sharding information or user information.
- **shard**: each shard contains a subset of sharded data and the shards are stored on multiple servers.
Currently, the mongos and config servers are free of charge, so you only need to pay for the shards.

![](https://main.qcloudimg.com/raw/89564dc17533c57719f23ad78316e471.png)

### Single-node instance
Single-node TencentDB for MongoDB is a cost-effective database service, whose operating costs are only one-third as many as the cluster MongoDB while ensuring good performance. It is suitable for learning, testing, and the businesses where the requirement for availability is not high, such as internal systems, and mini programs or applications of individual developers.
>?
>- Currently, the single-node architecture only supports MongoDB v4.0.
>- Currently, the single-node architecture does not support backup or rollback. If you have a high requirement for data reliability, please purchase other architectures.
>- Currently, the single-node architecture does not support slow log query or connection management.
>- The single-node architecture only has the primary node, so it does not support high availability.
>- The single-node architecture supports only one type of specification (1 core, 2 GB memory, and 150 GB disk capacity), which cannot be changed.
>- Currently, the single-node TencentDB for MongoDB can be purchased in the following zones: Guangzhou Zone 3, Shanghai Zone 4, Beijing Zone 4, and Chengdu Zone 1.
