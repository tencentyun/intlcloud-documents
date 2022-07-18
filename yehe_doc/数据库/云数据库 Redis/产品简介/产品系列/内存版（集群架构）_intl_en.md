TencentDB for Redis Memory Edition (Cluster Architecture) is a new edition of Redis built by Tencent Cloud based on Community Edition of Redis Cluster, which is compatible with Redis 4.0 and 5.0 commands. It uses a distributed architecture to enable elastic scaling and features high flexibility, availability, and performance of tens of millions of QPS. Specifically, it supports horizontal scaling of 1–128 shards and replica scaling of 1–5 replica sets, where the scaling and migration are virtually imperceptible to the business, maximizing the system availability.
![](https://main.qcloudimg.com/raw/d023aa7ddecec8b0b42a899b7ea307b0.png)

## Use Cases
**Master/replica high-availability (HA) scenarios**
Memory Edition (Cluster Architecture) allows you to configure a replica set for a single node to achieve high master/replica availability. It features dual-server hot backup and automatic failover to ensure high reliability and availability of the Redis service.
 **Read/Write separation scenarios**  
When the number of replica nodes is greater than or equal to 1, automatic read/write separation can be enabled for the TencentDB for Redis instance to extend the read performance of a single node. Up to five replica sets can be supported, and read access weights across the master and replica nodes can be configured. 
**Multi-shard high-performance scenarios**
Memory Edition (Cluster Architecture) automatically enables auto-sharding and achieves horizontal scaling of system performance by assigning different keys to multiple nodes.

## Cluster Specification
- Shard specs (GB): 2, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64
- Shard quantity: 1, 3, 5, 8, 12, 16, 24, 32, 40, 48, 64, 80, 96, 128
- Replica quantity: 1, 2, 3, 4, 5 

## Cluster Mode
- In cluster mode, data is automatically sharded. The system provides data load balancing and migration capabilities.
- The cluster mode supports shard specs of 2–64 GB.
- The cluster mode is compatible with certain commands of the non-cluster mode, mainly reflected in cross-slot data access. For more information, see [Notes on Command Compatibility](#xianzhi).

## Replica Description
- When there is only one replica, Redis provides master/replica real-time hot backup for high data reliability and availability (server-level HA is supported in a single AZ). When the HA system detects a node failure, it requests for switching to a replica node and adds a new replica node to the system.
- When the number of replicas is greater than 1, Redis provides master/replica real-time hot backup with the replica nodes being read-only.

## Features
**Flexibility** 
Memory Edition (Cluster Architecture) supports horizontal scaling of 1–128 nodes and scaling of 1-5 replica sets, making it ideal for various scenarios through instance specification adjustment.
**Availability** 
In Memory Edition (Cluster Architecture), scaling of shard quantity and replica quantity are virtually imperceptible to the business, maximizing the system availability.
 **Compatibility**
Memory Edition (Cluster Architecture) supports use cases of the Community Edition of Redis Cluster and Codis and is compatible with clients such as Jedis.
 **Ops**
Memory Edition (Cluster Architecture) maximizes system capability and has advanced features such as shard-level monitoring and management, data migration and load balancing, as well as monitoring of big and hot keys, which help facilitate total system management and Ops.

## [Notes on Command Compatibility](id:xianzhi)
For more information on the supported commands, see [Command Compatibility]](https://intl.cloud.tencent.com/document/product/239/48367).
