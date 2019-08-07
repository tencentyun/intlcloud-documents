### DynamoDB Cluster Overview
DynamoDB is a fully managed proprietary NoSQL service which supports document and key-value data structures and provides fast, predictable and scalable performance. Based on existing NoSQL module framework, Tencent Cloud adds DynamoDB-compatible protocols. Now DynamoDB is compatible with most basic protocols to meet database access requirements. Additionally, it supports instance-level backup and rollback, as well as automatic disaster recovery mechanism data services. You can access Tencent Cloud database via DynamoDB protocols with minimum code modification if you are a DynamoDB developer.


### Creating a DynamoDB Cluster
Enter the MongoDB [purchase page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharded Cluster**, and select **DynamoDB protocol** as the protocol type.
Sharding distributes data across multiple machines to scale horizontally. You need to specify number of shards, nodes in each shard, and desired specifications for each node. Each shard is a replica set containing multiple nodes, and shards use multi-node automatic disaster recovery mechanism to make sure services are available.
[![](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)

### DynamoDB Cluster Console
In the console, you can view detailed components of your Dynamo cluster instance, such as the composition of the shard, the specifications of the shard node and used capacity. You can also manage (renew, pay, etc.)  the instance as well as increase instance capacity.
[![](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)

### Increasing DynamoDB Cluster Capacity
You can only increase TencentDB for MongoDB sharded cluster capacity by expanding instead of adding nodes. Click the **Expand** button on the instance list page, specify the targeted capacity and click **Upgrade**.
[![](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)

### Backing up and Restoring a DynamoDB Cluster Instance 
Backup and restore operations in sharded cluster instances are the same as that in replica set instances. You can only back up and restore the data at instance level. Click the **Backup** on the instance details page, enter remark information, and click **Submit**.
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
You need to enter a date to which you want to roll the instance back. You can enter any point in time between two backups (when the instance is successfully backed up while oplog space is not fully occupied) within the past 5 days. If you instance does not satisfy the conditions above, please back it up manually.
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

### Monitoring a DynamoDB Cluster Instance
You can monitor your DynamoDB cluster at three levels: instance, shard, and node. Information about operation requests, capacity usage, load, etc., is provided.
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)

