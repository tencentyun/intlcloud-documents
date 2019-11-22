
### Does TencentDB for MongoDB support sharding?
Yes. For more information, see [Creating a Sharding Cluster](https://intl.cloud.tencent.com/document/product/240/8333).

### What is a MongoDB sharded cluster?
Sharded clusters are available on TencentDB for MongoDB.
- Sharded clusters distributively store data in multiple physical machines according to the shard key. Their great scalability, therefore, makes them very suitable for storing TB or PB level data.
- Sharded clusters support instance-level backup and rollback to ensure data reliability; The multi-node automatic disaster recovery is enabled for each shard to ensure high service availability.
- Using TencentDB for MongoDB sharding, you can easily and efficiently build a large-scale distributed storage system.

### How do I create a MongoDB sharded cluster?
Log in to [MongoDB Purchase Page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharded Cluster** in **Instance Type**, and select the number of shards, the number of nodes in each shard, and node specification based on your needs.
Since each shard is a replica set with multiple nodes, the multi-node auto disaster recovery is enabled to ensure service availability.

### How do I query the information of a MongoDB sharded cluster?
In the [console](https://console.cloud.tencent.com/mongodb), you can view detailed information of the sharded cluster instance, such as the shard composition, shard node specifications and used capacity, as well as perform operations including instance [capacity expansion](https://intl.cloud.tencent.com/document/product/240/31192).

### How do I expand the capacity of a MongoDB sharded cluster?
You can expand the capacity only by expanding all nodes at the same time. Adding nodes is not supported.
On the [console](https://console.cloud.tencent.com/mongodb), click the **Expand** on the instance list page, select the desired capacity, and click **Upgrade**.

### How do I monitor data in a MongoDB sharded cluster instance?
You can monitor the data of the TencentDB for MongoDB sharded cluster in three dimensions:
- Instance
- Shard
- Node

You can view the monitoring report in the **System Monitoring** page of an instance, from which you will see various indicators, including operation requests, capacity usage, and load.

### What is the MongoDB sharding policy?
- A sharding mechanism that supports hash key.
- The shard key is indexed compound fields.
- Sharding is required for all data sets in a sharding instance. It is recommended to place non-sharded data in a separate replica set instance.

### What is the authentication mechanism for MongoDB?
MongoDB fully supports SCRAM-SHA-1 and MongoDB-CR.

### What sharded cluster commands are supported by MongoDB?
For more information, see [Supported Sharded Cluster Commands](https://intl.cloud.tencent.com/document/product/240/8334).

