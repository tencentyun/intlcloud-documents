
### Does TencentDB for MongoDB support sharding?
Yes. For more information, see [Creating Sharded Cluster](https://intl.cloud.tencent.com/document/product/240/8333).

### What is a MongoDB sharded cluster?
TencentDB for MongoDB provides sharded clusters.
- These sharded clusters distributively store data in multiple physical machines according to the shard key. Their great scalability, therefore, makes them very suitable for storing TB- or PB-level data.
- Sharded clusters support instance-level backup and Rollback to ensure high data reliability. Multi-node automatic disaster recovery mechanism is used in each shard to ensure high service availability.
- You can leverage the sharding feature of TencentDB for MongoDB to build a massive distributed storage system easily and efficiently.

### How do I create a MongoDB sharded cluster?
Log in to the [TencentDB for MongoDB purchase page](https://buy.intl.cloud.tencent.com/mongodb?clusterType=1), click **Sharded Cluster** in **Instance Type**, and select the number of shards, the number of nodes in each shard, and node specification, according to your needs.
Each shard is a replica set containing multiple nodes. Multi-node automatic disaster recovery mechanism is used in each shard to ensure high service availability.

### How do I query the information of a MongoDB sharded cluster?
In the [console](https://console.cloud.tencent.com/mongodb/sharding), you can view detailed information of the sharded cluster instance, such as the shard composition, shard node specifications and used capacity, as well as perform operations including instance management and [capacity expansion](https://intl.cloud.tencent.com/document/product/240/31192).

### How do I expand the capacity of a MongoDB sharded cluster?
You can expand the capacity only by expanding all nodes at the same time. Adding nodes is not supported.
In the [console](https://console.cloud.tencent.com/mongodb/sharding), click **Adjust Configuration** on the instance list page and select the desired capacity.

### How do I monitor data in a MongoDB sharded cluster instance?
You can monitor the data of the TencentDB for MongoDB sharded cluster in 3 dimensions:
 - Instance
 - Shard
 - Node

You can view the monitoring report on the **System Monitoring** page of an instance, from which you will see various metrics, including operation requests, capacity usage, and load.

### What is the MongoDB sharding policy?
- The sharding mechanism supports hash key.
- The shard key is indexed compound fields.
- Sharding is required for all data sets in a shard instance. It is recommended to store non-sharded data in a separate replica set instance.

### What is the authentication mechanism for MongoDB shards?
MongoDB is fully compatible with SCRAM-SHA-1 and MONGODB-CR.

### What sharded cluster commands are supported by MongoDB?
 For more information, see [Supported Sharded Cluster Commands](https://intl.cloud.tencent.com/document/product/240/8334).


