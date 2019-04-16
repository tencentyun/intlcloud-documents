Redis マスタースレーブ版（コミュニティ）は、最も標準的な Redis のバージョンです。Redis バージョン2.8 のプロトコルおよびコマンドと互換性があり、マスタースレーブノード配置アーキテクチャを取り入れて、データの永続化とバックアップを可能にしました。データの信頼性、可用性の両方が求められるシナリオに適しています。マスターノードは日常のサービスへのアクセスに対応し、スレーブノードは HA の可用性の高さを提供します。マスターノードが故障した場合、システムは自動でスレーブノードに切り換わるため、サービスを安定した状態で運営できます。
![](https://main.qcloudimg.com/raw/37626b6980e25a1ddf4fd3efcf4bbd4a.png)

## 機能の特性
- **信頼できるサービス**
デュアルマシンマスタースレーブアーキテクチャを採用し、マスターとスレーブのノードが異なる物理マシンにあります。マスターノードは外部にアクセスを提供し、ユーザーは Redis コマンドラインと通常のクライアントを通してデータの追加や削除、変更や照会などをすることができます。マスターノードが故障した場合、自社開発による HA システムが自動でマスター/スレーブの切り替えを行い、安定してサービスを実行できるようにします。        
- **信頼できるデータ**
初期設定の状態で、データの永続化機能が作動しています。マスタースレーブ版はデータバックアップ機能に対応しているため、ユーザーはバックアップセットに対してインスタンスのロールバックやクローン作成を行うことができます。それにより、データの誤操作などの問題を効果的に解決します。

## 使用制限
- Redis マスタースレーブ版は0.25GB ～ 60GBの仕様をサポートしています。より大きなマスタースレーブ版の仕様が必要な場合、CKVマスタースレーブ版を選択していただくと最大で 384GB、クラスタ版なら最大で48TBの容量をサポートできます。
- Redis マスタースレーブ版は最大で10万 QPS をサポートします。より高い QPS が必要な場合、Redis クラスタ版または CKV クラスタ版を選択していただくと、数千万 QPS に対応可能です。

## 互換性
TencentDB for Redis マスタースレーブ版は、Redis 2.8 のプロトコルおよびコマンドと互換性があります。自己構築した Redis データベースは、スムーズに Redis スタンダード版に移行できます。また、データ転送ツール（DTS）は、増分した Redis の移行を行うことができるため、サービスの安定した移行を保証します。

>?2018年11月1日以前に購入したインスタンスは、client list、monitor、scritp コマンドをサポートしていません。使用したい場合、 [作業指示の送信](https://console.cloud.tencent.com/workorder/category) を申請してください。

**マスタースレーブ版 Redis がサポートするコマンド**

| **connection グループ** | **hashes グループ** | **keys グループ** | **lists グループ** | **pub/sub グループ** | **server グループ** | 
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


|**sets グループ** | **sorted sets グループ** | **strings グループ** | **transactions グループ** |**hyperloglog グループ** |**scripting グループ** |
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

**マスタースレーブ版 Redis がサポートしていないコマンド**

| **connection グループ** | **geo グループ** | **keys グループ** | **server グループ** | **strings グループ** |
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

    


