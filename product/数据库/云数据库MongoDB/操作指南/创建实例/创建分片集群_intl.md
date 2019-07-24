### Overview of Sharded Cluster
TencentDB for MongoDB now features sharding. Sharding is a method that partitions data by key ranges and distributes the data across multiple machines. Its horizontal scaling makes it well suited for TB/PB-level data storage. Additionally, sharded cluster supports instance-level backup and rollback to ensure data durability, and shards adopts multi-node automatic disaster recovery mechanism to make sure services are available and reliable. You can leverage the sharding feature of TencentDB for MongoDB to easily and efficiently build massive distributed storage system.


### Creating a Sharding Cluster
Enter the MongoDB [purchase page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharding Cluster**, and select the number of shards, the number of nodes in each shard, and node specification based on your needs. Each shard is a replica set containing multiple nodes. Therefore, shards use multi-node automatic disaster recovery mechanism to support high service availability. 
![](https://main.qcloudimg.com/raw/43ba7d1e09eb8b5938773fd678f7c641.png)

### Sharded Cluster Console
In the console, you can view detailed components of the sharded cluster instance, such as the composition of the shard, the specifications of the shard node and used capacity. You can also manage (renew, pay, etc.)  the instance as well as increase instance capacity.
![](https://main.qcloudimg.com/raw/8bfc2cb0389a2a0994faac75f24a13b3.png)

### Increasing Sharded Cluster Capacity
You can only increase TencentDB for MongoDB sharded cluster capacity by expanding instead of adding nodes. Click the **Expand** button on the instance list page, specify the targeted capacity and click **Upgrade**.
![](https://main.qcloudimg.com/raw/2063c5b70eab9173eb2a9357e235a1be.png)

### Backing up and Restoring a Sharded Cluster Instance 
Backup and restore operations in sharded cluster instances are the same as that in replica set instances. You can only back up and restore the data at instance level. Click the **Backup** on the instance details page, enter remark information, and then click **Submit**.
![](https://main.qcloudimg.com/raw/e9d332b812295f4e94e63d490589d066.png)
You need to enter a date to which you want to roll the instance back. You can enter any point in time between two backups (when the instance is successfully backed up while oplog space is not fully occupied) within the past 5 days. If you instance does not satisfy the conditions above, please back it up manually.
![](https://main.qcloudimg.com/raw/99545980a00cb7c8a4bc34351bb6efbf.png)

### Monitoring a Sharded Cluster Instance
You can monitor your TencentDB for MongoDB sharded cluster at three levels: instance, shard and node. Information about operation requests, capacity usage, load, etc., is provided.
![](https://main.qcloudimg.com/raw/7f1957c3dbdf9b71959cf5494718b949.png)

