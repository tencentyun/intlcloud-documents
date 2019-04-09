### DynamoDB Cluster Overview
AWS DynamoDB is a fully managed proprietary NoSQL service that supports document and key-value data structures and provides fast, predictable performance at any scale. Based on the existing NoSQL module framework, Tencent Cloud adds protocol-compatibility to AWS DynamoDB database service. Now DynamoDB is compatible with most basic protocols to meet database access requirements. Also, it supports instance-level backup and rollback, and automatic disaster recovery mechanism to ensure high reliability and availability of the service. As a DynamoDB developer, you can access Tencent Cloud Database via the DynamoDB protocol with minimum modification needed.


### Creating a DynamoDB Cluster
Enter the MongoDB [purchase page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharding Cluster**, and select **DynamoDB protocol** as the protocol type.
Because DynamoDB uses sharding, a database architecture for distributing data across multiple machines, to scale horizontally, you need to specify how many shards and nodes in each shard, as well as select the desired specification for each node. Each shard is a replica set containing multiple nodes. Therefore, shards use multi-node automatic disaster recovery mechanism to support high service availability.
[![](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)

### DynamoDB Cluster Console
In the console, you can view detailed components of your Dynamo cluster instance, such as the composition of the shard, the specifications of the shard node and used capacity. You can also manage (renew, pay, etc.)  the instance as well as increase instance capacity.
[![](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)

### Increasing DynamoDB Cluster Capacity
You can only increaseTencentDB for MongoDB sharded cluster capacity by expanding, instead of adding, nodes. Click the **Expand** button on the instance list page, specify the targeted capacity and click **Upgrade**.
[![](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)

### Backing up and Restoring a DynamoDB Cluster Instance 
Backup and restore operations in sharded cluster instances are the same as that in replica set instances. You can only back up and restore the data at instance level. Click the **Backup** on the instance details page, enter remark information, and then click **Submit**.
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
You need to enter a date to which you want to roll the instance back. You can enter any point in time between two backups (when the instance is successfully backed up while oplog space is not fully occupied) within the past 5 days. If you instance does not satisfy the conditions above, please back it up manually.
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

### Monitoring a DynamoDB Cluster Instance
You can monitor your DynamoDB cluster at three levels: instance, shard, and node. Information about operation requests, capacity usage, load, etc., is provided.
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)

