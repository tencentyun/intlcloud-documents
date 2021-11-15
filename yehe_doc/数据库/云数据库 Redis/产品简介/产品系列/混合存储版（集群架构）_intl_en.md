TencentDB for Redis Hybrid Storage Edition (cluster architecture) is based on Tendis, a KV (key-value) RocksDB storage engine developed by and widely used in Tencent. It is compatible with Redis protocols and features high performance, high compression ratio and high stability. Tencent has extensive experience in Tendis operation.

Hybrid Storage Edition (cluster architecture) is composed of two components, i.e., Redis (cache) and Tendis (storage engine). It is suitable for KV storage scenarios, as it balances performance and cost, and greatly reduces your business operating costs by 80% in the scenarios where cold data takes up a lot of storage space.

Hybrid Storage Edition (cluster architecture) is fully compatible with Redis 4.0 Cluster Edition commands. It is easy to use and can make full use of a rich variety of data structures and operational commands of Redis for efficiency.

Hybrid Storage Edition (cluster architecture) stores all data on disk, and caches all keys and the values of hot keys in the memory. The system architecture is shown as below:
![](https://main.qcloudimg.com/raw/66a17ff0e7b746da59ba2e6074cd6c09.png)

## Features
#### Low cost
- Data is automatically cached and automatically degraded to cold data. All data is stored on disk, and hot data is cached in the memory. Hybrid Storage Edition reduces operating costs by 40% to 80% compared with TencentDB for Redis Memory Edition.
- Hybrid Storage Edition adopts the LZ4 data compression algorithm to automatically compress data once stored on disk, which balances performance and capacity and saves up to 90% of the disk capacity.

#### High efficiency
- With 100% compatibility with Redis protocols, all efficient Redis data structures and APIs can be used in the business.
- In Hybrid Storage Edition, the business does not need to swap hot and cold data, or deal with the data inconsistency, cache breakdown, cache avalanche and other problems existing in traditional caching schemes. Hybrid Storage Edition reduces the complexity of the business, improves the development efficiency and reduces the OPS cost.

#### High performance
- Up to 3,000,000+ QPS for hot data access, comparable to native Redis
- Up to 1,000,000 QPS for concurrent writes

#### Large capacity
- Super-large storage capacity of 240 GB to 32 TB
- The data stored on disk can have 6 replicas, fully ensuring data reliability.

## Architecture
The core components of TencentDB for Redis Hybrid Storage Edition (cluster architecture) include Proxy, Redis cache, and Tendis engine, as described below:
- Proxy: it routes and distributes client requests, distributes commands to the correct shard according to their keys, collects part of monitoring data, and disables high-risk commands online, etc.
- Redis cache: it is based on Redis 4.0 Cluster Edition. In order to achieve automatic degradation to cold data, Hybrid Storage Edition modifies core Redis features, including value eviction, value eviction based on time, synchronization of written data to Tendis, cold data access, and master/slave synchronization of hot data, etc. The modified Redis in Hybrid Storage Edition is 100% compatible with Redis 4.0 Cluster Edition commands.
- Tendis engine: it is a KV storage engine developed by Tencent and compatible with Redis protocols. Tendis has been used in Tencent for many years with its performance and stability being fully verified. In the hybrid storage system, its key features include the storage and reading of full data, data backup, incremental log backup, etc.
![](https://main.qcloudimg.com/raw/cacc7ad9deaa3659e07d9d202d4ed608.png)

## Application Scenarios
### Recommended scenarios
#### Storage scenarios
The data access acceleration scenario where Redis is used as the primary storage engine rather than the cache.

#### Latency-insensitive scenario
Because cold data needs to be read from disks, the latency of accessing cold data in Hybrid Storage Edition will significantly increase to tens or even hundreds of milliseconds, while the access delay in Redis Memory Edition is less than 1 ms.

#### Distributed hot/cold data scenario
Hybrid storage is ideal for scenarios where hot data degrades to cold data over time. Hot data is accessed frequently and requires short response latency. Cold data can have a short response latency after prefetch.


### Scenarios not recommended
#### Caching scenario
- Insufficient performance: the caching scenario requires high performance, but the Hybrid Storage Edition’s performance in cold data is much inferior to that of Memory Edition. For more information about performance, please see [Performance](https://intl.cloud.tencent.com/document/product/239/17952).
- Cost increase: Hybrid Storage Edition increases the disk storage space and adds more disk storage compute nodes. Since the caching scenario requires memory capacity close to disk capacity, business costs will rise rather than fall.

#### Latency-sensitive scenario
Because cold data needs to be read from disks, the latency of accessing cold data in Hybrid Storage Edition will significantly increase to tens or even hundreds of milliseconds, while the access delay in Redis Memory Edition is less than 1 ms. Therefore, Hybrid Storage Edition is not recommended for a latency-sensitive scenario.

## Specifications
>?
>- The minimum disk capacity must be greater than the memory capacity, otherwise the data may not be written.
>- The memory caches all keys and only evicts values, so the memory may not be able to cache all keys due to too small disk capacity configuration. Please evaluate the disk space.
>- Run the following `set` command with the 128-byte value to test the maximum write performance:
```
redis-benchmark -h 10.0.0.5 -p 6379 -c 100 -n 60000000 -r 1000000000 -d 128 -t set -a passwd
```

| Shard Quantity | Total Cache Capacity (GB) | Total Disk Capacity Range (GB) | Maximum Write Performance (QPS) |
| -------------- | ------------------------- | ------------------------------ | ------------------------------- |
| 4              | 64                        | 240 - 520                      | 60,000                          |
| 4              | 128                       | 480 - 960                      | 60,000                          |
| 4              | 256                       | 1,000 - 2,000                  | 60,000                          |
| 8              | 128                       | 480 - 960                      | 120,000                         |
| 8              | 256                       | 960 - 1,920                    | 120,000                         |
| 8              | 512                       | 2,000 - 4,000                  | 120,000                         |
| 16             | 256                       | 960 - 1,920                    | 240,000                         |
| 16             | 512                       | 1,920 - 3,840                  | 240,000                         |
| 16             | 1,024                     | 4,000 - 8,000                  | 240,000                         |
| 32             | 512                       | 3,840 - 7,680                  | 480,000                         |
| 32             | 1,024                     | 7,680 - 15,360                 | 480,000                         |
| 32             | 2,048                     | 16,000 - 32,000                | 480,000                         |



## Degradation to Cold Data
#### Value eviction policy
- **Value eviction only**
When you set a timeout period for keys or use the `expire` command, both keys and values will be evicted from the memory; otherwise, only values will be evicted.
- **value-eviction-policy**
 - Through `value-eviction-policy`, you can set how many days a value has not been accessed before it is automatically evicted from the memory.
- The default value of this parameter is 7 days. It can be modified by users in the console.
- **maxmemory-policy**
 - Hybrid Storage Edition only supports `allkeys-lru` (default) and `allkeys-random`.
 - When Redis memory usage reaches `maxmemory`, the system evicts values from the memory according to `maxmemory-policy`.

#### Value cache policy
- **value-cache-policy**
You can use this parameter to configure when disk data is cached into Redis memory: Redis caches a value into the memory if the number of times the value is accessed within 5 minutes is greater than `value-cache-policy`. This parameter can avoid cache invalidation caused by, such as, data traversal. If this parameter is configured to `1`, the cold data is immediately cached.

- **The `expire` command description**
If you use `Expire Time` to set a timeout period for keys, Hybrid Storage Edition will follow the original semantics of this command to evict expired keys and values from the memory and disks. The same is true for keys set with `EXPIRE`, `EXPIREAT`, `PEXPIRE`, and `PEXPIREAT` commands. 

- **Big key eviction**
To ensure reading performance, Hybrid Storage Edition currently does not evict a value from the memory, if the value is larger than 8 MB or has complex (non-string) structures with more than 1,000 fields. Therefore, Hybrid Storage Edition does not have an ideal effect on the degradation of complex data structures, such as large Hash structures, which will be continuously optimized in the future.


## Command Compatibility
Hybrid Storage Edition (cluster architecture) stores data in a distributed manner, and its biggest difference from the Memory Edition (standard architecture) lies in whether a single command supports multikey access. For the cluster architecture, commands can be categorized into supported, custom, and unsupported. For the complete list of compatible commands, please see [Command Compatibility](https://intl.cloud.tencent.com/document/product/239/31958).

 - **Unsupported commands**
The system will return the following error:
```
 keys *
 (error) ERR unknown command 'keys'
```

- **Partially supported commands**
Hybrid Storage Edition (cluster architecture) is compatible with smart clients such as JedisCluster. For compatibility with JedisCluster, TencentDB for Redis modifies the IP list returned by the supported commands, and the IP address of each node in the returned information is the instance's VIP.
 - CLUSTER NODES
 - CLUSTER SLOTS
 - CONFIG GET

- **Supported cross-slot commands**
Currently, cross-slot access commands supported by Hybrid Storage Edition (cluster architecture) include MGET, MSET, and DEL but not other multikey commands.

- **Custom commands**
Through VIP encapsulation, Hybrid Storage Edition (cluster architecture) provides a user experience in cluster mode comparable to the standalone edition, making it much easier for use in different scenarios. To increase the transparency to OPS, custom commands can be used. Access to each node in the cluster is supported by adding a parameter **node ID** on the right of the original command parameter list, such as `COMMAND arg1 arg2 ... [node ID]`. The node ID can be obtained through the `cluster nodes` command or in the [console](https://console.cloud.tencent.com/redis).

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

- **Transactional support**
Hybrid Storage Edition (cluster architecture) supports transactional commands. The keys of a transaction should be stored in the same slot, and the keys of the `WATCH` command and transaction-related keys should be stored in the same slot too. HashTag is recommended for multikey transactions in cluster mode.

- **Multi-database support**
Hybrid Storage Edition (cluster architecture) supports the `SELECT 0` command but not multiple databases.

- **Poor-performance commands**
  - `linsert` and `lrem`: the `linsert` and `lrem` commands in the List command family have poor performance and are not recommended thus. They will traverse the list nodes in the disk with the O(n) execution time complexity. If there are many list nodes, the command execution will time out.
  - `append`: the `append` command performs poorly when the character size exceeds 1 MB.
