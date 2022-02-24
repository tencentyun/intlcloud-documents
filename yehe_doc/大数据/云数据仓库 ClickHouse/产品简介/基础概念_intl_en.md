### Region
A region is a geographical area where a physical Cloud Data Warehouse server is located. Select a Tencent Cloud region with caution as you cannot change it after service purchase and networks are completely isolated between regions. For a lower access latency and higher read and write speeds, we recommend you select a region closest to your users.

### AZ
An availability zone (AZ) is a physical IDC with isolated resources within a region.

### Cloud Data Warehouse Cluster
A Cloud Data Warehouse cluster is a distributed cluster of multiple ClickHouse nodes, each of which may have one or two replicas depending on the specifications you purchase. A cluster may contain one or more shards.

### Shard
Cloud Data Warehouse stores massive amounts of data on multiple nodes, each of which only stores and processes a part of the data. When there is one replica, a shard corresponds to a node; when there are two replicas, a shard corresponds to two nodes.

### Replica
A replica is used to guarantee data security and service availability in case of exceptions. Cloud Data Warehouse stores data on two nodes to generate two replicas.

### HA
In HA mode, each shard has two replicas to ensure the cluster availability in case one of them fails.
