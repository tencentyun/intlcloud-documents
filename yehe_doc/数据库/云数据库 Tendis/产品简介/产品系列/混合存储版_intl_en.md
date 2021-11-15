TencentDB for Tendis Hybrid Storage Edition (cluster architecture) is based on Tendis, a KV (key-value) RocksDB storage engine developed by and widely used in Tencent. It is compatible with Redis protocols and features high performance, high compression ratio and high stability. Tencent has extensive experience in Tendis operation.

- Hybrid Storage Edition (cluster architecture) is composed of two components, i.e., Redis (cache) and Tendis (storage engine). It is suitable for KV storage scenarios, as it balances performance and cost, and greatly reduces your business operating costs by 80% in the scenarios where cold data takes up a lot of storage space.

- Hybrid Storage Edition (cluster architecture) is fully compatible with Redis 4.0 Cluster Edition commands. It is easy to use and can make full use of a rich variety of data structures and operational commands of Redis for efficiency.
- Hybrid Storage Edition (cluster architecture) stores all data on disk, and caches all keys and the values of hot keys in the memory.

## Features
#### Low costs
- Data is automatically cached and automatically degraded to cold data. All data is stored on disk, and hot data is cached in the memory. Hybrid Storage Edition reduces operating costs by 40% to 80% compared with TencentDB for Tendis Memory Edition.
- Hybrid Storage Edition adopts the LZ4 data compression algorithm to automatically compress data once stored on disk, which balances performance and capacity and saves up to 90% of the disk capacity.

#### High efficiency
- With 100% compatibility with Redis protocols, all efficient Redis data structures and APIs can be used in the business.
- In Hybrid Storage Edition, the business does not need to swap hot and cold data, or deal with the data inconsistency, cache breakdown, cache avalanche and other problems existing in traditional caching schemes. Hybrid Storage Edition reduces the complexity of the business, improves the development efficiency and reduces the OPS cost.

#### High performance
- Hot data access performance comparable to native Redis that can sustain more than 3 million [QPS](https://intl.cloud.tencent.com/document/product/1083/39245).
- Up to 1 million QPS for concurrent writes.

#### Large capacity
- Super-Large storage capacity of 240 GB to 32 TB
- The data stored on disk can have 6 replicas, fully ensuring data reliability.

## Architecture
The core components of TencentDB for Tendis Hybrid Storage Edition (cluster architecture) include Proxy, Redis cache, and Tendis engine, as described below:
- Proxy: it routes and distributes client requests, distributes commands to the correct shard according to their keys, collects part of monitoring data, and disables high-risk commands online, etc.
- Redis cache: it is based on Redis 4.0 Cluster Edition. In order to achieve automatic degradation to cold data, Hybrid Storage Edition modifies core Redis features, including value eviction, value eviction based on time, synchronization of written data to Tendis, cold data access, and primary/secondary synchronization of hot data, etc. The modified Redis in Hybrid Storage Edition is 100% compatible with Redis 4.0 Cluster Edition commands.
- Tendis engine: it is a KV storage engine developed by Tencent and compatible with Redis protocols. Tendis has been used in Tencent for many years with its performance and stability being fully verified. In the hybrid storage system, its key features include the storage and reading of full data, data backup, incremental log backup, etc.


## Specifications
>?
>- The minimum disk capacity must be greater than the memory capacity, otherwise the data may not be written.
>- The memory caches all keys and only evicts values, so the memory may not be able to cache all keys due to too small disk capacity configuration. Please evaluate the disk space.
>- Run the following `set` command with the 128-byte value to test the maximum write performance:
```
redis-benchmark -h 10.0.0.5 -p 6379 -c 100 -n 60000000 -r 1000000000 -d 128 -t set -a passwd
```

| Shard Quantity|Total Cache Capacity (GB)| Total Disk Capacity Range (GB)|Maximum Write Performance (QPS)|
| -----| -----| ---- | ---- |
| 4 | 64 | 240 - 520|60,000|
| 4 | 128 | 480 - 960|60,000|
| 4 | 256 | 1,000 - 2,000|60,000|
| 8 | 128 | 480 - 960|120,000|
| 8 | 256 | 960 - 1,920|120,000|
| 8 | 512 | 2,000 - 4,000|120,000|
| 16 | 256 | 960 - 1,920|240,000|
| 16 | 512 | 1,920 - 3,840|240,000|
| 16 | 1024 | 4,000 - 8,000|240,000|
| 32 | 512 | 3,840 - 7,680|480,000|
| 32 | 1024 | 7,680 - 15,360|480,000|
| 32 | 2048 | 16,000 - 32,000|480,000|


## Degradation to Cold Data
#### Value eviction policy
- **value-eviction-policy**
 - Valid values of the `value-eviction-policy` parameter include `time-to-eviction` and `none`. The default value is `none`, indicating that keys will not be evicted from the memory by default if the memory is sufficient.
 - By setting `value-eviction-policy` to `time-to-eviction`, you can specify that keys that have not been accessed in N minutes will be automatically evicted from the memory. The default value of the `value-time-to-eviction` parameter is 10,080 minutes (7 days), which can be customized in the [console](https://console.cloud.tencent.com/tendis#/).
- **maxmemory-policy**
 - Hybrid Storage Edition only supports `allkeys-lru` (default) and `allkeys-random`.
 - When memory usage reaches `maxmemory`, the system evicts values from the memory according to `maxmemory-policy`.

#### Value cache policy
- **value-cache-policy**
You can use this parameter to configure when the data will be cached into the Tendis cache. You can also use the following parameters to avoid cache invalidation issues caused by data traversal and other operations.
 - The default value of the `value-cache-policy-period` parameter is 300 seconds (5 minutes). You can specify that if the number of key accesses within N seconds is greater than or equal to N (value of `value-cache-policy-threshold`), Tendis will cache the value into the memory.
 - The default value of the `value-cache-policy-threshold` parameter is 1, and its range value is 1–100. If it is set to 1, cold data will be cached immediately.

- **`expire` command description**
If you use `Expire Time` to set a timeout period for keys, Hybrid Storage Edition will follow the original semantics of this command to evict expired keys and values from the memory and disks. The same is true for keys set with `EXPIRE`, `EXPIREAT`, `PEXPIRE`, and `PEXPIREAT` commands. 

- **Big key eviction**
To ensure reading performance, Hybrid Storage Edition currently does not evict a value from the memory, if the value is larger than 8 MB or has complex (non-string) structures with more than 1,000 fields. Therefore, Hybrid Storage Edition does not have an ideal effect on the degradation of complex data structures, such as large Hash structures, which will be continuously optimized in the future.


## Command Compatibility
Hybrid Storage Edition (cluster architecture) stores data in a distributed manner. For the cluster architecture, commands can be categorized into supported, custom, and unsupported. For the complete list of compatible commands, please see [Command Compatibility](https://intl.cloud.tencent.com/document/product/1083/39290).

 - **Unsupported commands**
The system will return the following error:
```
 keys *
 (error) ERR unknown command 'keys'
```

- **Partially supported commands**
Hybrid Storage Edition (cluster architecture) is compatible with smart clients such as JedisCluster. For compatibility with JedisCluster, TencentDB for Tendis modifies the IP list returned by the supported commands, and the IP address of each node in the returned information is the instance's VIP.
 - CLUSTER NODES
 - CLUSTER SLOTS
 - CONFIG GET

- **Supported cross-slot commands**
Currently, cross-slot access commands supported by Hybrid Storage Edition (cluster architecture) include MGET, MSET, and DEL but not other multikey commands.

- **Custom commands**
Through VIP encapsulation, Hybrid Storage Edition (cluster architecture) provides a user experience in cluster mode comparable to the standalone edition, making it much easier for use in different scenarios. To increase the transparency to OPS, custom commands can be used. Access to each node in the cluster is supported by adding a parameter **node ID** on the right of the original command parameter list, such as `COMMAND arg1 arg2 ... [node ID]`. The node ID can be obtained through the `cluster nodes` command or in the [console](https://console.cloud.tencent.com/tendis).

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

  Sample `SCAN` command:
  scan 0 238b45926a528c85f40ae89d6779c802eaa394a2
  scan 0 match a* 238b45926a528c85f40ae89d6779c802eaa394a2

  Sample `KEYS` command:
  keys a* 238b45926a528c85f40ae89d6779c802eaa394a2
```

- **Multi-Database support**
Hybrid Storage Edition (cluster architecture) supports the `SELECT 0` command but not multiple databases.

- **Poor-Performance commands**
  - `linsert` and `lrem`: the `linsert` and `lrem` commands in the List command group have poor performance and are not recommended thus. They will traverse the list nodes in the disk with the O(n) execution time complexity. If there are many list nodes, the command execution will time out.
  - `append`: the `append` command performs poorly when the character size exceeds 1 MB.

