Redis 클러스터 버전(CKV)은 더블 복제본 세트 클러스터 버전 인스턴스를 제공하며 단선 스레드 병목현상을 극복하고 대용량 또는 고성능 비즈니스 수요를 최대적으로 만족시킬 수 있습니다. 클러스터 버전은 Redis 3.2 버전의 프로토콜 및 명령과 호환하며, 최대 128개의 샤딩을 지원하고 12GB - 48TB 용량을 지원합니다.

## 기능 특성
- **강력한 서비스**
이중 서버 마스터/슬레이브 아키텍처를 채택하며, 마스터/슬레이브 노드는 다른 물리적 기기에 위치합니다. 마스터 노드는 외부 접근을 지원하며, 사용자는 Redis 명령행과 공용 클라이언트를 통해 데이터를 추가, 삭제, 수정 및 조회할 수 있고 슬레이브 노드는 데이터 백업 및 고가용성을 제공합니다. 서버 노드가 고장날 경우, 자체 연구한 HA 시스템이 마스터/슬레이브 전환을 자동으로 진행하여 비즈니스를 안정적으로 실행할 수 있도록 확보합니다.        
- **믿을 만한 데이터**
데이터 지속화 기능을 기본적으로 활성화하고 데이터는 모두 디스크로 저장합니다. 마스터/슬레이브 버전은 데이터 백업 기능을 지원하며, 사용자는 백업 세트에 대해 인스턴스 롤백 또는 클론 등 작업을 진행할 수 있으며 데이터 오작동 등 문제를 효과적으로 해결할 수 있습니다.
- **저지연**
CKV는 고성능 네트워크 플랫폼 및 Proxy 없는 아키텍처를 채택하며 접근 지연과 네트워크 지연을 크게 감소합니다. 높은 부하 시나리오에서 지연은 최대 60%까지 감소할 수 있습니다.
- **슬레이브 읽기 전용**
CKV 마스터/슬레이브 버전은 슬레이브를 사용하여 읽기 성능을 향상시킵니다. 평균적인 상황에서 40%의 읽기 성능을 향상시킬 수 있으며, CKV 마스터/슬레이브 버전은 기본적으로 슬레이브 읽기 전용을 사용하지 않습니다. 현재는 티켓을 제출하여 슬레이브 읽기 전용을 신청할 수 있습니다. CKV 마스터 노드와 슬레이브 노드에 복제 지연이 존재하여, 슬레이브 읽기 전용을 활성화한 후에 구식 버전 데이터를 읽을 가능성이 있습니다. 이 기능을 활성화하기 전에 비즈니스가 읽기 데이터의 불일치를 받아들일 수 있는지 확인하십시오.
- **원활한 업그레이드**
CKV 클러스터 버전은은 독창적인 솔루션을 통해 비즈니스에 영향울 끼치지 않도록 버전을 업그레이드할 수 있어, 서비스의 가용성을 최대하게 보장합니다.

## 적용 시나리오
- **단일 인스턴스에 데이터량이 큰 경우**
클러스터 버전은 분산형 아키텍처로 단일 인스턴스에 용량이 비교적 큰 시나리오에 적합합니다. 용량은 CKV 마스터/슬레이브 버전의 384GB 한도를 초과할 수 있습니다.
- **QPS 및 동시 발생 요구가 높은 경우**
클러스터 버전은 분산형 아키텍차로서 읽기/쓰기를 여러 노드에 할당하고 Key 분포가 균등한 상황에서 QPS는 노드 수에 따라 선형으로 높아지며, 현재 최대 128개 샤딩, 천만 수준의 QPS 성능을 지원합니다.
- **민감하지 않는 프로토콜**
오픈 소스 버전과 비교할 때, 클러스터 버전은 지원하는 프로토콜의 측면에서 소량의 프로토콜을 지원하지 않습니다.

##  연결 예시
CKV 클러스터 버전은 “인스턴스 ID: 비밀번호”의 형식만 지워합니다. 예를 들어 인스턴스 ID는 crs-bkuza6i3이고, 설정한 비밀번호는 abcd1234인 경우, 연결 명령은 `redis-cli -h IP 주소 -p 포트 -a crs-bkuza6i3:abcd1234`입니다.


##  사용 제한
- CKV 엔진의 pttl 설정의 최소 표시 단위는 초이고 Redis 커뮤니티 버전과 일치하지 않습니다.
- 현재 지원하는 string 유형은 Key이고 Value 최대 크기는 32MB로 Redis 커뮤니티 버전과 일치하지 않습니다.
- mset, mget 배치 작업이 제한을 받지 않는 것을 제외하고 기타 배치 작업은 배치의 Key가 동일한 slot에 있어야 합니다. 그렇지 않을 경우, 오류를 보고하고 `CROSSSLOT Keys in request don't hash to the same slot`을 표시합니다.
- 샤딩이 가득 찼을 경우, subscribe, psubscribe는 일정 메모리를 점용해야 합니다. 새로 생성된 구독은 영향을 받게 되며, 이미 구독한 channel의 publish는 영향을 받지 않습니다.

## 특수 설명
- 현재 클러스터 버전 단일 샤딩의 크기는 기본적으로 4GB입니다. 단일 key의 value 크기는 4Gb를 초과하지 않길 권장합니다.
- 현재 클러스터 버전은 클러스터 차원의 모니터링을 제공합니다.


## 호환성

**클러스터 버전이 지원하는 명령**:
 
| **connection 패밀리** | **geo 패밀리** | **hashes 패밀리** | **hyperloglog 패밀리** | **keys 패밀리** | **lists 패밀리** | **pub/sub 패밀리** | 
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

|**sets 패밀리** | **sorted sets 패밀리** | **strings 패밀리** | **transactions 패밀리** |**server 패밀리** | 
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

**클러스터 버전이 지원하지 않는 명령:**

| **cluster 패밀리** | **connection 패밀리** | **keys 패밀리** | **lists 패밀리** | **scripting 패밀리** | **server 패밀리** | **strings 패밀리** |
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



