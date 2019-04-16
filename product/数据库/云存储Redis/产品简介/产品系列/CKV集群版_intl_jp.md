Redis クラスタ版（CKV）は、デュアルコピーによるクラスタ版インスタンスを提供します。シングルスレッドの限界を解決しているため、大容量または高パフォーマンスのサービスに最適です。クラスタ版は Redis バージョン 3.2 のプロトコルおよびコマンドと互換性があり、最大で128のシャード、12GB～48TBの容量をサポートします。

## 機能の特性
- **信頼できるサービス**
デュアルマシンマスタースレーブアーキテクチャを採用し、マスターとスレーブのノードが異なる物理マシンにあります。マスターノードは外部にアクセスを提供し、ユーザーは Redis コマンドラインと通常のクライアントを通してデータの追加や削除、変更や照会をすることができます。スレーブノードはデータのバックアップと高い可用性を提供します。マスターノードが故障した場合、自社開発による HA システムが自動でマスター/スレーブの切り替えを行い、安定してサービスを実行できるようにします。        
- **信頼できるデータ**
初期設定の状態でデータの永続化機能がオンになっているため、データは全てディスクに保存されます。データバックアップ機能に対応しているため、ユーザーはバックアップセットに対してインスタンスのロールバックやクローン作成を行うことができます。それにより、データの誤操作などの問題を効果的に解決します。
- **遅延を少なく**
CKV は高パフォーマンスのネットワークプラットフォームを採用し、Proxy アーキテクチャがないため、アクセス遅延とネットワーク遅延が大幅に減少します。高負荷のシナリオで、遅延は最大60%も減少します。
- **スレーブ読み取り専用**
CKV クラスタ版は、スレーブを作動させることで読み取り性能を大きく向上させることができ、一般的な状況で読み取り性能が40%向上します。CKV クラスタ版は、初期設定の状態ではスレーブの読み取り専用が作動していません。現在、スレーブの読み取り専用を申請することができます。CKV マスターノードとスレーブノードにコピーの遅延があることにより、スレーブの読み取り専用をオンにした後、旧バージョンのデータを読み取ってしまうことがあります。この機能をオンにする前に、読み取りデータが一致しないことでサービスに問題が起こらないかを確認してください。
- **スムーズなアップグレード**
CKV クラスタ版では、独自の手法によって、サービスが感知することなくバージョンをアップグレードすることが可能です。そのため、サービスの可用性を最大限に引き出します。

## 適したシナリオ
- **1つのインスタンスのデータ量が多い場合**
クラスタ版は分散アーキテクチャです。1つのインスタンスの容量が大きいシナリオに適しており、容量は CKV マスタースレーブ版の384GBの上限を超えることが可能です。
- **QPS と平行性の要件が高い場合**
クラスタ版は分散アーキテクチャのため、読み取りと書き込みが複数のノードに分散しています。Key 分散が均一な状況で、QPS はノード数に従って直線的に増加し、現在は最大で128のシャード、数千万レベルの QPS 性能をサポートしています。
- **プロトコルサポートにこだわらない場合**
オープンソース版と比較すると、クラスタ版はプロトコルサポートにおいてサポートしていないプロトコルがいくつかあります。

## 接続サンプル
CKV クラスタ版は、“インスタンス ID:パスワード”のパスワード形式にのみ対応しています。インスタンス ID が crs-bkuza6i3、設定したパスワードが abcd1234 である場合、接続コマンドは`redis-cli -h IP アドレス -p ポート -a crs-bkuza6i3:abcd1234`となります。


##  使用制限
- CKV エンジンの pttl 設定の最小表示単位は秒です。コミュニティ版 Redis とは異なります。
- 現在サポートする string 型 Key は、Value の最大 Size が32MBです。コミュニティ版 Redis とは異なります。
- mset、mget の一括操作が制限を受けないことを除き、その他の一括操作では全てバッチ Key が同一 slot 内にあることが求められます。それ以外の場合はエラーとなり、`CROSSSLOT Keys in request don't hash to the same slot`と表示されます。
- シャード全体に書き込んだ後、subscribe、psubscribe は一定のメモリを占有する必要があります。追加した新しいサブスクリプションは影響を受けますが、既に channel をサブスクリプションした publish は影響を受けません。

##  特別説明
- 現在、クラスタ版のシャード1つのサイズはデフォルトで4GBです。そのため、1つの key の value サイズを4GB以内とすることをお勧めします。
- 現在、クラスタ版はクラスタディメンションの監視に対応しています。


## 互換性

**クラスタ版がサポートするコマンド**
 
| **connection グループ** | **geo グループ** | **hashes グループ** | **hyperloglog グループ** | **keys グループ** | **lists グループ** | **pub/sub グループ** | 
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

|**sets グループ** | **sorted sets グループ** | **strings グループ** | **transactions グループ** |**server グループ** | 
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

**クラスタ版がサポートしていないコマンド**

| **cluster グループ** | **connection グループ** | **keys グループ** | **lists グループ** | **scripting グループ** | **server グループ** | **strings グループ** |
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


