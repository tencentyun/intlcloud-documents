### Command Compatibility of Different Editions
In the following table, ✓ indicates "supported", x indicates "unsupported", and - indicates that cross-slot access is not applicable to the command.
For custom command descriptions, please see [Hybrid Storage Edition > Custom commands](https://intl.cloud.tencent.com/document/product/1083/39296).


| Command Group          | Command                  | Storage Edition   | Hybrid Storage Edition |Cross-slot Support in Cluster Architecture |
| --------------- | --------------------- | -------- | ---------- | ------------------- |
| connection group   | auth                  | &#10003; | &#10003;   | -                   |
| connection group   | echo                  | &#10003; | &#10003;   | -                   |
| connection group   | ping                  | Custom   | Custom     | -                   |
| connection group   | quit                  | &#10003; | &#10003;   | -                   |
| connection group   | select                | &#10003; | &#10003;   | -                   |
| connection group   | swapdb                | x        | &#10003;   | -                   |
| hash group         | hdel                  | &#10003; | &#10003;   | -                   |
| hash group         | hexists               | &#10003; | &#10003;   | -                   |
| hash group         | hget                  | &#10003; | &#10003;   | -                   |
| hash group         | hgetall               | &#10003; | &#10003;   | -                   |
| hash group         | hincrby               | &#10003; | &#10003;   | -                   |
| hash group         | hincrbyfloat          | &#10003; | &#10003;   | -                   |
| hash group         | hkeys                 | &#10003; | &#10003;   | -                   |
| hash group         | hlen                  | &#10003; | &#10003;   | -                   |
| hash group         | hmget                 | &#10003; | &#10003;   | -                   |
| hash group         | hmset                 | &#10003; | &#10003;   | -                   |
| hash group         | hset                  | &#10003; | &#10003;   | -                   |
| hash group         | hsetnx                | &#10003; | &#10003;   | -                   |
| hash group         | hstrlen               | &#10003; | &#10003;   | -                   |
| hash group         | hvals                 | &#10003; | &#10003;   | -                   |
| hash group         | hscan                  | x   | x     | x                  |
| keys group         | del                   | &#10003; | &#10003;   | &#10003;            |
| keys group         | scan                  | x   | x     | x                  |
| keys group         | exists                | &#10003; | &#10003;   | x                   |
| keys group         | expire                | &#10003; | &#10003;   | -                   |
| keys group         | expireat              | &#10003; | &#10003;   | -                   |
| keys group         | keys                  | Custom   | Custom     | -                   |
| keys group         | type                  | &#10003; | &#10003;   | -                   |
| keys group         | move                  | &#10003; | &#10003;   | -                   |
| keys group         | ttl                   | &#10003; | &#10003;   | -                   |
| keys group         | persist               | &#10003; | &#10003;   | -                   |
| keys group         | pexpire               | &#10003; | &#10003;   | -                   |
| keys group         | pexpireat             | &#10003; | &#10003;   | -                   |
| keys group         | pttl                  | &#10003; | &#10003;   | -                   |
| keys group         | randomkey             | x        | &#10003;   | -                   |
| keys group         | rename                | &#10003; | &#10003;   | x                   |
| keys group         | renamenx              | &#10003; | &#10003;   | x                   |
| keys group         | sort                  | &#10003; | &#10003;   | -                   |
| keys group         | touch                 | x        | &#10003;   | -                   |
| keys group         | restore               | &#10003; | &#10003;   | -                   |
| keys group         | object                | x        | x          | -                   |
| keys group         | unlink                | &#10003; | &#10003;   | x                   |
| keys group         | wait                  | x        | x          | -                   |
| keys group         | migrate               | x        | x          | -                   |
| keys group         | dump                  | &#10003; | &#10003;   | -                   |
| list group         | lindex                | &#10003; | &#10003;   | -                   |
| list group         | linsert               | &#10003; | &#10003;   | -                   |
| list group         | llen                  | &#10003; | &#10003;   | -                   |
| list group         | lpop                  | &#10003; | &#10003;   | -                   |
| list group         | lpush                 | &#10003; | &#10003;   | -                   |
| list group         | lpushx                | &#10003; | &#10003;   | -                   |
| list group         | lrange                | &#10003; | &#10003;   | -                   |
| list group         | lrem                  | &#10003; | &#10003;   | -                   |
| list group         | lset                  | &#10003; | &#10003;   | -                   |
| list group         | ltrim                 | &#10003; | &#10003;   | -                   |
| list group         | rpop                  | &#10003; | &#10003;   | -                   |
| list group         | rpoplpush             | &#10003; | &#10003;   | x                   |
| list group         | rpush                 | &#10003; | &#10003;   | -                   |
| list group         | rpushx                | &#10003; | &#10003;   | -                   |
| list group         | blpop                 | x        | &#10003;   | x                   |
| list group         | brpop                 | x        | &#10003;   | x                   |
| list group         | brpoplpush            | x        | &#10003;   | x                   |
| pub/sub group      | psubscribe            | &#10003; | &#10003;   | -                   |
| pub/sub group      | pubsub                | &#10003; | &#10003;   | -                   |
| pub/sub group      | publish               | &#10003; | &#10003;   | -                   |
| pub/sub group      | punsubscribe          | &#10003; | &#10003;   | -                   |
| pub/sub group      | subscribe             | &#10003; | &#10003;   | -                   |
| pub/sub group      | unsubscribe           | &#10003; | &#10003;   | -                   |
| sets group         | sadd                  | &#10003; | &#10003;   | -                   |
| sets group         | scard                 | &#10003; | &#10003;   | -                   |
| sets group         | sdiff                 | &#10003; | &#10003;   | x                   |
| sets group         | sdiffstore            | &#10003; | &#10003;   | x                   |
| sets group         | sinter                | &#10003; | &#10003;   | x                   |
| sets group         | sinterstore           | &#10003; | &#10003;   | x                   |
| sets group         | sismember             | &#10003; | &#10003;   | -                   |
| sets group         | smembers              | &#10003; | &#10003;   | -                   |
| sets group         | smove                 | &#10003; | &#10003;   | x                   |
| sets group         | spop                  | &#10003; | &#10003;   | -                   |
| sets group         | srandmember           | &#10003; | &#10003;   | -                   |
| sets group         | srem                  | &#10003; | &#10003;   | -                   |
| sets group         | sscan                 | &#10003; | &#10003;   | -                   |
| sets group         | sunion                | &#10003; | &#10003;   | x                   |
| sets group         | sunionstore           | &#10003; | &#10003;   | x                   |
| sorted sets group  | zadd                  | &#10003; | &#10003;   | -                   |
| sorted sets group  | zcard                 | &#10003; | &#10003;   | -                   |
| sorted sets group  | zcount                | &#10003; | &#10003;   | -                   |
| sorted sets group  | zincrby               | &#10003; | &#10003;   | -                   |
| sorted sets group  | zinterstore           | &#10003; | &#10003;   | x                   |
| sorted sets group  | zlexcount             | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrange                | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrangebylex           | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrangebyscore         | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrank                 | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrem                  | &#10003; | &#10003;   | -                   |
| sorted sets group  | zremrangebylex        | &#10003; | &#10003;   | -                   |
| sorted sets group  | zremrangebyrank       | &#10003; | &#10003;   | -                   |
| sorted sets group  | zremrangebyscore      | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrevrange             | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrevrangebylex        | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrevrangebyscore      | &#10003; | &#10003;   | -                   |
| sorted sets group  | zscore                | &#10003; | &#10003;   | -                   |
| sorted sets group  | zrevrank              | &#10003; | &#10003;   | -                   |
| sorted sets group  | zscan                 | &#10003; | &#10003;   | -                   |
| sorted sets group  | zunionstore           | &#10003; | &#10003;   | x                   |
| sorted sets group  | zpopmax               | x        | x          | -                   |
| sorted sets group  | zpopmin               | x        | x          | -                   |
| sorted sets group  | bzpopmax              | x        | x          | -                   |
| sorted sets group  | bzpopmin              | x        | x          | -                   |
| strings group      | append                | &#10003; | &#10003;   | -                   |
| strings group      | bitcount              | &#10003; | &#10003;   | -                   |
| strings group      | bitop                 | &#10003; | &#10003;   | x                   |
| strings group      | bitpos                | &#10003; | &#10003;   | -                   |
| strings group      | decr                  | &#10003; | &#10003;   | -                   |
| strings group      | decrby                | &#10003; | &#10003;   | -                   |
| strings group      | get                   | &#10003; | &#10003;   | -                   |
| strings group      | getbit                | &#10003; | &#10003;   | -                   |
| strings group      | getrange              | &#10003; | &#10003;   | -                   |
| strings group      | getset                | &#10003; | &#10003;   | -                   |
| strings group      | incr                  | &#10003; | &#10003;   | -                   |
| strings group      | incrby                | &#10003; | &#10003;   | -                   |
| strings group      | incrbyfloat           | &#10003; | &#10003;   | -                   |
| strings group      | mget                  | &#10003; | &#10003;   | &#10003;            |
| strings group      | mset                  | &#10003; | &#10003;   | &#10003;            |
| strings group      | msetnx                | &#10003; | &#10003;   | x                   |
| strings group      | psetex                | &#10003; | &#10003;   | -                   |
| strings group      | setex                 | &#10003; | &#10003;   | -                   |
| strings group      | set                   | &#10003; | &#10003;   | -                   |
| strings group      | setbit                | &#10003; | &#10003;   | -                   |
| strings group      | setnx                 | &#10003; | &#10003;   | -                   |
| strings group      | setrange              | &#10003; | &#10003;   | -                   |
| strings group      | strlen                | &#10003; | &#10003;   | -                   |
| strings group      | bitfield              | &#10003; | &#10003;   | -                   |
| transactions group | discard               | &#10003; | &#10003;   | -                   |
| transactions group | exec                  | &#10003; | &#10003;   | -                   |
| transactions group | multi                 | &#10003; | &#10003;   | -                   |
| transactions group | unwatch               | &#10003; | &#10003;   | -                   |
| transactions group | watch                 | &#10003; | &#10003;   | -                   |
| hyperloglog group  | pfadd                 | &#10003; | &#10003;   | -                   |
| hyperloglog group  | pfcount               | &#10003; | &#10003;   | x                   |
| hyperloglog group  | pfmerge               | &#10003; | &#10003;   | x                   |
| scripting group    | eval                  | &#10003; | &#10003;   | x                   |
| scripting group    | evalsha               | &#10003; | &#10003;   | x                   |
| scripting group    | script debug          | &#10003; | &#10003;   | -                   |
| scripting group    | script exists         | &#10003; | &#10003;   | x                   |
| scripting group    | script flush          | &#10003; | &#10003;   | -                   |
| scripting group    | script load           | &#10003; | &#10003;   | -                   |
| scripting group    | script kill           | &#10003; | &#10003;   | -                   |
| geo group          | geoadd                | x        | &#10003;   | -                   |
| geo group          | geohash               | x        | &#10003;   | -                   |
| geo group          | geopos                | x        | &#10003;   | -                   |
| geo group          | geodist               | x        | &#10003;   | -                   |
| geo group          | georadius             | x        | &#10003;   | -                   |
| geo group          | georadiusbymember     | x        | &#10003;   | -                   |
| server group       | bgrewriteaof          | x        | x          | -                   |
| server group       | bgsave                | x        | x          | -                   |
| server group       | client kill           | x        | x          | -                   |
| server group       | sync                  | x        | x          | -                   |
| server group       | psync                 | x        | x          | -                   |
| server group       | client list           | &#10003; | &#10003;   | -                   |
| server group       | client getname        | x        | x          | -                   |
| server group       | client pause          | x        | x          | -                   |
| server group       | client reply          | x        | x          | -                   |
| server group       | client setname        | x        | x          | -                   |
| server group       | command count         | x        | x          | -                   |
| server group       | command getkeys       | x        | x          | -                   |
| server group       | command info          | x        | x          | -                   |
| server group       | slaveof               | x        | x          | -                   |
| server group       | config rewrite        | x        | x          | -                   |
| server group       | config set            | x        | x          | -                   |
| server group       | config resetstat      | x        | x          | -                   |
| server group       | debug object          | x        | x          | -                   |
| server group       | debug segfault        | x        | x          | -                   |
| server group       | role                  | x        | x          | -                   |
| server group       | save                  | x        | x          | -                   |
| server group       | lastsave              | x        | x          | -                   |
| server group       | shutdown              | x        | x          | -                   |
| server group       | MEMORY                | x        | Custom     | -                   |
| server group       | command               | &#10003; | &#10003;   | -                   |
| server group       | dbsize                | &#10003; | &#10003;   | -                   |
| server group       | info                  | Custom   | Custom     | -                   |
| server group       | time                  | &#10003; | &#10003;   | -                   |
| server group       | client list           | &#10003; | &#10003;   | -                   |
| server group       | config get            | &#10003; | &#10003;   | -                   |
| server group       | monitor               | Custom   | Custom     | -                   |
| server group       | flushdb               | Custom   | Custom     | -                   |
| server group       | flushall              | &#10003; | &#10003;   | -                   |
| server group       | slowlog               | Custom   | Custom     | -                   |
| server group       | cluster keyslot       | &#10003; | &#10003;   | -                   |
| server group       | cluster nodes         | &#10003; | &#10003;   | -                   |
| server group       | cluster getkeysinslot | &#10003; | &#10003;   | -                   |
| server group       | cluster (others)          | x        | x          | -                   |
| server group       | module                | x        | x          | -                   |
| server group       | lolwut                | x        | x          | -                   |
| Stream group       | xinfo                 | x        | x          | -                   |
| Stream group       | xadd                  | x        | x          | -                   |
| Stream group       | xtrim                 | x        | x          | -                   |
| Stream group       | xdel                  | x        | x          | -                   |
| Stream group       | xrange                | x        | x          | -                   |
| Stream group       | xrevrange             | x        | x          | -                   |
| Stream group       | xlen                  | x        | x          | -                   |
| Stream group       | xread                 | x        | x          | x                   |
| Stream group       | xgroup                | x        | x          | -                   |
| Stream group       | xreadgroup            | x        | x          | x                   |
| Stream group       | xack                  | x        | x          | -                   |
| Stream group       | xlclaim               | x        | x          | -                   |
| Stream group       | xpending              | x        | x          | -                   |

