Redis Cluster Edition is a new edition of Redis built by Tencent Cloud based on the Community Edition of Redis Cluster that is compatible with Redis 4.0 and 5.0 commands. It uses a distributed architecture to enable elastic scaling and features high flexibility, availability, and performance of tens of millions of QPS. Specifically, it supports horizontal scaling of 3–128 shards and replica scaling of 1–5 replica sets, where the scaling and migration are virtually imperceptible to the business, maximizing the system availability. ![](https://main.qcloudimg.com/raw/d023aa7ddecec8b0b42a899b7ea307b0.png)

## Cluster Specification
- Shard size (GB): 2, 4, 8, 12, 16, 20, 24, 28, 32
- Number of shards: 3, 5, 8, 12, 16, 24, 32, 64, 96, 128 
- Number of replicas: 1, 2, 3, 4, 5 
>With the shard specification of 2 GB, up to 8 shards can be supported.

## Cluster Mode
- In Redis cluster mode, data is automatically sharded. The system provides data load balancing and migration capabilities.
- Redis cluster mode supports shards of 2–32 GB specifications.
- Redis cluster mode is compatible with certain commands of the non-cluster mode, mainly reflected in cross-slot data access. For more information, pleas see [Notes on Command Compatibility](#xianzhi).

## Replica Description
- When there is only one replica, Redis provides master/slave real-time hot backup for high data reliability and high availability (cross-server in the same AZ). When the HA system detects a node failure, it requests for switching to a slave node, and add a new slave node to the system.
- When the number of replicas is greater than 1, Redis provides master/slave real-time hot backup with the slave nodes being read-only.

## Features
**Flexibility** 
Redis Cluster Edition supports horizontal scaling of 3–128 nodes and replica scaling of 1–5 replica sets, making it ideal for various scenarios through instance specification adjustment.
**Availability** 
In Redis Cluster Edition, scaling of shard quantity and replica quantity are virtually imperceptible to the business, maximizing the system availability.
 **Compatibility**
Redis Cluster Edition supports use cases of native clusters of the Redis Community Edition and Codis and is compatible with clients such as Jedis.
 **OPS**
Redis Cluster Edition maximizes system capability openness and has advanced features such as shard-level monitoring and management, data migration and load balancing, as well as monitoring of big and hot keys, which help facilitate total system management and OPS.

## Use Cases
**Master/Slave high-availability scenarios**
Redis Cluster Edition allows you to configure a replica set for a single node to achieve high master/slave availability. It features dual-server hot backup and automatic failover to ensure high reliability and availability of the Redis service.
 **Read/write separation scenarios**  
When the number of replica nodes is greater than 1, automatic read/write separation can be enabled for the TencentDB for Redis instance to extend the read performance of a single node. Up to 5 replica sets can be supported and read access weights across the master node and replica nodes can be configured. 
**Multi-shard high-performance scenarios**
Redis Cluster Edition automatically enables auto-sharding and achieves horizontal scaling of system performance by assigning different keys to multiple nodes.


<span id = "xianzhi"></span>
## Command Compatibility Description
Redis Cluster Edition stores data in a distributed manner, and its biggest difference from the Standard Edition lies in whether a single command supports multikey access. For the Cluster Edition, commands can be categorized into supported, partially supported, and unsupported. For the complete list of compatible commands, please see [Command Compatibility](https://intl.cloud.tencent.com/document/product/239/31958).

#### Unsupported commands
The system will return the following error:
```
 keys *
 (error) ERR unknown command 'keys'
```

#### Partially supported commands
Redis Cluster Edition is compatible with smart clients such as JedisCluster. For compatibility with JedisCluster, TencentDB for Redis modifies the IP list returned by the supported commands, and the IP address of each node in the returned information is the instance's VIP.
- CLUSTER NODES
- CLUSTER SLOTS
- CONFIG GET

#### Supported cross-slot commands
Currently, cross-slot access commands supported by the Cluster Edition include MGET, MSET, and DEL but not other multikey commands.

<span id = "ziding"></span>
#### Custom commands
Through VIP encapsulation, Redis Cluster Edition provides a user experience in cluster mode comparable to the standalone edition, making it much easier for use in different scenarios. To increase the transparency to OPS, custom commands can be used. Access to each node in the cluster is supported by adding a parameter **node ID** on the right of the original command parameter list, such as COMMAND arg1 arg2 ... node ID. The node ID can be obtained through the `cluster nodes` command or in the console:
```
  10.1.1.1:2000> cluster nodes
  25b21f1836026bd49c52b2d10e09fbf8c6aa1fdc 10.0.0.15:6379@11896 slave 36034e645951464098f40d339386e9d51a9d7e77 0 1531471918205 1 connected
  da6041781b5d7fe21404811d430cdffea2bf84de 10.0.0.15:6379@11170 master - 0 1531471916000 2 connected 10923-16383
  36034e645951464098f40d339386e9d51a9d7e77 10.0.0.15:6379@11541 myself,master - 0 1531471915000 1 connected 0-5460
  53f552fd8e43112ae68b10dada69d3af77c33649 10.0.0.15:6379@11681 slave da6041781b5d7fe21404811d430cdffea2bf84de 0 1531471917204 3 connected
  18090a0e57cf359f9f8c8c516aa62a811c0f0f0a 10.0.0.15:6379@11428 slave ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 0 1531471917000 2 connected
  ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 10.0.0.15:6379@11324 master - 0 1531471916204 0 connected 5461-10922

  Native command:
  info server
  Custom command:
  info server ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171
  
  SCAN command examples:
  scan 0 238b45926a528c85f40ae89d6779c802eaa394a2
  scan 0 match a* 238b45926a528c85f40ae89d6779c802eaa394a2
  
  KEYS command example:
  keys a* 238b45926a528c85f40ae89d6779c802eaa394a2
```

Custom command list:
- INFO
- MEMORY
- SLOWLOG
- FLUSHDB
- PING
- KEYS (hashtag is supported and has matching priority)
- SCAN (hashtag is supported and has matching priority)
- MONITOR

#### Transactional support
Redis Cluster Edition supports transactional commands provided that the transactions are started by the WATCH command. The keys of a transaction should be stored in the same slot, and the keys of WATCH and transaction-related keys should be stored in the same slot too. HashTag is recommended for multikey transactions in cluster mode.

#### Multi-Database support
Redis Cluster Edition supports multiple databases (256 by default); therefore, it can support all commands related to database operations.
