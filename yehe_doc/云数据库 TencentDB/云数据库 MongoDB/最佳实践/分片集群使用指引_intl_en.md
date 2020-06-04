The sharded cluster is distributed MongoDB. Compared with replica sets, the sharded cluster has a more complex architecture, and can evenly distribute data across shards. It not only greatly increases the upper limit of the data capacity of the whole cluster, but also disperses the read/write pressure to shards, thus solving the performance bottleneck of replica sets. This document lists the precautions for using TencentDB for MongoDB sharded cluster.

## Sharded Cluster Components
A MongoDB sharded cluster consists of all the following components:
- shard: each shard contains a subset of the sharded data, and can be deployed as a replica set.
- mongos: the mongos acts as a query router, providing an interface between client applications and the sharded cluster.
- config servers: config servers store metadata and configuration settings for the cluster, including permission and authentication configurations.

## Sharding Strategies and Performance Impact
MongoDB sharded cluster supports 3 sharding strategies for distributing data: ranged sharding, hashed sharding, and zone/tag-based sharding. A sharding strategy will have different effects on performance when used in different businesses.
- **Ranged sharding**
Advantages: good performance in shard key range-based query and read
Disadvantages: possibly uneven data distribution with hot spots
- **Hashed sharding**
Advantages: even data distribution, good write performance, and suitable for high concurrency scenarios such as logging and Internet of Things
Disadvantages: low range-based query efficiency
- **Zone/tag-based sharding**
Data which has a natural distinction, such as geographical or time distinction, can be distinguished by tags.
Advantages: good data distribution


## Choosing a Shard Key
The shard key is an indexed field that exists in every document. MongoDB uses it to route and query data across shards. The choice of shard key cannot be changed after sharding.
The choice of shard key can have a great impact on sharding efficiency due to the following factors:

- **Cardinality**
Choose a shard key with high cardinality. A shard key with low cardinality means inadequate number of available values, which constrains the maximum number of chunks. As the data increases, the chunk size grows, making it difficult to migrate chunks in horizontal scaling.
For example: if you use age as the cardinality, there are only up to 100 available shard key values. With the increase of data, a chunk will store too much data of the same shard key value, growing beyond the specified chunk size and becoming a jumbo chunk. Such a chunk cannot be migrated, resulting in uneven data distribution and performance bottlenecks.

- **Distribution**
Choose a shard key whose values are distributed evenly; otherwise, some chunks may contain huge volumes of data, also resulting in uneven data distribution and performance bottlenecks.
 
- **Shard key-based query**
Use the shard key as the query condition. Mongos can locate the specific shard according to the shard key; otherwise, mongos needs to distribute the query to all shards and wait for their responses.
 
- **Monotonically changing shard keys not recommended**
A monotonically increasing shard key leads to fewer migrations of data, but all new inserts are routed to the last chunk which has to keep migrating as it grows. The same problem will occur when a monotonically decreasing shard key is used.

Therefore, consider each factor when choosing a shard key. A shard key that satisfies the conditions above as many as possible can reduce the performance impact of chunk migration and get the best performance experience.

## Balancing and Related Parameters
MongoDB sharded cluster partitions data into chunks. The background process `balancer` manages the creation and migration of chunks to balance the load on each shard server.
>The system creates an initial chunk, and the chunk size is 64 MB by default.

Because chunk migrations have an impact on cluster read/write performance, you can set the balancing window to avoid the impact during business peak, or run commands to disable balancing.

Commands to manage balancing are described as follows. If you do not have the permission to run the commands, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance.

- **Checking whether balancing is enabled for MongoDB sharded cluster**
```
mongos> sh.getBalancerState()
true
```
You can also run `sh.status()` to check balancing status.

- **Checking whether data is migrating**
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

