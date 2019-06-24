Redis 마스터/슬레이브 버전(커뮤니티)은 가장 일반적으로 사용되는 Redis 버전으로 Redis 2.8 버전의 프로토콜, 명령과 호환합니다. 마스터/슬레이브 노드 배포 아키텍처를 채택하여 데이터 지속화와 백업을 제공하며 데이터 신뢰성 및 가용성에 대한 요구가 있는 시나리오에 적합합니다. 마스터 노드는 일상 서비스 접근을 제공하며, 슬레이브 노드는 가용성이 뛰어난 클러스터(HA)를 제공합니다. 마스터 노드가 고장날 경우, 시스템은 슬레이브 노드로 자동으로 전환하여 비즈니스를 안정적으로 실행할 수 있도록 확보합니다.
![](https://main.qcloudimg.com/raw/37626b6980e25a1ddf4fd3efcf4bbd4a.png)

## 기능 특성
-   **강력한 서비스**
이중 서버 마스터/슬레이브 아키텍처를 채택하며, 마스터/슬레이브 노드는 다른 물리적 기기에 위치합니다. 마스터 노드는 외부 접근을 지원하며, 사용자는 Redis 명령행과 공용 클라이언트를 통해 데이터를 추가, 삭제, 수정 및 조회할 수 있습니다. 서버 노드가 고장날 경우, 자체 연구한 HA 시스템이 마스터/슬레이브 전환을 자동으로 진행하여 비즈니스를 안정적으로 실행할 수 있도록 확보합니다.        
-   **믿을 만한 데이터**
데이터 지속화 기능을 기본적으로 활성화합니다. 마스터/슬레이브 버전은 데이터 백업 기능을 지원하며, 사용자는 백업 세트에 대해 인스턴스 롤백 또는 클론 등 작업을 진행할 수 있으며 데이터 오작동 등 문제를 효과적으로 해결할 수 있습니다.

## 사용 제한
- Redis 마스터/슬레이브 버전은 지원하는 사양은 0.25GB - 60GB이며, 더 큰 마스터/슬레이브 버전 사양이 필요할 경우, 최대 384GB까지 지원하는 CKV 마스터/슬레이브 버전을 선택하거나 최대 48TB의 용량까지 지원하는 클러스터 버전을 선택할 수 있습니다.
- Redis 마스터/슬레이브 버전은 최대 10만 QPS를 지원하며 더 높은 QPS가 필요할 경우, Redis 클러스터 버전 또는 CKV 클러스터 버전을 선택하십시오. 천만 수준의 QPS를 지원할 수 있습니다.

## 호환성
TencentDB for Redis 마스터/슬레이브 버전은 Redis 2.8 프로토콜 명령과 호환합니다. 자체 연구한 Redis 데이터베이스는 Redis 표준 버전까지 순조롭게 마이그레이션할 수 있을 뿐만 아니라 데이터 전송 도구(DTS)를 제공하여 증분의 Redis 마이그레이션을 진행함으로서 비즈니스를 원활하게 전환할 수 있습니다.

>?2018년 11월 1일 이전에 구매한 인스턴스는 client list, monitor, scritp 명령을 지원하지 않으며 활성화해야 할 경우, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 하여 신청하십시오.

**마스터/슬레이브 버전 Redis가 지원하는 명령:**

| **connection 패밀리** | **hashes 패밀리** | **keys 패밀리** | **lists 패밀리** | **pub/sub 패밀리** | **server 패밀리** | 
| --- | --- | --- | --- | --- | --- |
| auth | hdel | del | lindex | psubscribe | command | 
| echo | hexists | scan | linsert | pubsub | dbsize |
| ping | hget | exists | llen | publish | info | 
| quit | hgetall | expire | lpop | punsubscribe | time | 
| select | hincrby | expireat | lpush | subscribe | client list  | 
| -  | hincrbyfloat | keys | lpushx | unsubscribe | config get  | 
| -　 | hkeys | type | lrange | -　 | monitor  | 
| -　 | hlen | move | lrem | -　 | flushdb  |
| -　 | hmget | ttl | lset | -　 | flushall  |
| -　 | hmset | persist | ltrim | -　 | slowlog  |
| -　 | hset | pexpire | rpop | -　 | -  |
| -　 | hsetnx | pexpireat | rpoplpush | -　 | -  |
| -　 | hstrlen | pttl | rpush | -　 |-  |
| -　 | hvals | randomkey | rpushx | -　 | -  |
| -　 | hscan | rename | blpop | -　 | -  |
| -　 | -　 | renamenx | brpop | -　 | -　 |
| -　 | -　 | sort | brpoplpush | -　 | -　 |


|**sets 패밀리** | **sorted sets 패밀리** | **strings 패밀리** | **transactions 패밀리** |**hyperloglog 패밀리** |**scripting 패밀리** |
| --- | --- | --- | --- | --- | -- |
| sadd | zadd | append | discard |pfadd |eval |
| scard | zcard | bitcount | exec |pfcount| evalsha |
| sdiff | zcount | bitop | multi |pfmerge| script debug |
| sdiffstore | zincrby | bitpos | unwatch |  |script exists|
| sinter | zinterstore | decr | watch | | script flush |
| sinterstore | zlexcount | decrby | -　 | | script load |
| sismember | zrange | get | -　 | |script kill |
| smembers | zrangebylex | getbit | -　 |
| smove | zrangebyscore | getrange | -　 |
| spop | zrank | getset | -　 |
| srandmember | zrem | incr | -　 |
| srem | zremrangebylex | incrby | -　 |
| sscan | zremrangebyrank | incrbyfloat | -　 |
| sunion | zremrangebyscore | mget | -　 |
| sunionstore | zrevrange | mset | -　 |
| -　 | zrevrangebylex | msetnx | -　 |
|- 　 | zrevrangebyscore | psetex | -　 |
| -　 | zscore | setex | -　 |
| -　 | zrevrank | set | -　 |
| -　 | zscan | setbit | -　 |
| -　 | zunionstore | setnx | -　 |
| -　 | -　 | setrange | -　 |
| -　 | -　 | strlen | -　 |

**마스터/슬레이브 버전 Redis가 지원하지 않는 명령:**

| **connection 패밀리** | **geo 패밀리** | **keys 패밀리** | **server 패밀리** | **strings 패밀리** |
| --- | --- | --- | --- | --- |
| swapdb | geoadd | touch |  bgrewriteaof | bitfield |
| -　 | geohash |  restore |  bgsave |- 　 |
| -　 | geopos |  object |  client kill | -　 |
| -　 | geodist |  unlink |  sync | -　 |
| -　 | georadius |  wait | client getname | -　 |
| -　 | georadiusbymember | migrate | client pause |- 　 |
| -　 | -　 | dump | client reply | -　 |
| -　 | -　 |  -　 | client setname |- 　 |
| -　 | -　 |  -　 |  command count | -　 |
| -　 | -　 | - 　 |  command getkeys | -　 |
| -　 | -　 |  -　 | command info |- 　 |
| -　 | -　 |  -　 | slaveof | -　 |
| -　 | -　 | -　 | config rewrite |- 　 |
| -　 | -　 | - 　 |  config set | 　- |
| -　 | -　 |  - | config resetstat | -　 |
| -　 | -　 |  -　 |  debug object | -　 |
| -　 | -　 |  -　 | debug segfault | -　 |
| -　 | -　 | -　 | role  | -　 |
| -　 | -　 | -　 | save  | -　 |
| -　 | -　 | -　 | lastsave |- 　 |
| -　 | -　 |  -　 | shutdown  | -　 |

    



