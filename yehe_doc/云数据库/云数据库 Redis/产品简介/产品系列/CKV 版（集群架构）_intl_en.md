
>?TencentDB for Redis CKV Edition is currently unavailable. We recommend [TencentDB for Redis Memory Edition](https://intl.cloud.tencent.com/document/product/239/18336) for you.

TencentDB for Redis CKV Edition (cluster architecture) provides dual-replica cluster instances, which break the single-thread bottleneck to meet your business needs for large capacity or high performance. CKV Edition (cluster architecture) is compatible with Redis 3.2 protocols and commands and supports up to 128 shards of 12 GB–48 TB capacity.

## Features
- **Robust service**
With a dual-server master/replica architecture, the master and replica nodes reside on different physical machines with the master node providing external access and the replica node providing data backup and high availability (HA). You can perform data CRUD using the Redis command line or client. In case that the master node fails, the proprietary HA system will automatically perform master/replica switchover to ensure smooth operation of the business.        
- **Reliable data**
The data persistence feature is enabled by default with all data stored in disks. CKV Edition (cluster architecture) supports data backup. You can roll back or clone instances from backup sets to effectively cope with data misoperations and other issues.
-**Lower latency**
CKV uses a high-performance network platform and a proxy-free architecture, which significantly reduce the access latency and network latency by up to 60% in high-load scenarios.
- **Read-only replica**
CKV Edition (cluster architecture) can greatly improve the read performance by 40% on average by enabling read-only replica. The read-only replica feature is not enabled by default. Currently, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. Due to the replication delay between the CKV master node and replica node, after the read-only replica feature is enabled, some legacy data may be read; therefore, please confirm whether your business can accept slight data inconsistency before enabling this feature.
- **Smooth upgrade**
With unique schemes, CKV Edition (cluster architecture) can ensure the business-imperceptible version upgrade, thus maximizing the service availability.

## Use Cases
- **Large volume of data in a single instance**
CKV Edition (cluster architecture) uses a distributed architecture, making it suitable for storing high volumes of data in one single instance. Its capacity can exceed the upper limit of 384 GB of CKV Edition (standard architecture).
- **High QPS and concurrence requirements**
CKV Edition (cluster architecture) uses a distributed architecture where reads and writes are spread across multiple nodes. Under the condition that the keys are evenly distributed, its QPS can increase linearly with the number of nodes. At present, it supports a maximum of 128 shards and 10 million QPS.
- **Insensitive protocol support**
CKV Edition (cluster architecture) supports slightly less protocols than the open-source editions.

## Connection Example
CKV Edition (cluster architecture) only supports the password format: `instance id:password`. For example, if your instance ID is crs-bkuza6i3 and the password is abcd1234, the connection command is redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234.


## Use Limits
- The minimum unit of `pttl` in CKV Edition is second, which is different from Redis Community Edition.
- Currently, string-type keys are supported, and a value can be up to 32 MB, which are different from Redis Community Edition.
- Except MSET and MGET, other batch operations require that all the keys be in the same slot, otherwise an error message "CROSSSLOT Keys in request don't hash to the same slot" may occur.
- When a shard is full, `subscribe`/`psubscribe` takes up a certain amount of memory, which affects the addition of a new subscription, but does not affect the publish of the subscribed channel.

## Notes
- At present, the size of a single shard in CKV Edition (cluster architecture) is 4 GB by default; therefore, it is recommended that the value of a single key not exceed 4 GB.
- CKV Edition (cluster architecture) currently provides monitoring at the cluster dimension.


## Compatibility

**Commands supported by CKV Edition (cluster architecture):**
 
| **connection Group** | **geo Group** | **hashes Group** | **hyperloglog Group** | **keys Group** | **lists Group** | **pub/sub Group** | 
| --- | --- | --- | --- | --- | --- | --- |
| auth | geoadd | hdel | pfadd | del | lindex | psubscribe | 
| echo | geohash | hexists | pfcount | exists | linsert | pubsub | 
| ping | geopos | hget | pfmerge | expire | llen | publish | time |
| quit | geodist | hgetall | -　 | expireat| lpop | punsubscribe | - |
| select | georadius | hincrby | -　 | type | lpush | subscribe | -　 |
| -　 | georadiusbymember | hincrbyfloat | - | ttl| lpushx | unsubscribe | -　 |
| -　 | -　 | hkeys | -　 | persist | lrange | -　 | -　 |
| -　 | -　 | hlen | -　 | pexpire | lrem | -　 | -　 |
| -　 | -　 | hmget | -　 | pexpireat | lset | -　 | -　 |
| -　 | -　 | hmset | -　 | pttl | ltrim | -　 | -　 |
| -　 | -　 | hset | -　 | rename | rpop | -　 | -　 |
| -　 | -　 | hsetnx | -　 | renamenx | rpoplpush | -　 | -　 |
| -　 | -　 | hstrlen | -　 | sort | rpush | -　 | -　 |
| -　 | -　 | hvals | -　 | - | rpushx | -　 | -　 |
| -　 |- 　 | hscan | -　 |-  | -　 | -　 | -　 |

|**sets Group** | **sorted sets Group** | **strings Group** | **transactions Group** |**server Group** | 
| --- | --- | --- | --- | --- |
| sadd | zadd | append | discard | command |
| scard | zcard | bitcount | exec | dbsize |
| sdiff | zcount | bitop | multi |- |
| sdiffstore | zincrby | bitpos | unwatch |- |
| sinter | zinterstore | decr | watch |- |
| sinterstore | zlexcount | decrby | -　 |- |
| sismember | zrange | get | -　 |- |
| smembers | zrangebylex | getbit | -　 |- |
| smove | zrangebyscore | getrange | -　 |- |
| spop | zrank | getset | -　 |- |
| srandmember | zrem | incr | -　 |- |
| srem | zremrangebylex | incrby | -　 |- |
| sscan | zremrangebyrank | incrbyfloat | -　 |- |
| sunion | zremrangebyscore | mget | -　 |- |
| sunionstore | zrevrange | mset | -　 |- |
| -　 | zrevrangebylex | msetnx | -　 |- |
| -　 | zrevrangebyscore | psetex | -　 |- |
| -　 | zrevrank | set | -　 |- |
| -　 | zscan | setbit |- 　 |- |
| -　 | zscore | setex | -　 |- |
| -　 | zunionstore | setnx | -　 |- |
| -　 | -　 | setrange | -　 |- |
| -　 | -　 | strlen | -　 |- |

**Commands not supported by CKV Edition (cluster architecture):**

| **cluster Group** | **connection Group** | **keys Group** | **lists Group** | **scripting Group** | **server Group** | **strings Group** |
| --- | --- | --- | --- | --- | --- | --- |
| cluster addslots | swapdb | touch | blpop | eval | bgrewriteaof | bitfield |
| cluster count-failure-reports | -　 | restore | brpop | evalsha | bgsave | -　 |
| cluster delslots | -　 | object | brpoplpush | script debug | client kill | -　 |
| cluster failover | -　 | unlink | -　 | script exists | client list | -　 |
| cluster forget | -　 | wait | -　 | script flush | client getname | -　 |
| cluster meet | -　 | migrate | -　 | script kill | client pause | -　 |
|cluster replicate  | -　 | dump | -　 | script load | client reply | -　 |
| cluster reset | -　 | scan | -　 | -　 | client setname | -　 |
| cluster saveconfig | -　 |keys 　 | 　- | -　 | command count | -　 |
|cluster set-config-epoch  | -　 |move 　 | -　 | -　 | command getkeys | -　 |
| cluster setslot | -　 |randomkey 　 | -　 | -　 | command info | -　 |
|cluster slaves  | -　 | -　 | -　 | -　 | config get | 　- |
|readonly  | -　 | -　 | -　 | -　 | config rewrite |- 　 |
| readwrite |- 　 | -　 | -　 | -　 | config set | -　 |
| - | -　 | -　 | -　 | -　 | config resetstat | -　 |
| - | -　 | -　 | -　 | -　 | debug object | -　 |
| - | -　 | -　 | -　 | -　 | debug segfault | -　 |
| - | -　 | -　 | -　 | -　 | flushall | -　 |
|-  | -　 | -　 | -　 | -　 | flushdb | -　 |
| - | -　 | -　 | -　 | -　 | lastsave | -　 |
| -　 | -　 | -　 | -　 | -　 | monitor | -　 |
| -　 | -　 | -　 | -　 | -　 | role | -　 |
| -　 | -　 | -　 | -　 | -　 | save | -　 |
| -　 | -　 | -　 | -　 | -　 | shutdown | -　 |
| -　 | -　 | -　 | -　 | -　 | slaveof | -　 |
| -　 | -　 | -　 | -　 | -　 | slowlog | -　 |
| -　 | -　 | -　 | -　 | -　 | sync | -　 |
| -　 | -　 | -　 | -　 | -　 | info | 　- |


