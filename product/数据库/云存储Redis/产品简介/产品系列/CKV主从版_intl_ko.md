Redis 마스터/슬레이브 버전(CKV)은 마스터/슬레이브 노드 배포 아키텍처를 채택하며 데이터 지속화와 백업을 제공하며 데이터 신뢰성, 가용성이 모두 요구되는 시나리오에 적합합니다.
마스터 노드는 일상 서비스 접근을 제공하며, 슬레이브 노드는 HA를 제공합니다. 마스터 노드가 고장날 경우, 시스템은 슬레이브 노드로 자동으로 전환하여 비즈니스를 안정적으로 운행할 수 있도록 확보합니다. CKV 마스터/슬레이브 버전은 Redis 3.2 버전의 명령과 프로토콜을 호환하며, 4GB - 384GB 사양을 지원하고 대용량 스토리지 수요를 만족시킵니다.
![](https://main.qcloudimg.com/raw/9d31769110caed41693a5f2f82a0f03c.png)

## 기능 특성
- **강력한 서비스**
이중 서버 마스터/슬레이브 아키텍처를 채택하며, 마스터/슬레이브 노드는 다른 물리적 기기에 위치합니다. 마스터 노드는 외부 접근을 지원하며, 사용자는 Redis 명령행과 공용 클라이언트를 통해 데이터를 추가, 삭제, 수정 및 조회할 수 있고 슬레이브 노드는 데이터 백업 및 고가용성을 제공합니다. 서버 노드가 고장날 경우, 자체 연구한 HA 시스템이 마스터/슬레이브 전환을 자동으로 진행하여 비즈니스를 안정적으로 실행할 수 있도록 확보합니다.        
- **믿을 만한 데이터**
데이터 지속화 기능을 기본적으로 활성화하고 데이터는 모두 디스크로 저장합니다. 마스터/슬레이브 버전은 데이터 백업 기능을 지원하며, 사용자는 백업 세트에 대해 인스턴스 롤백 또는 클론 등 작업을 진행할 수 있으며 데이터 오작동 등 문제를 효과적으로 해결할 수 있습니다.
- **저지연**
CKV는 고성능 네트워크 플랫폼 및 Proxy 없는 아키텍처를 채택하며 접근 지연과 네트워크 지연을 크게 감소합니다. 높은 부하 시나리오에서 지연은 최대 60%까지 감소할 수 있습니다.
- **슬레이브 읽기 전용**
CKV 마스터/슬레이브 버전은 슬레이브 시작을 통해 읽기 성능을 향상시킵니다. 평균적인 상황에서 40%의 읽기 성능을 향상시킬 수 있으며, CKV 마스터/슬레이브 버전은 기본적으로 슬레이브 읽기 전용을 시작하지 않습니다. 현재는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)로 슬레이브 읽기 전용을 신청할 수 있습니다. CKV 마스터 노드와 슬레이브 노드가 복제 지연이 존재할 경우, 슬레이브 읽기 전용 활성화 이후 구 버전 데이터의 상황을 읽게 됩니다. 이 기능을 활성화하기 전 비즈니스가 읽기 데이터가 일치하지 않는 상황을 받아들일 수 있는지 확인하십시오.
- **원활한 업그레이드**
CKV 마스터/슬레이브 버전은 독창적인 솔루션을 통해 비즈니스에 영향울 끼치지 않도록 버전을 업그레이드할 수 있어, 서비스의 가용성을 최대하게 보장합니다.



## 사용 제한

- CKV 마스터/슬레이브 버전 성능은 최대 12만 QPS를 지원하며, 더 고성능이 필요할 경우 CKV 또는 Redis 클러스터 버전을 선택하십시오. 천만 수준의 QPS를 지원할 수 있습니다.
- CKV 엔진의 pttl 설정의 최소 표시 단위는 초이고 커뮤니티 버전과 일치하지 않습니다.
- 현재 string 유형의 Key를 지원하며 Value 최대 크기는 32MB입니다.
- 인스턴스 연결 방식은 “인스턴스 ID: 비밀번호”이며 Redis 스탠드 얼로운, 마스터/슬레이브, 클러스터 버전의 연결 방식과 일치하지 않습니다.
- `dbsize` 명령 구현의 시간 복잡도는 O(n)이며 명령 실행 시 현재 DB의 모든 Key를 순회해야 합니다. 신중히 사용하십시오.
- string 유형의 Key: `{ckv_plus_pub_sub}_patterns`를 를 보유하고 있습니다. 이 Key는 pub, sub 구독 기능에 사용됩니다. 구독 기능을 사용해야 할 경우, 이 Key를 삭제하지 마십시오. 그렇지 않으면 구독이 무효화될 수 있습니다.
- 이벤트 알림은 만료와 제거 전략 알림을 지원하지 않습니다.
- 제거 전략은 현재 `volatile-lru`만 지원합니다. 또는 제거 메커니즘이 종료할 수 있고 해당 매개변수는 `maxmemory-policy`입니다.


##  연결 예시
CKV 마스터/슬레이브 버전은 “인스턴스 ID: 비밀번호”의 형식만 지워합니다. 예를 들어 인스턴스 ID는 crs-bkuza6i3이고, 설정한 비밀번호는 abcd1234인 경우, 연결 명령은 `redis-cli -h IP 주소 -p 포트 -a crs-bkuza6i3:abcd1234`입니다.

## 호환성
**CKV 마스터/슬레이브 버전이 지원하는 명령:**

| **connection 패밀리** | **geo 패밀리** | **hashes 패밀리** | **hyperloglog 패밀리** | **keys 패밀리** | **lists 패밀리** | **pub/sub 패밀리** | **server 패밀리** | 
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


|**sets 패밀리** | **sorted sets 패밀리** | **strings 패밀리** | **transactions 패밀리** | **scripting 패밀리** |
| --- | --- | --- | --- | --- |
| sadd | zadd | append | discard |eval|
| scard | zcard | bitcount | exec |script debug|
| sdiff | zcount | bitop | multi |script exists|
| sdiffstore | zincrby | bitpos | unwatch |script flush|
| sinter | zinterstore | decr | watch |script kill|
| sinterstore | zlexcount | decrby | -　 |script load |
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
| -　 | zscan | setbit | -　 |-
| -　 | zscore | setex | -　 |-
| -　 | zunionstore | setnx | -　 |-
| -　 | -　 | setrange |- 　 |-
| -　 | -　 | strlen | -　 |-

**CKV 마스터/슬레이브 버전이 지원하지 않는 명령:**

| **cluster 패밀리** | **connection 패밀리** | **keys 패밀리** | **lists 패밀리** | **scripting 패밀리** | **server 패밀리** | **strings 패밀리** |
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

