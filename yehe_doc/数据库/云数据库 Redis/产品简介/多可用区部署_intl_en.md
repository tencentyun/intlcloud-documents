You can now deploy TencentDB for Redis master and replica nodes in different availability zones (AZs) of the same region. Multi-AZ deployed instances have higher availability and better disaster recovery capability than single-AZ deployed instances.
- Single-AZ deployed instance: host- and rack-level disaster recovery
- Multi-AZ deployed instance: host-, rack-, and AZ-level disaster recovery

## Deployment Architecture
![](https://main.qcloudimg.com/raw/855cfa6d9f004b589c708eeb12de1518.png)
Description:
- LB (Load Balancer): a TencentDB for Redis instance in standard architecture or cluster architecture has at least 3 proxies which need to be accessed through LB.
- VIP: a multi-AZ deployed instance has only one VIP. You can use this VIP to access all nodes of the instance deployed in the region. Master-Replica switches of the instance will not change its VIP.
- Proxy: an instance has at least three proxies. For a standard architecture instance, the number of proxies = 3 + (the number of replicas -1); for a cluster architecture instance, the number of proxies = the number of shards * the number of replicas.
- Master (Group): "Master" refers to the master node of a TencentDB for Redis instance in standard architecture; "Master Group" refers to the master nodes of all shards of a TencentDB for Redis instance in cluster architecture.
- Replica (Group): "Replica" refers to the replica nodes of a TencentDB for Redis instance in standard architecture; "Replica Group" refers to the collection of replica nodes, each of which comes from a different shard of a TencentDB for Redis instance in the cluster architecture. For a cluster architecture instance, the replicas of a shard are divided into multiple Replica Groups so that these Replica Groups can be deployed in different AZs.
- Master AZ: the master AZ refers to the AZ where the master node resides. Unless manually changed in the console, the master AZ will remain the same. If the master node fails, it may be temporarily switched to a replica AZ, and will be automatically switched back to the master AZ in a few minutes once certain conditions are met. This switching back process won’t affect your business unless your business uses block commands, such as `blpop` or `blpush`.

## Failover (HA)
- Detect failed nodes: TencentDB for Redis in standard architecture or cluster architecture adopts the same cluster management mechanism as the Redis Cluster, which uses the Gossip protocol to detect the status of nodes in a cluster. The `cluster-node-timeout` parameter is used to specify the maximum amount of time a Redis cluster node can be unavailable, without it being considered as failing. We recommend you set this parameter to its default value (15 s) and do not change it. For more information, please see [Redis cluster tutorial](https://redis.io/topics/cluster-tutorial).
- Promote a replica to master: TencentDB for Redis adopts a failover mechanism different from that of Redis Cluster, which gives priority to promoting replicas in the master AZ to reduce access delay of the master AZ. The details are as follows:
 - Promote the replica if it has the latest data
 - Promote the replica in the master AZ if all replicas have the same data

## Cross-AZ Access
### Instances without read-only replicas
Read/Write separation disabled (that is, replicas can be written to and read from): write/read requests in a replica AZ are routed by proxy to the master node, and the master node synchronizes with replica nodes to ensure consistent data across all nodes. In this process, only one cross-AZ access happens.

### Instances with read-only replicas
Read/Write separation enabled (that is, replicas can only be read from): write requests are routed by proxy to the master node, but read requests are routed to the replica node in the same AZ as the proxy, so that read requests can get responded by the nearest node.

## Recommended Deployment Solution
### Two-AZ deployment
Deploy the master node and one replica node in the master AZ, and two replica nodes in the replica AZ. Both AZs, each of which has two nodes, are accessed through LB. If one node in an AZ fails, the read requests can be processed by the other node in the AZ. If an AZ fails, the other AZ is still highly available. This solution is applicable for use cases which have high requirements on availability and delay.
![](https://main.qcloudimg.com/raw/5a3cc43871565e6371d1d990e9845324.png)

### Three-AZ deployment
Deploy the master node in the master AZ, one replica node in replica AZ 1, and one replica node in replica AZ 2. If one node or one AZ fails, the whole architecture still has cross-AZ high availability. This solution is applicable to use cases which have ultra high requirements on availability but are insensitive to delay.
![](https://main.qcloudimg.com/raw/d2c4ad9ce6354559eaee7e191be59b7e.png)
 
## Operations
- For more information on how to configure and view multi-AZ deployment in the TencentDB for Redis console, please see [Configuring Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/239/39799).
- For more information on how to upgrade the deployment from single-AZ to multi-AZ in the TencentDB for Redis console, see [Upgrading to Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/239/39982).
- For more information on how to enable and disable read/write separation in the TencentDB for Redis console, please see [Enabling/Disabling Read/Write Separation](https://intl.cloud.tencent.com/document/product/239/31935).
- A single-AZ deployed TencentDB for Redis instance can be accessed by a VIP. So can a multi-AZ deployed instance. For more information, see [Accessing Multi-AZ Deployed Instances](https://intl.cloud.tencent.com/document/product/239/41053).
- TencentDB for Redis supports auto-failover to ensure the high availability of database service. For more information, see [Failover](https://intl.cloud.tencent.com/document/product/239/41052).
- Multi-AZ deployed TencentDB for Redis instances support auto-failback. For more information, see [Auto-Failback](https://intl.cloud.tencent.com/document/product/239/41051).
- For a multi-AZ deployed TencentDB for Redis instance, you can manually promote a replica node (group) in a specific AZ to master node (group) and the AZ will be automatically promoted to master AZ. For more information, see [Manually Promoting to Master Node (Group)](https://intl.cloud.tencent.com/document/product/239/41050).
- To reduce the latency of accessing a multi-AZ deployed TencentDB for Redis instance, you can read local nodes only. For more information, see [Reading Local Nodes Only](https://intl.cloud.tencent.com/document/product/239/41049).

