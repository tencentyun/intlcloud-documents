### Overview of Sharded Cluster
TencentDB for MongoDB now features sharding. Sharding is a method that partitions data by key ranges and distributes the data across multiple machines. Its horizontal scaling makes it well suited for TB/PB-level data storage. Additionally, sharded cluster supports instance-level backup and rollback to ensure data durability, and shards adopts multi-node automatic disaster recovery mechanism to make sure services are available and reliable. You can leverage the sharding feature of TencentDB for MongoDB to easily and efficiently build massive distributed storage system.


### Creating a Sharding Cluster
Enter the MongoDB [purchase page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharding Cluster**, and select the number of shards, the number of nodes in each shard, and node specification based on your needs. Each shard is a replica set containing multiple nodes. Therefore, shards use multi-node automatic disaster recovery mechanism to support high service availability. 
[![](https://mc.qcloudimg.com/static/img/6fb80892b40e93cbcc19cb43d2d70b80/goumaiye.png)](https://mc.qcloudimg.com/static/img/6fb80892b40e93cbcc19cb43d2d70b80/goumaiye.png)

### Sharded Cluster Console
In the console, you can view detailed components of the sharded cluster instance, such as the composition of the shard, the specifications of the shard node and used capacity. You can also manage (renew, pay, etc.)  the instance as well as increase instance capacity.
[![](https://mc.qcloudimg.com/static/img/6cabd8fbb7652a85648fe454b243d365/k2.png)](https://mc.qcloudimg.com/static/img/6cabd8fbb7652a85648fe454b243d365/k2.png)

### Increasing Sharded Cluster Capacity
You can only increase TencentDB for MongoDB sharded cluster capacity by expanding, instead of adding, nodes. Click the **Expand** button on the instance list page, specify the targeted capacity and click **Upgrade**.
[![](https://mc.qcloudimg.com/static/img/e723c37c10c076c03e2836dbdeec7b80/%7BADB18884-AB90-4475-B309-83F334A26A1E%7D.png)](https://mc.qcloudimg.com/static/img/e723c37c10c076c03e2836dbdeec7b80/%7BADB18884-AB90-4475-B309-83F334A26A1E%7D.png)

### Backing up and Restoring a Sharded Cluster Instance 
Backup and restore operations in sharded cluster instances are the same as that in replica set instances. You can only back up and restore the data at instance level. Click the **Backup** on the instance details page, enter remark information, and then click **Submit**.
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
You need to enter a date to which you want to roll the instance back. You can enter any point in time between two backups (when the instance is successfully backed up while oplog space is not fully occupied) within the past 5 days. If you instance does not satisfy the conditions above, please back it up manually.
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

### Monitoring a Sharded Cluster Instance
You can monitor your TencentDB for MongoDB sharded cluster at three levels: instance, shard and node. Information about operation requests, capacity usage, load, etc., is provided.
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)

