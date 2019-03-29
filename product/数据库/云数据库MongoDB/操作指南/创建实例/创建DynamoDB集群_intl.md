### Introduction to DynamoDB cluster
DynamoDB is a table-based and highly scalable NoSQL database service that supports document and key-value storage models. Based on the existing NoSQL module framework, Tencent Cloud's database team launches a new database service which provides high compatibility with DynamoDB protocol, fast and stable performance, instance-level backup and rollback, and automatic disaster recovery mechanism. If you are a DynamoDB development enthusiast, you can access databases through the DynamoDB protocol without many code modifications.


### Create a DynamoDB cluster
Enter the MongoDB [purchase page](https://buy.cloud.tencent.com/mongodb?clusterType=1), click **Sharding Cluster**, and select **DynamoDB protocol** as the protocol type.
As the smooth expansion of underlying storage capacity is also achieved by distributing the data across multiple physical machines, you also need to select the number of shards, the number of nodes in each shard, and node specification, according to your needs. Each shard is a replica set containing multiple nodes. Multi-node automatic disaster recovery mechanism is used in each shard to ensure high service availability.
[![](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)

### Console
In the console, you can view detailed information of the DynamoDB cluster instance, such as the composition of the node, the specifications of the node and occupied capacity, as well as perform operations including instance renewal management and capacity expansion.
[![](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)

### Capacity expansion
You can only expand DynamoDB cluster by expanding all nodes. Expanding by adding nodes is not supported. Click the **Expand** button on the instance list page, select the target capacity you wish to expand to and click **Upgrade**.
[![](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)


### Backup and rollback
You can only back up and roll back data at the instance level. Click **Backup** in the instance details page, and enter remark information, and then click **Submit** to commence instance backup.
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
You need to enter a date to which you want to roll the instance back. You can enter any time point within the past 5 days, but you can only select a time between two backups. If there is no backup to satisfy this condition, please perform manual backup.
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

### Instance monitoring
Monitoring metrics of three dimensions are provided to monitor data in the entire sharding cluster: the instance dimension, the shard dimension and the node dimension. Monitoring data of multiple metrics will be provided, such as operation requests, capacity usage, load, etc.
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)

