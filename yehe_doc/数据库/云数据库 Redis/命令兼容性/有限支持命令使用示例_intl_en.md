Memory Edition (Cluster Architecture) is compatible with smart clients such as JedisCluster. For compatibility with JedisCluster, TencentDB for Redis modifies the IP list returned by the supported commands, and the IP address of each node in the returned information is the instance's private IPv4 Address. 

## CLUSTER NODES
CLUSTER NODES is used to get the information of each node in a Redis cluster, where each output line represents a node. Node information includes node ID, private IPv4 address and port, node role (master or replica), attributes, and assigned slots.
![](https://qcloudimg.tencent-cloud.cn/raw/4bcd785fd19d0fc263fff02ad39f51a0.png)

## CLUSTER SLOTS
CLUSTER SLOTS is used to get the mapping relationship between cluster slots and Redis instances. Each returned result contains:
- Start slot range.
- End slot range.
- Information of the cluster's master node corresponding to the slot range, including the private IPv4 address, port, and node ID.
- Information of the first replica of the cluster's master node corresponding to the slot range.
- Information of the second replica.
- And so on in a similar manner until the information of all replicas is returned.

![](https://qcloudimg.tencent-cloud.cn/raw/f72c98ff24f2b834e0fe79d61852622d.png)

