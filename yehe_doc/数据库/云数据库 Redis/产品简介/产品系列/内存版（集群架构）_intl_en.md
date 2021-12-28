TencentDB for Redis Memory Edition (cluster architecture) is a new edition of Redis built by Tencent Cloud based on Community Edition of Redis Cluster, which is compatible with Redis 4.0 and 5.0 commands. It uses a distributed architecture to enable elastic scaling and features high flexibility, availability, and performance of tens of millions of QPS. Specifically, it supports horizontal scaling of 1–128 shards and replica scaling of 1–5 replica sets, where the scaling and migration are virtually imperceptible to the business, maximizing the system availability.
![](https://main.qcloudimg.com/raw/d023aa7ddecec8b0b42a899b7ea307b0.png)

## Use Cases
**Master/replica high-availability (HA) scenarios**
The Memory Edition (cluster architecture) allows you to configure a replica set for a single node to achieve high master/replica availability. It boasts dual-server hot backup and automatic failover to ensure high reliability and availability of the Redis service.
 **Read/write separation scenarios**  
When the number of replica nodes is greater than 1, automatic read/write separation can be enabled for the TencentDB for Redis instance to extend the read performance of a single node. Up to 5 replica sets can be supported and read access weights across the master node and replica nodes can be configured. 
**High-performance scenarios for multiple shards**
The Memory Edition (cluster architecture) automatically enables auto-sharding and achieves horizontal scaling of system performance by assigning different keys to multiple nodes.

## Cluster Specifications
- Shard size (GB): 2, 4, 8, 12, 16, 20, 24, 28, 32, 40, 48, 64
- Number of shards: 1, 3, 5, 8, 12, 16, 24, 32, 40, 48, 64, 80, 96, 128
- Number of replicas: 1, 2, 3, 4, 5 

## Cluster Mode
- In cluster mode, data is automatically sharded. The system provides data load balancing and migration capabilities.
- The cluster mode supports shards of 2-64 GB.
- The cluster mode is compatible with certain commands of the non-cluster mode, mainly reflected in cross-slot data access. For more information, please see [Notes on Command Compatibility](#xianzhi).

## Replica Description
- When there is only one replica, Redis provides master/replica real-time hot backup for high data reliability and availability (server-level HA is supported in a single AZ). When the HA system detects a node failure, it requests for switching to a replica node, and add a new replica node to the system.
- When the number of replicas is greater than 1, Redis provides master/replica real-time hot backup with the replica nodes being read-only.

## Features
**Flexibility** 
The Memory Edition (cluster architecture) supports horizontal scaling of 1-128 nodes and scaling of 1-5 replica sets, making it ideal for various scenarios through instance specification adjustment.
**Availability** 
In Memory Edition (cluster architecture), scaling of shard quantity and replica quantity are virtually imperceptible to the business, maximizing the system availability.
 **Compatibility**
The Memory Edition (cluster architecture) supports use cases of the Community Edition of Redis Cluster and Codis and is compatible with clients such as Jedis.
 **OPS**
The Memory Edition (cluster architecture) maximizes system capability and has advanced features such as shard-level monitoring and management, data migration and load balancing, as well as monitoring of big and hot keys, which help facilitate total system management and OPS.

## [Notes on Command Compatibility](id:xianzhi)
The Memory Edition (cluster architecture) stores data in a distributed manner, and its biggest difference from standard architecture lies in whether a single command supports multikey access. For the cluster architecture, commands can be categorized into custom, supported, and unsupported. For the complete list of compatible commands, please see [Command Compatibility](https://intl.cloud.tencent.com/document/product/239/31958).

#### Unsupported commands
The system will return the following error:
```
 keys *
 (error) ERR unknown command 'keys'
```

#### Partially supported commands
The Memory Edition (cluster architecture) is compatible with smart clients such as JedisCluster. For compatibility with JedisCluster, TencentDB for Redis modifies the IP list returned by the supported commands, and the IP address of each node in the returned information is the instance's VIP.
- CLUSTER NODES
- CLUSTER SLOTS
- CONFIG GET

#### Supported cross-slot commands
Currently, cross-slot access commands supported by Memory Edition (cluster architecture) include only MGET, MSET, and DEL.

#### [Custom commands](id:ziding)
Through VIP encapsulation, the Memory Edition (cluster architecture) provides a user experience in cluster mode comparable to the standalone edition, making it much easier for use in different scenarios. To increase the transparency to OPS, custom commands can be used. Access to each node in the cluster is supported by adding a parameter **node ID** on the right of the original command parameter list, such as "COMMAND arg1 arg2 ... node ID". The node ID can be obtained through the `cluster nodes` command or in the console:
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

List of custom commands:
- INFO
- MEMORY
- SLOWLOG
- FLUSHDB
- PING
- KEYS (hashtag is supported and has matching priority)
- MONITOR

#### Transactional support
The Memory Edition (cluster architecture) supports transactional commands. A transaction should start with the `WATCH` command, the keys of a transaction should be stored in the same slot, and the keys of `WATCH` and transaction-related keys should be stored in the same slot too. Hashtag is recommended for multikey transactions in cluster mode.

#### Multi-database support
The Memory Edition (cluster architecture) supports multiple databases (256 by default); therefore, it can support all commands related to database operations.
