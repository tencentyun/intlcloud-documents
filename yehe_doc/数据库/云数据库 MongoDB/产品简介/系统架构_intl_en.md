
## Replica Set
The replica set architecture of TencentDB for MongoDB achieves high availability by deploying multiple servers to store data replicas. Each replica set instance consists of one primary node and one or more secondary nodes.

- Primary node: it is responsible for processing client read and write requests. There can be only one primary node in each replica set instance.
- Secondary node: it replicates the data of the primary node by periodically polling the oplogs of the primary node with data consistency guaranteed. When the original primary node fails, a new primary node will be elected from multiple secondary nodes to ensure the high availability.

The architecture diagram of a replica set instance is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/b736f3db997ed56b7609889d78460ad6.png)

Replica set 4.0 simplifies the architecture by removing the proxy set component, so you can directly access each node for a higher performance:
![](https://qcloudimg.tencent-cloud.cn/raw/57826733ce38e14c866697e8d80f89e9.png)

## Sharded Cluster
TencentDB for MongoDB's sharded cluster architecture implements the horizontal capacity expansion of data based on the replica set architecture by combining multiple replica sets. Each sharded cluster instance is composed of mongos nodes, config server nodes, shard nodes, and other components.

- **mongos node**: it is responsible for receiving connection query requests from all client applications, routing the requests to the corresponding shards in the cluster, and splicing the received responses back to the clients. You can purchase multiple mongos nodes to achieve load balancing and failover. Each sharded cluster instance can contain 3–48 mongos nodes.

- **Config server node**: it is responsible for storing the metadata of the cluster and shard nodes, such as the cluster node information and routing information of sharded data. A config server node has a fixed specification of 1 CPU core, 2 GB memory, and 20 GB disk space in the form of 3-replica set by default, which cannot be modified. 

- **Shard node**: it is responsible for sharding data storage on multiple servers. You can purchase multiple shard nodes to horizontally expand the data storage and read/write concurrency capabilities of the instance. Each sharded cluster instance can contain 2–20 shard nodes.

![](https://qcloudimg.tencent-cloud.cn/raw/0a2a9805fccb368b431acfb7e66ed300.png)

## Single Node
Single-Node TencentDB for MongoDB is a cost-effective database service, whose operating costs are only one-third as many as the cluster MongoDB while ensuring good performance. It is suitable for learning, testing, and the businesses where the requirement for availability is not high, such as internal systems, and mini programs or applications of individual developers.
>?
>- Currently, the single-node architecture only supports MongoDB v4.0.
>- Currently, the single-node architecture does not support backup or rollback. If you have a high requirement for data reliability, purchase other architectures.
>- Currently, the single-node architecture does not support slow log query or connection management.
>- In the single-node architecture, only the primary node is retained, so high-availability services cannot be provided, and the [SLA](https://intl.cloud.tencent.com/document/product/301/30977) cannot be guaranteed.
>- The single-node architecture supports only one type of specification (1 core, 2 GB memory, and 150 GB disk capacity), which cannot be changed.
>- Currently, the single-node TencentDB for MongoDB can be purchased in the following zones: Guangzhou Zone 3, Shanghai Zone 4, Beijing Zone 4, and Chengdu Zone 1.
