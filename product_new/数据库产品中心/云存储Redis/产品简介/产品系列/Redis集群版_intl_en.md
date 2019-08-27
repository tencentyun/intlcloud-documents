Redis Cluster Edition is a new edition of Redis built by Tencent Cloud based on the Community Edition of Redis 4.0. It uses a distributed architecture to enable elastic scaling and features high flexibility, availability, and performance of tens of millions of QPS. Specifically, it supports horizontal scaling of 3-128 shards and vertical scaling of 1-5 replica sets, where the scaling and migration are virtually imperceptible to the business, maximizing the system availability. ![](https://main.qcloudimg.com/raw/d023aa7ddecec8b0b42a899b7ea307b0.png)

## Cluster Specifications
- Shard size (GB): 4, 8, 12, 16, 20, 24, 28, 32
- Number of shards: 3, 5, 8, 12, 16, 24, 32, 64, 96, 128 
- Number of replicas: 1, 2, 3, 4, 5 

## Cluster Mode
- In Redis cluster mode, data is automatically sharded. The system providers data load balancing and migration capabilities.
- Redis cluster mode supports shards of 4-32 GB specifications.
- Redis cluster mode is compatible with certain commands of the non-cluster mode in terms of cross-slot data access. For more information, see [Use Limits](http://intl.cloud.tencent.com/document/product/239/18336).

## Replica Descriptions
- When there is only one replica, Redis provides master/slave real-time hot backup for high data reliability and availability. When the HA system detects a node failure, there will be requests for switching to a slave node, and a new slave node will be added to the system.
- When the number of replicas is greater than 1, Redis provides master/slave real-time hot backup with the slave nodes being read-only.

## Features
**Flexibility** 
Redis Cluster Edition supports horizontal scaling of 3-128 nodes and vertical scaling of 1-5 replica sets, making it ideal for various scenarios through instance specification adjustment.
**Availability** 
In Redis Cluster Edition, horizontal scaling (shard quantity) and vertical scaling (replica quantity) are virtually imperceptible to the business, maximizing the system availability.
 **Compatibility**
Redis Cluster Edition supports use cases of native clusters of the Redis Community Edition and Cordis and is compatible with clients such as Jedis.
 **OPS**
Redis Cluster Edition maximizes system capability openness and has advanced features such as shard-level monitoring and management, data migration and load balancing, as well as monitoring of big and hot keys, which help facilitate system management and OPS.

## Use Cases
**Master/slave high-availability scenarios**
Redis Cluster Edition allows you to configure a replica set for a single node to achieve high master/slave availability. It boasts dual-server hot backup and automatic failover to ensure high reliability and availability of the Redis service.
 **Read-write separation scenarios**  
When the number of replica nodes is greater than 1, automatic read-write separation can be enabled for the TencentDB for Redis instance to extend the read performance vertically of a single node. Up to 5 replica sets can be supported and read access weights across the master node and replica nodes can be configured. 
**Multi-shard high-performance scenarios**
Redis Cluster Edition automatically enables auto-sharding and achieves horizontal scaling of system performance by assigning different keys to multiple nodes.

## Use Limits
Redis Cluster Edition features automatic hash-based sharding. Shards of less than 4 GB are currently not provided in cluster mode.
In cluster mode, the support for commands by Redis includes: **supported**, **partially supported**, **custom commands**, and **unsupported**. For unsupported commands, an error will be returned as shown below:
```
 select 1
 (error) ERR unknown command 'select'
```

**Unsupported commands:**
Redis Cluster Edition does not support multi-DB but supports the `select 0` command, which may compromise performance. Therefore, dedicated databases are recommended. The following commands will be blocked, and an error will occur during their execution:
- MOVE
- SWAPDB
  

As data persistence and backup can be managed in the console, the following commands are not supported:
- BGREWRITEAOF
- BGSAVE
- LASTSAVE
  

System replication and high availability are managed by the backend of TencentDB for Redis in a unified manner. As corresponding operations may incur a stability risk, the following commands are not supported:
- REPLCONF
- SLAVEOF
- SYNC / PSYNC

Other unsupported commands:
- DEBUG 
- PFDEBUG
- OBJECT
- SHUTDOWN
- MONITOR
- COMMAND
- SCRIPT-DEBUG
- LATENCY
- READONLY
- TIME
- WAIT
- MODULE
- DBSIZE

**Partially supported commands:**
For compatibility with Jedis cluster, TencentDB for Redis modifies the IP list returned by the supported commands, and the IP address of each node in the returned information is the instance’s VIP.
- CLUSTER NODES
- CLUSTER SLOTS 
- CONFIG GET

Supported cross-slot commands
Currently, supported cross-slot access commands include:
- MGET
- MSET
- DEL

Cross-slot commands are not supported. The following error message will be displayed:
 `(error) CROSSSLOT Keys in request don't hash to the same slot`

Currently, unsupported cross-slot access commands are as follows:
- UNLINK
- EXISTS
- BRPOP
- BLPOP
- SINTER
- STNTERSTORE
- SUNION
- SDIFF
- SDIFFSTORE
- MSETNX
- PFCOUNT
- PFMERGE

**Transactional support**
Redis Cluster Edition supports transactional commands provided that the transactions are started by the WATCH command. The keys of a transaction should be stored in the same slot, and the keys of WATCH and transaction-related keys should be stored in the same slot too. HashTag is recommended for transactions in cluster mode. Supported commands are as follows:
- WATCH
- MULTI
- EXEC
- DISCARD
- UNWATCH
  

**Custom commands:**
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

 List of custom commands:
- INFO	 
- MEMORY
- SLOWLOG
- FLUSHDB
- PING
- KEYS (hashtag is supported and has matching priority)
- SCAN (hashtag is supported and has matching priority)

**Supported commands:**
  Redis Cluster Edition supports all commands except those mentioned above.

