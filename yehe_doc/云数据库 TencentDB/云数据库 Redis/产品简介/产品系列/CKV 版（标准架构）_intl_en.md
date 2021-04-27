
>?TencentDB for Redis CKV Edition is currently unavailable. We recommend [TencentDB for Redis Memory Edition](https://intl.cloud.tencent.com/document/product/239/31959) for you.

TencentDB for Redis CKV Edition (standard architecture) uses a master/replica node deployment architecture to provide data persistence and backup, making it suitable for scenarios that require both high data reliability and availability.
A master node provides daily service access, while a replica node ensures high availability (HA). In case that the master node fails, the system will automatically switch to the replica node to guarantee business continuity. CKV Edition (standard architecture) is compatible with Redis 3.2 commands and protocols and supports a specification of 4–384 GB to meet the needs of large-capacity storage.
![](https://main.qcloudimg.com/raw/dd4615622819ebf541e3c33d76302b73.png)

## Features
- **Robust service**
With a dual-server master/replica architecture, the master and replica nodes reside on different physical machines with the master node providing external access and the replica node providing data backup and HA. You can perform data CRUD using the Redis command line or client. In case that the master node fails, the proprietary HA system will automatically perform master/replica switchover to ensure smooth operation of the business.        
-**Reliable data**
The data persistence feature is enabled by default with all data stored in disks. CKV Edition (standard architecture) supports data backup. You can roll back or clone instances from backup sets to effectively cope with data misoperations and other issues.
- **Lower latency**
CKV uses a high-performance network platform and a proxy-free architecture, which significantly reduce the access latency and network latency by up to 60% in high-load scenarios.
- **Read-only replicas**
CKV Edition (standard architecture) can greatly improve the read performance by 40% on average by enabling read-only replica. The read-only replica feature is not enabled by default. Currently, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. Due to the replication delay between the CKV master node and replica node, after the read-only replica feature is enabled, some legacy data may be read; therefore, please confirm whether your business can accept slight data inconsistency before enabling this feature.
- **Smooth upgrade**
With unique schemes, CKV Edition (standard architecture) can ensure the business-imperceptible version upgrade, thus maximizing the service availability.

## Use Limits

- CKV Edition (standard architecture) supports up to 120,000 QPS. If you need a higher QPS, you can choose the cluster architecture that supports tens of millions of QPS.
-The minimum unit of `pttl` in CKV Edition is second, which is different from Redis Community Edition.
- Currently, string-type keys are supported, and a value can be up to 32 MB.
- The instance connection method is `instance ID:password`, which is different from that of the Memory Edition in standard or cluster architecture.
- The time complexity implemented by the `dbsize` command is O(n). When the command is executed, it needs to traverse all keys in the current database; therefore, it should be used with caution.
- There is a built-in string-type key: `{ckv_plus_pub_sub}_patterns`, which is used to support the pub/sub feature. If you need to use this feature, please do not delete this key; otherwise, subscriptions will become invalid.
- Event notification currently does not support notifications of expiration and eviction policy.
- The eviction policy currently only supports `volatile-lru`. The eviction mechanism can be disabled with the corresponding parameter `maxmemory-policy`.


## Connection Example
CKV Edition (standard architecture) only supports the password format: `instance id:password`. For example, if your instance ID is crs-bkuza6i3 and the password is abcd1234, the connection command is `redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`.

## Compatibility
**Commands supported by CKV Edition (standard architecture):**

| **connection Group** | **geo Group** | **hashes Group** | **hyperloglog Group** | **keys Group** | **lists Group** | **pub/sub Group** | **server Group** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| auth | geoadd | hdel | pfadd | del | lindex | psubscribe | command |
| echo | geohash | hexists | pfcount | scan | linsert | pubsub | dbsize |
| ping | geopos | hget | pfmerge | exists | llen | publish | info |
| quit | geodist | hgetall | -　 | expire | lpop | punsubscribe | time |
| select | georadius | hincrby | -　 | expireat | lpush | subscribe | -　 |
| -　 | georadiusbymember | hincrbyfloat | -　 | keys | lpushx | unsubscribe | -　 |
| -　 |- 　 | hkeys | -　 | type | lrange | -　 | -　 |
| -　 | -　 | hlen | -　 | move | lrem | -　 | -　 |
| -　 | -　 | hmget | -　 | ttl | lset | 　- | -　 |
| -　 | -　 | hmset | -　 | persist | ltrim | -　 | -　 |
| -　 | -　 | hset | -　 | pexpire | rpop | -　 | -　 |
| -　 | -　 | hsetnx | -　 | pexpireat | rpoplpush | -　 | -　 |
| -　 | -　 | hstrlen | -　 | pttl | rpush | -　 | -　 |
| -　 | -　 | hvals | -　 | randomkey | rpushx | -　 | -　 |
| -　 | -　 | hscan | -　 | rename | -　 | -　 | -　 |
| -　 | -　 | -　 | -　 | renamenx | -　 | -　 | -　 |
| -　 | -　 | -　 | -　 | sort | -　 | -　 | -　 |


|**sets Group** | **sorted sets Group** | **strings Group** | **transactions Group** | **scripting Group** |
| --- | --- | --- | --- | --- |
| sadd | zadd | append | discard |eval|
| scard | zcard | bitcount | exec |script debug|
| sdiff | zcount | bitop | multi |script exists|
| sdiffstore | zincrby | bitpos | unwatch |script flush|
| sinter | zinterstore | decr | watch |script kill|
| sinterstore | zlexcount | decrby | -　 |script load |
| sismember | zrange | get | -　 |-  |
| smembers | zrangebylex | getbit | -　 |-  |
| smove | zrangebyscore | getrange | -　 |-  |
| spop | zrank | getset | -　 |-  |
| srandmember | zrem | incr | -　 |-  |
| srem | zremrangebylex | incrby | -　 |-  |
| sscan | zremrangebyrank | incrbyfloat | -　 |-  |
| sunion | zremrangebyscore | mget | -　 |-  |
| sunionstore | zrevrange | mset | -　 |-  |
| -　 | zrevrangebylex | msetnx | -　 |-  |
| -　 | zrevrangebyscore | psetex | -　 |-  |
| -　 | zrevrank | set | -　 |-  |
| -　 | zscan | setbit | -　 |-  |
| -　 | zscore | setex | -　 |-  |
| -　 | zunionstore | setnx | -　 |-  |
| -　 | -　 | setrange |- 　 |-  |
| -　 | -　 | strlen | -　 |-  |

**Commands not supported by CKV Edition (standard architecture):**

| **cluster Group** | **connection Group** | **keys Group** | **lists Group** | **scripting Group** | **server Group** | **strings Group** |
| --- | --- | --- | --- | --- | --- | --- |
| cluster addslots | swapdb | touch | blpop | evalsha | bgrewriteaof | bitfield |
| cluster count-failure-reports | -　 | restore | brpop | - | bgsave |- 　 |
| cluster countkeyinslot | -　 | object | brpoplpush | - | client kill | -　 |
| cluster delslots | -　 | unlink | -　 |-  | client list | -　 |
| cluster failover | - | wait | 　- |-  | client getname | -　 |
| cluster forget | -　 | migrate | -　 |-  | client pause | 　- |
| cluster getkeysinslot | -　 | dump | 　- |- | client reply | -　 |
| cluster info | -　 | 　- | -　 | 　- | client setname | 　- |
| cluster keyslot | -　 | -　 | -　 | 　- | command count | -　 |
| cluster meet |- 　 | -　 | 　- | -　 | command getkeys | 　- |
| cluster nodes | 　- | 　- | -　 | -　 | command info | -　 |
| cluster replicate | -　 | 　- | -　 | -　 | config get | -　 |
| cluster reset | 　- | 　- | -　 |- 　 | config rewrite | -　 |
| cluster saveconfig | -　 | 　- | 　- | 　- | config set | -　 |
| cluster set-config-epoch | -　 | -　 | 　- | 　- | config resetstat | 　- |
| cluster setslot | 　- | 　- | 　- |- 　 | debug object | -　 |
| cluster slaves | 　- | 　- | 　- | -　 | debug segfault | -　 |
| cluster slots | -　 | 　- | 　- | 　- | flushall | -　 |
| readonly | -　 | 　- | 　- | -　 | flushdb | 　- |
| readwrite | -　 | -　 | -　 | 　- | lastsave | -　 |
| -　 | -　 | -　 | -　 | 　- | monitor | -　 |
| -　 | -　 | -　 | 　- | 　- | role | 　- |
| 　- | -　 | -　 | -　 | -　 | save | 　- |
| 　- | -　 | -　 | -　 | -　 | shutdown | 　- |
| -　 | -　 | -　 | -　 | -　 | slaveof | -　 |
| -　 | -　 | -　 | -　 | -　 | slowlog | -　 |
| -　 | -　 | -　 | -　 | -　 | sync | -　 |
