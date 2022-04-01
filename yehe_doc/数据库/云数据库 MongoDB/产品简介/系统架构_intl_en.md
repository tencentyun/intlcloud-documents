
## Replica Set
The replica set architecture of TencentDB for MongoDB achieves high availability by deploying multiple servers to store data replicas. Each replica set instance consists of one primary node and one or more secondary nodes.

- Primary node: it is responsible for processing client read and write requests. There can be only one primary node in each replica set instance.
- Secondary node: it replicates the data of the primary node by periodically polling the oplogs of the primary node with data consistency guaranteed. When the original primary node fails, a new primary node will be elected from multiple secondary nodes to ensure the high availability.

The architecture diagram of a replica set instance is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/bc1c6b6c2ce9fd2be557ccdda1a00172.png)

Replica set 4.0 simplifies the architecture by removing the proxy set component, so you can directly access each node for a higher performance:
![](https://qcloudimg.tencent-cloud.cn/raw/b494d248fc185dff72c5d077fe157473.png)

## Sharded Cluster
TencentDB for MongoDB's sharded cluster architecture implements the horizontal capacity expansion of data based on the replica set architecture by combining multiple replica sets. Each sharded cluster instance is composed of mongos nodes, config server nodes, shard nodes, and other components.

- **mongos node**: it is responsible for receiving connection query requests from all client applications, routing the requests to the corresponding shards in the cluster, and splicing the received responses back to the clients. You can purchase multiple mongos nodes to achieve load balancing and failover. Each sharded cluster instance can contain 3–32 mongos nodes.

- **Config server node**: it is responsible for storing the metadata of the cluster and shard nodes, such as the cluster node information and routing information of sharded data. A config server node has a fixed specification of 1 CPU core, 2 GB memory, and 20 GB disk space in the form of 3-replica set by default, which cannot be modified. 

- **Shard node**: it is responsible for sharding data storage on multiple servers. You can purchase multiple shard nodes to horizontally expand the data storage and read/write concurrency capabilities of the instance. Each sharded cluster instance can contain 2–20 shard nodes.

![](https://qcloudimg.tencent-cloud.cn/raw/4bd4036e4ef5d9d4e9756cfa14f83250.png)

