
### Does TencentDB for MongoDB support sharding?
Yes. For more information, see [Creating a Sharding Cluster](https://cloud.tencent.com/document/product/240/8333).

### What is a MongoDB sharding cluster?
TencentDB for MongoDB provides sharding clusters.
- These sharding clusters distributively store data in multiple physical machines according to sharding keys. The clusters have smooth scalability and are very suitable for scenarios where TBs or PBs of data is stored.
- Sharding clusters support instance-level backup and rollback, to ensure high data reliability. Multi-node automatic disaster recovery mechanism is used in each shard to ensure high service availability.
- You can leverage the sharding feature of TencentDB for MongoDB to build a massive distributed storage system easily and efficiently.

### How do I create a MongoDB sharding cluster?
Log in to [MongoDB Purchase Page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharding Cluster** in **Instance Type**, and select the number of shards, the number of nodes in each shard, and node specification, according to your needs.
Each shard is a replica set containing multiple nodes. Multi-node automatic disaster recovery mechanism is used in each shard to ensure high service availability.

### How do I query the information of a MongoDB sharding cluster?
In the [console](https://console.cloud.tencent.com/mongodb), you can view detailed information of the sharding cluster instance, such as the composition of the shard, the specifications of the shard node and occupied capacity, as well as perform operations including instance [renewal management](https://cloud.tencent.com/document/product/240/3552) and [capacity expansion](https://cloud.tencent.com/document/product/240/19911).

### How do I expand the capacity of a MongoDB sharding cluster?
You can only expand the capacity by expanding all nodes. Expanding by adding nodes is not supported.
In the [console](https://console.cloud.tencent.com/mongodb), click the **Expand** button on the instance list page, select the target capacity you wish to expand to, and click **Upgrade**.

### How do I monitor data in a MongoDB sharding cluster instance?
Monitoring metrics of three dimensions are provided to monitor data in the entire TencentDB for MongoDB sharding cluster:
 - Instance
 - Shard
 - Node

You can view the monitoring data of multiple metrics, such as operation requests, capacity usage and load, in the **System Monitoring** page of an instance.

### What are the sharding policies for MongoDB?
- Hash key sharding mechanism is supported.
- You can combine the shard keys of fields.
- Sharding is required for all data sets under a sharding instance. It is recommended to place non-sharded data in a separate replica set instance.

### What is the verification mechanism of MongoDB shards?
MongoDB is fully compatible with two mechanisms: SCRAM-SHA-1 and MONGODB-CR.

### What are the sharding cluster commands supported by MongoDB?
 For more information, see [Supported Sharding Cluster Commands](https://cloud.tencent.com/document/product/240/8334).
 


