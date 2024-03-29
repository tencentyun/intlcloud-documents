内存版（集群架构）兼容 Jedis Cluster 等智能客户端，为兼容 Jedis Cluster 的使用场景，云数据库 Redis 对 Cluster 支持命令返回对 IP 列表进行了修改，返回信息中每个节点的 IP 地址为实例的内网 IPv4 地址。 

## CLUSTER NODES
Redis 集群中的每个节点的信息，输出的每一行都代表一个节点。节点信息包含：节点 ID、内网 IPv4 地址与端口、节点主从角色、属性及其分配的槽位等。
![](https://qcloudimg.tencent-cloud.cn/raw/4bcd785fd19d0fc263fff02ad39f51a0.png)

## CLUSTER SLOTS
CLUSTER SLOTS 用于获取集群插槽与 Redis 实例的映射关系 。每个返回结果包含：
- 开始插槽范围。
- 结束插槽范围。
- 插槽范围对应的集群主节点信息，包括：内网 IPv4 地址与端口，及其节点 ID。
- 插槽范围对应的集群主节点的第一个副本信息。
- 第二个副本。
- ...继续，直到返回此主设备的所有副本。

![](https://qcloudimg.tencent-cloud.cn/raw/f72c98ff24f2b834e0fe79d61852622d.png)

