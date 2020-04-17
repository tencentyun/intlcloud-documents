Redis Cluster Edition (CKV) provides dual-replica cluster edition instances, which break the single-thread bottleneck to meet your business needs for large capacity or high performance. The Cluster Edition is compatible with Redis 3.2 protocols and commands and supports up to 128 shards of 12 GB–48 TB capacity.

## Features
- **Service reliability**
With a dual-server master/slave architecture, the master and slave nodes reside on different physical machines with the master node providing external access. You can perform data CRUD using the Redis command line or client. The slave node provides data backup and high availability. In case that the master node fails, the proprietary HA system will automatically perform master/slave switchover to ensure smooth operation of the business.        
- **Data reliability**
The data persistence feature is enabled by default, so all data will be stored in disks. Data backup is supported; therefore, you can roll back or clone instances for backup sets to effectively cope with data misoperations and other issues.
- **Lower latency**
CKV uses a high-performance network platform and a proxy-free architecture, which significantly reduce the access latency and network latency by up to 60% in high-load scenarios.
- **Read-only slave**
CKV Cluster Edition can greatly improve the read performance by 40% on average by enabling slaves. The read-only slave feature is not enabled by default. Currently, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. Due to the replication delay between the CKV master node and slave node, after the real-only slave feature is enabled, some legacy data may be read; therefore, please confirm whether your business can accept slight data inconsistency before enabling this feature.
- **Smooth upgrade**
CKV Cluster Edition uses a unique scheme to ensure that version upgrade is imperceptible to the business, thereby ensuring maximum service availability.

## Use Cases
- **Single instance for high data volume**
The Cluster Edition uses a distributed architecture, making it suitable for storing high volumes of data in one single instance. Its capacity can exceed the upper limit of 384 GB of the CKV Standard Edition.
- **High QPS and concurrence requirements**
The Cluster Edition uses a distributed architecture where reads and writes are spread across multiple nodes. Under the condition that the keys are evenly distributed, its QPS can increase linearly with the number of nodes. At present, it supports a maximum of 128 shards and 10 million QPS.
- **Insensitivity for protocol support**
The Cluster Edition supports slightly less protocols than the open-source editions.

## Connection Sample
CKV Cluster Edition only supports the password format of `instance ID:password`. For example, if your instance ID is `crs-bkuza6i3` and the password is `abcd1234`, then the connection command should be `redis-cli -h IP -p port -a crs-bkuza6i3:abcd1234`.


## Use Limits
-The minimum unit of `pttl` setting display in the CKV engine is second, which is different from Redis Community Edition.
- Currently, string-type keys are supported, and a value can be up to 32 MB, which are different from Redis Community Edition.
- Except batch operations of MSET and MGET, other batch operations require the batch keys to be in the same slot; otherwise, an error will be displayed stating`CROSSSLOT Keys in request don't hash to the same slot`.
- After a shard is full, `subscribe` and `psubscribe` operations need to use a certain amount of memory; therefore, new subscriptions will be affected, but `publish` operations on subscribed channels will not.

## Notes
- At present, the size of a single shard in the Cluster Edition is 4 GB by default; therefore, it is recommended that the value of a single key not exceed 4 GB.
- The Cluster Edition currently provides monitoring at the cluster dimension.


## Compatibility

**Commands supported by the Cluster Edition:**
 
| **connection type** | **geo type** | **hashes type** | **hyperloglog type** | **keys type** | **lists type** | **pub/sub type** | 
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

|**sets type** | **sorted sets type** | **strings type** | **transactions type** |**server type** | 
| --- | --- | --- | --- | --- |
| sadd | zadd | append | discard | command |
| scard | zcard | bitcount | exec | dbsize |
| sdiff | zcount | bitop | multi |-
| sdiffstore | zincrby | bitpos | unwatch |-
| sinter | zinterstore | decr | watch |-
| sinterstore | zlexcount | decrby | -　 |-
| sismember | zrange | get | -　 |-
| smembers | zrangebylex | getbit | -　 |-
| smove | zrangebyscore | getrange | -　 |-
| spop | zrank | getset | -　 |-
| srandmember | zrem | incr | -　 |-
| srem | zremrangebylex | incrby | -　 |-
| sscan | zremrangebyrank | incrbyfloat | -　 |-
| sunion | zremrangebyscore | mget | -　 |-
| sunionstore | zrevrange | mset | -　 |-
| -　 | zrevrangebylex | msetnx | -　 |-
| -　 | zrevrangebyscore | psetex | -　 |-
| -　 | zrevrank | set | -　 |-
| -　 | zscan | setbit |- 　 |-
| -　 | zscore | setex | -　 |-
| -　 | zunionstore | setnx | -　 |-
| -　 | -　 | setrange | -　 |-
| -　 | -　 | strlen | -　 |-

**Commands not supported by the Cluster Edition:**

| **cluster type** | **connection type** | **keys type** | **lists type** | **scripting type** | **server type** | **strings type** |
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


