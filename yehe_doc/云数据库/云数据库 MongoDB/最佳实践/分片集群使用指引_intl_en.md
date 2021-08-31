A sharded cluster is distributed MongoDB database architecture. Compared with replica sets, sharded clusters evenly distribute data across shards, which not only greatly increases the capacity, but also distributes the read/write workload across shards, effectively solving the performance bottleneck of replica sets. The trade off is increased complexity in architecture. This document lists some issues you should take note of when using TencentDB for MongoDB sharded clusters.

## Sharded Cluster Components
A MongoDB sharded cluster consists of the following components:
- shard: each shard contains a subset of the sharded data, and can be deployed as a replica set.
- mongos: the mongos acts as a query router, providing an interface between client applications and the sharded cluster.
- config servers: config servers store metadata and configuration settings for the cluster, including permission and authentication configurations.

## Sharding Strategies and Performance Impact
MongoDB sharded clusters supports 3 sharding strategies for data distribution: ranged sharding, hashed sharding, and zone/tag-based sharding. Each sharding strategy results in different performances when used in different functions.
- **Ranged sharding**
Advantages: good performance in shard key range-based query and read
Disadvantages: possibly uneven data distribution with hot spots
- **Hashed sharding**
Advantages: even data distribution, good write performance, and suitable for high concurrency use cases such as logging and Internet of Things
Disadvantages: low range-based query efficiency
- **Zone/tag-based sharding**
Data which has a natural distinction, such as geographical or time distinction, can be distinguished by tags.
Advantages: good data distribution


## Choosing a Shard Key
The shard key is an indexed field that exists in every document. MongoDB uses it to route and query data across shards. The choice of shard key cannot be changed after sharding.
The choice of shard key can have a great impact on sharding efficiency due to the following factors:

- **Cardinality**
Choose a shard key with high cardinality. A shard key with low cardinality will have a small number of available values, which constrains the maximum number of chunks. As the data increases, the chunk size grows, making it difficult to migrate chunks in horizontal scaling.
For example: if you use age as the cardinality, there will only be at most 100 available shard key values. As data increases, a chunk will soon store too much data and grow beyond the specified chunk size and becoming a jumbo chunk. Such a chunk cannot be migrated, resulting in uneven data distribution and performance bottlenecks.

- **Distribution**
Choose a shard key whose values are distributed evenly; otherwise, some chunks may contain huge volumes of data, which will result in uneven data distribution and performance bottlenecks.
 
- **Shard key-based query**
Use the shard key as the query condition. Mongos can locate the specific shard according to the shard key; otherwise, mongos needs to distribute the query to all shards and wait for their responses.
 
- **Monotonically changing shard keys (not recommended)**
A monotonically increasing shard key leads to fewer migrations of data, but all new inserts are routed to the last chunk which has to keep migrating as it grows. The same problem will occur when a monotonically decreasing shard key is used.

Consider all of the above factors when choosing a shard key to reduce the negative effects of chunk migration and optimize overall performance. 

## Balancing and Related Parameters
MongoDB sharded cluster partitions data into chunks. The background process `balancer` monitors the number of chunks on each shard and migrates the chunks between shards to balance the load on each shard server.
>?The system creates an initial chunk, and the chunk size is 64 MB by default.

Because chunk migrations have an impact on cluster read/write performance, you can set the balancing window to avoid the impact during business peak, or run commands to disable balancing.

Commands to manage balancing are described as follows. If you do not have the permission to run the commands, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance.

- **Checking whether balancing is enabled for MongoDB sharded cluster**
```
mongos> sh.getBalancerState()
true
```
You can also run `sh.status()` to check balancing status.

- **Checking whether there are data in migration**
```
mongos> sh.isBalancerRunning()
false
```

- **Setting the balancing window**
 - Modify the balancing window:
```
db.settings.update(
   { _id: "balancer" },
   { $set: { activeWindow : { start : "<start-time>", stop : "<stop-time>" } } },
   { upsert: true }
)
```

 - Delete the balancing window:
```
use config
db.settings.update({ _id : "balancer" }, { $unset : { activeWindow : true } })
```

- **Disabling balancing**
 - By default, the balancer can migrate a chunk whenever it needs to be migrated. You can run the following commands to disable balancing:
```
sh.stopBalancer()
sh.getBalancerState()
```

 - Run the following commands to query whether a migration process is running after balancing is disabled:
```
use config
while( sh.isBalancerRunning() ) {
          print("waiting...");
          sleep(1000);
}
```

- **Enabling balancing**
 - Run the following command to enable balancing again:
```
sh.setBalancerState(true)
```

 - When the driver does not support `sh.startBalancer()`, run the following commands to enable balancing again:
```
use config
db.settings.update( { _id: "balancer" }, { $set : { stopped: false } } , { upsert: true } )
```


- **Balancing on a collection**
 - Disable balancing on a collection:
```
sh.disableBalancing("students.grades")
```

 - Enable balancing on a collection:
```
sh.enableBalancing("students.grades")
```

 - Check whether balancing is enabled on a collection:
```
db.getSiblingDB("config").collections.findOne({_id : "students.grades"}).noBalance
```

