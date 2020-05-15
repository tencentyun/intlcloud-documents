The Standalone Edition can be your self-created Redis Standalone Edition or TencentDB for Redis Standard Edition. This document describes the compatibility issues in migrating data from Redis Standalone Edition to TencentDB for Redis Cluster Edition.

<span id = "jrxsm"></span>
## Compatibility Description
TencentDB for Redis Cluster Edition adopts the cluster architecture consisting of Tencent Cloud's proprietary proxy and Redis Community Cluster Edition, which is 100% compatible with Redis Community Cluster Edition commands.
![](https://main.qcloudimg.com/raw/4db4ee669a1e5f2730f28a901f8db0c8.png)

The most challenging problem in migrating data from the Standalone Edition to the Cluster Edition is the command compatibility with usage specifications of the Cluster Edition. You need to pay attention to the following usage specification issues:

### Multikey operation
Redis Cluster Edition uses the hash algorithm to distribute keys to 16,000 slots. For more information on the principle, please see [Redis Cluster Specification](https://redis.io/topics/cluster-spec).
- Redis Community Cluster Edition: it does not support any cross-slot multi-key access commands.
- TencentDB for Redis Cluster Edition: it supports cross-slot multi-key access of the `MGET`, `MSET`, and `DEL` commands. This mainly works by using Tencent Cloud's proprietary proxy to implement aggregated command computing among multiple nodes.
- Hash tag: in your business, keys that need to engage in multi-key computing can be aggregated into the same slot through a hash tag. For more information on how to use hash tags, please see [Redis Cluster Specification](https://redis.io/topics/cluster-spec).
- Cross-slot command list:

| Command Group         | Command          | Cross-Slot Support in Cluster Edition |
| -------------- | ------------- | ------------------ |
| keys        | del           | ✓                  |
| keys        | exists        | x                  |
| keys        | rename        | x                  |
| keys        | renamenx      | x                  |
| keys        | unlink        | x                  |
| list        | rpoplpush     | x                  |
| list        | blpop         | x                  |
| list        | brpop         | x                  |
| list        | brpoplpush    | x                  |
| sets        | sdiff         | x                  |
| sets        | sdiffstore    | x                  |
| sets        | sinter        | x                  |
| sets        | sinterstore   | x                  |
| sets        | smove         | x                  |
| sets        | sunion        | x                  |
| sets        | sunionstore   | x                  |
| sorted sets | zinterstore   | x                  |
| sorted sets | zunionstore   | x                  |
| strings     | bitop         | x                  |
| strings     | mget          | ✓                  |
| strings     | mset          | ✓                  |
| strings     | msetnx        | x                  |
| hyperloglog | pfcount       | x                  |
| hyperloglog | pfmerge       | x                  |
| scripting   | eval          | x                  |
| scripting   | evalsha       | x                  |
| scripting   | script exists | x                  |
| Stream      | xread         | x                  |
| Stream      | xreadgroup    | x                  |

### Support for Lua
- The Cluster Edition supports Lua commands, but cross-slot access to keys in Lua scripts is not supported.
- The `KEY` parameter must be passed in for the `EVAL` and `EVALSHA` commands; otherwise, they cannot be executed.
- The subcommands `LOAD`, `FLUSH`, `KILL`, and `EXIST` of `SCRIPT` will be distributed to all master nodes in the cluster through the proxy.
```
> eval "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second
1) "key1"
2) "key2"
3) "first"
4) "second"
```
>The `key1` and `key2` parameters must be passed in when you use Lua.

### Transaction support
- The Cluster Edition supports transactions, but cross-slot access to keys in transactions is not supported.
- You need to first run the `watch key` command and then the `multi` and `exec` commands in the current version. This operation will be optimized in future versions to eliminate need to run `watch key` first.

<span id = "zdyml"></span>
### Custom command
Through VIP encapsulation, Redis Cluster Edition provides a user experience in cluster mode comparable to the standalone edition, making it much easier for use in different scenarios. To increase the transparency to OPS, custom commands can be used. Access to each node in the cluster is supported by adding a parameter "node ID" on the right of the original command parameter list, such as COMMAND arg1 arg2 ... [node ID]. The node ID can be obtained through the `cluster nodes` command or in the [console](https://console.cloud.tencent.com/redis):
```
10.1.1.1:2000> cluster nodes25b21f1836026bd49c52b2d10e09fbf8c6aa1fdc 10.0.0.15:6379@11896 slave 36034e645951464098f40d339386e9d51a9d7e77 0 1531471918205 1 connectedda6041781b5d7fe21404811d430cdffea2bf84de 10.0.0.15:6379@11170 master - 0 1531471916000 2 connected 10923-1638336034e645951464098f40d339386e9d51a9d7e77 10.0.0.15:6379@11541 myself,master - 0 1531471915000 1 connected 0-546053f552fd8e43112ae68b10dada69d3af77c33649 10.0.0.15:6379@11681 slave da6041781b5d7fe21404811d430cdffea2bf84de 0 1531471917204 3 connected18090a0e57cf359f9f8c8c516aa62a811c0f0f0a 10.0.0.15:6379@11428 slave ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 0 1531471917000 2 connectedef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 10.0.0.15:6379@11324 master - 0 1531471916204 0 connected 5461-10922
Native command: info server
Custom command: info server ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171SCAN 
Sample command: scan 0 238b45926a528c85f40ae89d6779c802eaa394a2scan 0 match a* 238b45926a528c85f40ae89d6779c802eaa394a2KEYS 
Sample command: keys a* 238b45926a528c85f40ae89d6779c802eaa394a2
```


### Client access method
You are recommended to use a standalone (e.g., [Jedis](https://intl.cloud.tencent.com/document/product/239/7043) but not Jedis Cluster) client to access TencentDB for Redis Cluster Edition, as this access method is more efficient and simpler. You can also access through cluster clients, such as Jedis Cluster.

### Codis compatibility
TencentDB for Redis Cluster Edition is 100% compatible with Codis Server commands with no modification to your business required. You can use DTS to quickly migrate data to TencentDB for Redis, which has the following advantages over Codis:
- TencentDB for Redis Cluster Edition is compatible with more editions. Codis supports only Redis v3.2 or below, while TencentDB for Redis Cluster Edition supports Redis v4.0 and v5.0 and will be continuously updated in sync with the Redis Community.
- TencentDB for Redis Cluster Edition is compatible with more commands. Codis does not support blocking commands such as `BLPOP` and `SUBSCRIBE`.
- If a big key occurs in data migration with Codis, the service may become unavailable. In contrast, TencentDB for Redis supports lossless expansion with no fear for big keys.

## Compatibility Check
Currently, no tools can be used to exactly determine whether there will be compatibility problems in data migration from the Standalone Edition to the Cluster Edition. You can use the following two tools to evaluate the compatibility before migration. You are recommended to perform static evaluation, dynamic evaluation, and business verification before migration to ensure that data can be smoothly migrated.

### Static evaluation
1. Download the [cluster_migrate_online_check.py static verification tool](https://redis-doc-2020-1254408587.cos.ap-guangzhou.myqcloud.com/cluster_migrate_check.py) and use it to run the `info commandstats` command to check whether the Standalone Edition has ever executed cross-slot commands in order to determine whether there is compatibility problem.
```
Usage:
./cluster_migrate_check.py host port password 
```
>Enter the corresponding Redis Standalone Edition information for `host`, `port`, and `password`.
2. Check whether each item can passe as instructed in [Compatibility Description](#jrxsm) above.

### Dynamic evaluation
Download the [cluster_migrate_online_check dynamic verification tool](https://redis-doc-2020-1254408587.cos.ap-guangzhou.myqcloud.com/cluster_migrate_online_check) and use it to simulate the execution of the `psync` command on the client so as to sync incremental data from the Standalone Edition to the TencentDB for Redis Cluster Edition in real time. By performing real-time sync, you can check whether there is compatibility problem in write commands. This tool cannot test the compatibility of read commands.

The steps are as follows:
1. Activate the TencentDB for Redis Cluster Edition in the [console](https://console.cloud.tencent.com/redis).
2. Use the tool to sync data from the Standalone Edition to the TencentDB for Redis Cluster Edition in real time.
3. After a period of verification (such as 6 or 24 hours), if the tool does not report any errors, the write commands do not have compatibility problems; otherwise, you can get the information of incompatible commands in the error message.
```
Usage:
./cluster_migrate_online_check srcip:srcport srcpasswd dstip:dstport dstpasswd 
Environment variable parameters:
export logout=1  // It is used to print command in the console, which is disabled by default
export pipeline = 2000  // Number of concurrent pipelines, which is 1,000 by default
```
>
>- `srcip:srcport`: Redis Standalone Edition address information, which is required.
>- `dstip:dstport`: TencentDB for Redis Cluster Edition address information, which is optional. If it is left empty, the tool can be used as a monitor.
4. Check whether each item can pass as instructed in [Compatibility Description](#jrxsm) above.

### Business verification
To ensure successful data migration, you are recommended to test the business in the testing environment. You can connect the business in the testing environment to the TencentDB for Redis Cluster Edition and confirm whether all features can work properly before data migration.

## Migrating Data Online with DTS
For detailed directions, please see [Migrating with DTS](https://intl.cloud.tencent.com/document/product/239/31941).

## Migration Failure
-  The `client-output-buffer-limit` parameter value is too small. You are recommended to set it to 512 MB or 1,024 MB by running the following command:
```
config set client-output-buffer-limit "slave 1073741824 1073741824 600"
```
- Parameters have not been passed in for the `EVAL` command.

