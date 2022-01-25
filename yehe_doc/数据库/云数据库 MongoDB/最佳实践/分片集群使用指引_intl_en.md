
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

## Choosing Shard Key
The shard key is a field in a document used for routing queries.
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


#### Modifying shard key value
Prior to MongoDB 4.2, the shard key field value of a document cannot be changed.

Starting from MongoDB 4.2, unless the shard key field is an immutable `_id` field, you can update its value in the following methods:

| Command                                                         | Method                                                         |
| --------------------------------------------------- | --------------------------------------------------- |
| [update](https://docs.mongodb.com/manual/reference/command/update/#dbcmd.update) with multi: false | <li>[db.collection.replaceOne()](https://docs.mongodb.com/manual/reference/method/db.collection.replaceOne/#db.collection.replaceOne)  <li>[db.collection.updateOne()](https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/#db.collection.updateOne)  <li>[db.collection.update()](https://docs.mongodb.com/manual/reference/method/db.collection.update/#db.collection.update) with multi: false |
| [findAndModify](https://docs.mongodb.com/manual/reference/command/findAndModify/#dbcmd.findAndModify) | <li>[db.collection.findOneAndReplace()](https://docs.mongodb.com/manual/reference/method/db.collection.findOneAndReplace/#db.collection.findOneAndReplace)<li>[db.collection.findOneAndUpdate()](https://docs.mongodb.com/manual/reference/method/db.collection.findOneAndUpdate/#db.collection.findOneAndUpdate) <li> [db.collection.findAndModify()](https://docs.mongodb.com/manual/reference/method/db.collection.findAndModify/#db.collection.findAndModify) |
|     -                                                         |<li> [db.collection.bulkWrite()](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/#db.collection.bulkWrite)  <li>[Bulk.find.updateOne()](https://docs.mongodb.com/manual/reference/method/Bulk.find.updateOne/#Bulk.find.updateOne)  <br>If the shard key modification causes the document to be moved to another shard, you cannot specify multiple shard keys for batch modification; that is, the batch size must be `1`. <br>Otherwise, you can specify multiple shard keys for batch modification. </br> |

Notes on shard key modification:
- You must perform it in a transaction or on mongos in a retryable write mode. Do not perform it directly on shards.
- You must include an equality condition in the complete shard key of the query filter. For example, if you use `{country:1, userid:1}` as the shard key in a shard collection, to update the document shard key, you must include `country:, userid:` in the query filter. You can also include other fields in the query as needed.


## Balancing and Related Parameters
MongoDB sharded cluster partitions data into chunks. The background process `balancer` monitors the number of chunks on each shard and migrates the chunks between shards to balance the load on each shard server.
>?The system creates an initial chunk, and the chunk size is 64 MB by default.

Because chunk migrations have an impact on cluster read/write performance, you can set the balancing window to avoid the impact during business peak, or run commands to disable balancing.

Commands to manage balancing are described as follows. If you do not have the permission to run the commands, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance.

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

