## Tencent Cloud Custom Commands
Through VIP encapsulation, Memory Edition (Cluster Architecture) delivers a user experience in cluster mode comparable to the standalone edition, making it much easier for use in different scenarios. However, in Ops scenarios, each node in the cluster needs to be accessed frequently to locate exceptions. In this case, the custom command feature can add a **node ID** parameter to the parameter list of the original command in the format of `COMMAND arg1 arg2 ... [node ID]` in order to easily get the information of the specified node. The node ID can be obtained from the **Node Management** page in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) or through the `cluster nodes` command.

## INFO 
This command returns the information and statistics of a server.

#### Custom command format
```
info [section] [node ID]
```

Here, optional parameters can be used to select a specific part of the information:
- `server`: The general information of a Redis server.
- `clients`: The information of connected clients.
- `memory`: The information of memory usage.
- `persistence`: The information of RDB and AOF.
- `stats`: The general statistics.
- `replication`: The information of master/replica replication.
- `cpu`: The information of CPU usage.
- `commandstats`: The statistics of Redis commands.
- `cluster`: The information of a Redis cluster.
- `keyspace`: The statistics of a database.

The command can also take the following values:
- `all`: Returns all the information.
- `default`: Returns the default information.

#### Example
The following example runs the `INFO` command with `section` being `server`:
![](https://qcloudimg.tencent-cloud.cn/raw/0662345a9d5f442f534380aaea94813f.png)

## SLOWLOG
This command reads slow logs. It uses `SLOWLOG GET` to return the entries in slow logs. You can specify to return only the last N entries and pass other parameters to this command, such as `SLOWLOG GET 10`. 

#### Custom command format
```
slowlog get [Redis node ID]
slowlog get [slow log quantity][Redis node ID]
```

#### Example
![](https://qcloudimg.tencent-cloud.cn/raw/a46acc9fd17ea7ecaeffae7540df02aa.png)

## FLUSHDB
This command deletes all keys of the currently selected database. It will never fail. 

#### Custom command format
```
flushdb [Redis node ID]
```

#### Example
```
cd-crs-rhxxxay.sql.tencentcdb.com:24894> flushdb f2f3c387b9fab0e67af02039845c60278b13bed0
OK
```

## PING
This command is often used to test whether the connection still exists or to measure the latency. 

#### Custom command format
```
ping [message] [node ID]
```

#### Example
```
[ crs-rh**** | DB0 ] # PING "PONG" f2f3c3************************
PONG
[ crs-rh**** | DB0 ] # PING "hello world"
hello world
```

## KEYS
This command queries all the matched keys.

#### Custom command format
```
 keys [pattern]  [Redis node ID]
```

#### Example
```
keys a* f2f3c3*************************
```
![](https://qcloudimg.tencent-cloud.cn/raw/064d9708bc2fbcb8971d88f2becd6aed.png)

## SCAN
#### Custom command format
```
scan cursor [MATCH pattern] [COUNT count] [Redis node ID]
```

#### Example
```
[ crs-******** | DB0 ] # scan 0 f2f3c3*************************
1)  "2"
```


