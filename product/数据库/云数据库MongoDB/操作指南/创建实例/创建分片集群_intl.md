### Sharded cluster Overview
Sharding is now available on TencentDB for MongoDB that allows you to build a massive distributed storage system easily and efficiently. Sharding is a method that partitions data by key ranges and distributes the data across multiple machines. Sharding enables horizontal scaling, so sharded clusters are very suitable for storing TB/PB-level data sets. In addition, sharded cluster supports instance-level backup and rollback, which ensures data durability. Each shard uses Multi-node automatic disaster recovery mechanism to support high service availability. 


### Creating a sharding cluster
Enter the MongoDB [purchase page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharding Cluster**, and select the number of shards, the number of nodes in each shard, and node specification, according to your needs. Each shard is a replica set containing multiple nodes, and it uses Multi-node automatic disaster recovery mechanism to support high service availability. 
[![](https://mc.qcloudimg.com/static/img/6fb80892b40e93cbcc19cb43d2d70b80/goumaiye.png)](https://mc.qcloudimg.com/static/img/6fb80892b40e93cbcc19cb43d2d70b80/goumaiye.png)

### Sharded Cluster Console
In the console, you can view detailed components of the sharded cluster instance, such as the composition of the shard, the specifications of the shard node and used capacity. You can also manage (renew, pay, etc.)  the instance as well as increase instance capacity.
[![](https://mc.qcloudimg.com/static/img/6cabd8fbb7652a85648fe454b243d365/k2.png)](https://mc.qcloudimg.com/static/img/6cabd8fbb7652a85648fe454b243d365/k2.png)

### Increasing sharded cluster capacity
You can only increaseTencentDB for MongoDB sharded cluster capacity by expanding all nodes. Expanding by adding nodes is not supported. Click the **Expand** button on the instance list page, specify the targeted capacity and click **Upgrade**.
[![](https://mc.qcloudimg.com/static/img/e723c37c10c076c03e2836dbdeec7b80/%7BADB18884-AB90-4475-B309-83F334A26A1E%7D.png)](https://mc.qcloudimg.com/static/img/e723c37c10c076c03e2836dbdeec7b80/%7BADB18884-AB90-4475-B309-83F334A26A1E%7D.png)

### Backing up and restoring a sharded cluster instance 
Backup and restore operations in sharded cluster instances are the same as that in replica set instances. You can only back up and restore the data at the instance level. Click the **Backup** button in the instance details page, enter remark information, and then click **Submit**.
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
You need to enter a date to which you want to roll the instance back. You can enter any point in time between two backups (the instance is successful backed up while oplog space is not fully occupied) within the past 5 days. If you instance is not satisfy the conditions above, please back it up manually.
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

### Monitoring a sharded cluster instance 
You can monitor your TencentDB for MongoDB sharded cluster at three levels: instance, shard and node. Information such as operation requests, capacity usage and load is provided.
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)

