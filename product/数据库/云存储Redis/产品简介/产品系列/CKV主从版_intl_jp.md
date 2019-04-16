Redis マスタースレーブ版（CKV）は、マスタースレーブノード配置アーキテクチャを取り入れ、データの永続化とバックアップを提供します。データの信頼性、可用性の両方が求められるシナリオに適しています。
マスターノードは日常のサービスへのアクセスに対応し、スレーブノードは HA に対応します。マスターノードが故障した場合、システムは自動でスレーブノードに切り換わるため、サービスを安定した状態で運営できます。CKV マスタースレーブ版は、Redis バージョン 3.2 のコマンドおよびプロトコルと互換性があります。4GB ～ 384GBの仕様をサポートするため、大容量メモリのニーズに応えます。
![](https://main.qcloudimg.com/raw/9d31769110caed41693a5f2f82a0f03c.png)

## 機能の特性
- **信頼できるサービス**
デュアルマシンマスタースレーブアーキテクチャを採用し、マスターとスレーブのノードが異なる物理マシンにあります。マスターノードは外部にアクセスを提供し、ユーザーは Redis コマンドラインと通常のクライアントを通してデータの追加や削除、変更や照会などをすることができます。スレーブノードはデータのバックアップと高い可用性を提供します。マスターノードが故障した場合、自社開発による HA システムが自動でマスター/スレーブの切り替えを行い、安定してサービスを実行できるようにします。        
- **信頼できるデータ**
初期設定の状態でデータの永続化機能がオンになっているため、データは全てディスクに保存されます。データバックアップ機能に対応しているため、ユーザーはバックアップセットに対してインスタンスのロールバックやクローン作成を行うことができます。それにより、データの誤操作などの問題を効果的に解決します。
- **遅延を少なく**
CKV は高パフォーマンスのネットワークプラットフォームを採用し、Proxy アーキテクチャがないため、アクセス遅延とネットワーク遅延が大幅に減少します。高負荷のシナリオで、遅延は最大60%も減少します。
- **スレーブ読み取り専用**
CKV マスタースレーブ版は、スレーブを作動させることで読み取り性能を大きく向上させることができ、一般的な状況で読み取り性能が40%向上します。CKV マスタースレーブ版は、初期設定の状態ではスレーブの読み取り専用が作動していません。現在、 [作業指示の送信](https://console.cloud.tencent.com/workorder/category) でスレーブの読み取り専用を申請できます。CKV マスターノードとスレーブノードにコピーの遅延があることにより、スレーブの読み取り専用をオンにした後、旧バージョンのデータを読み取ってしまうことがあります。この機能をオンにする前に、読み取りデータが一致しないことでサービスに問題が起こらないかを確認してください。
- **スムーズなアップグレード**
CKV マスタースレーブ版では、独自の手法によって、サービスが感知することなくバージョンをアップグレードすることが可能です。そのため、サービスの可用性を最大限に引き出します。



## 使用制限

- CKV マスタースレーブ版は最大で12万 QPS をサポートします。より高いパフォーマンスが必要な場合、 CKV または Redis クラスタ版を選択していただくと、数千万 QPS に対応可能です。
- CKV エンジンの pttl 設定の最小表示単位は秒です。コミュニティ版とは異なります。
- 現在 string 型の Key をサポートし、Value の最大 Size は32MBです。
- インスタンスの接続方式は“インスタンス ID:パスワード”です。Redis スタンドアロン版、マスタースレーブ版、クラスタ版の接続方式とは異なります。
- `dbsize` コマンドが実現する時間複雑度を O(n)とし、コマンド実行時には、現在の DB の全ての Key を走査する必要があります。慎重に使用してください。
- string 型の Keyである`{ckv_plus_pub_sub}_patterns`が内蔵され、このKey は pub、sub のサブスクリプション機能をサポートするために使用します。サブスクリプション機能を使用する場合、この Key を削除しないでください。削除した場合、サブスクリプションは無効になります。
- 現在、イベント通知は期限切れの通知や廃棄ポリシーの通知に対応していません。
- 廃棄ポリシーについては現在、`volatile-lru`のみをサポートするか、廃棄メカニズムを無効にします。対応するパラメータは、`maxmemory-policy`です。


## 接続サンプル
CKV マスタースレーブ版は、“インスタンス ID:パスワード”のパスワード形式にのみ対応しています。インスタンス ID が crs-bkuza6i3、設定したパスワードが abcd1234 である場合、接続コマンドは`redis-cli -h IP アドレス -p ポート -a crs-bkuza6i3:abcd1234`となります。

## 互換性
**CKV マスタースレーブ版がサポートするコマンド**

| **connection グループ** | **geo グループ** | **hashes グループ** | **hyperloglog グループ** | **keys グループ** | **lists グループ** | **pub/sub グループ** | **server グループ** | 
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


|**sets グループ** | **sorted sets グループ** | **strings グループ** | **transactions グループ** | **scripting グループ** |
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

**CKV マスタースレーブ版がサポートしていないコマンド**

| **cluster グループ** | **connection グループ** | **keys グループ** | **lists グループ** | **scripting グループ** | **server グループ** | **strings グループ** |
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
