
## Overview
[redis-port (Linux 64-bit)](https://main.qcloudimg.com/raw/47154504189a8941250f57b60f1e2fcb/redis-port.tgz)

redis-port is a collection of open-source tools mainly used for database sync, data import, and data export between Redis nodes and supports cross-edition Redis data migration. The toolkit contains the following tools:
- redis-sync: It is used for data migration between Redis instances.
- redis-restore: It supports importing Redis backup files (in RDB format) to the specified Redis instance.
- redis-dump: It supports backing up Redis data in RDB format.
- redis-decode: It supports decoding RDB files into readable files.

## Compatible Versions
- Source instances on Redis 2.8, 3.0, 3.2, and 4.0 are supported.
- Destination instances on Redis 2.8, 3.0, 3.2, and 4.0 and in all editions of TencentDB are supported, including Redis Standard Edition (Community) and Cluster Edition (Community).


## Online Migration via redis-sync
**How it works**
- redis-sync has two modules which are simulated as replication nodes to sync data from the source instance and translate the replicated data into write commands to update the destination instance.
- Data replication is done in two phases: full sync and incremental sync.

**Parameter descriptions**:
- -n: Number of concurrent write tasks, which is recommended to be either left alone or set to CPU core quantity * 2.
- -m: Source instance address in the format of "password@ip:port".
- -t: Destination instance address in the format of "password@ip:port".
- --tmpfile=FILE: Temporary filename.
- --tmpfile-size=SIZW: Maximum length of the temporary file.
- --help: Help command.

**Example:**
```
./redis-sync -m 127.0.0.1:6379 -t 192.17.1.1:6379
```

**Output log**:

```
[root@VM_5_16_centos bin]# ./redis-sync -m 127.0.0.1:6379 -t xxx2018@10.0.5.8:6379
2019/02/21 09:56:00 sync.go:76: [INFO] sync: master = "127.0.0.1:6379", target = "Passwd2018@10.0.5.8:6379"
2019/02/21 09:56:01 sync.go:103: [INFO] +
2019/02/21 09:56:01 sync.go:109: [INFO] sync: runid = "f63e2ad58e2fcc15c8cc122f15778389a012c1a4", offset = 18576271
2019/02/21 09:56:01 sync.go:110: [INFO] sync: rdb file = 9063349 (8.64mb)
2019/02/21 09:56:01 sync.go:208: [INFO] sync: (r/f,s/f,s) = (read,rdb.forward,rdb.skip/rdb.forward,rdb.skip)
2019/02/21 09:56:02 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(1703936/71754,0/0,0) ~ (1.62mb/-,-/-,-) ~ speed=(1.62mb/71754,0/0,0)
2019/02/21 09:56:03 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(3407872/153850,0/0,0) ~ (3.25mb/-,-/-,-) ~ speed=(1.62mb/82096,0/0,0)
2019/02/21 09:57:54 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(80487526/411969,0/1587212,0) ~  (76.76mb/-,-/-,-) ~ speed=(0/0,0/0,0)
```

**Use instructions**:
- The db capacity of the destination instance should be greater than that of the source instance; otherwise, the migration will fail.
- If migration is interrupted for reasons such as network failure, you need to empty the destination instance first and then perform migration again; otherwise, there may be dirty data.
- The progress of migration is displayed in the log, where "sync: rdb = 9063349 - [100.00%]" indicates that full data has been synced and incremental data sync is in progress, while "speed=(0/0,0/0,0)" indicates that incremental data has been synced.
- You can stop data sync and migration by pressing Ctrl + C or through other means.

## Importing Data via redis-restore
redis-restore supports importing Redis backup files (in RDB format) on Redis 2.8, 3.0, 3.2, and 4.0 as well as AOF files into the specified Redis instance.

**Parameter descriptions**:
- -n: Number of concurrent write tasks, which is recommended to be either left alone or set to CPU core quantity * 2.
- -i: RDB file path.
- -t: Destination instance address in the format of "password@ip:port".
- -a: AOF file path.
- --db=DB: ID of the imported DB, which is the same as the source instance ID by default.
- --unixtime-in-milliseconds=EXPR: The Key expiration time value is updated in the process of data import.
- --help: Help command.

**Example:**
```
./redis-restore dump.rdb -t 127.0.0.1:6379
```


## Backing up Data via redis-dump
redis-dump supports backing up Redis data into RDB files and incremental data into AOF files.
> TencentDB for Redis currently does not support backing up data via redis-dump. You can back up and download data in the TencentDB for Redis Console or through APIs. However, you can use redis-dump to back up your self-built Redis instances.

**Parameter descriptions**:
- -n: Number of concurrent write tasks, which is recommended to be either left alone or set to CPU core quantity * 2.
- -m: Redis instance address in the format of "password@ip:port".
- -o: Path to the outputted RDB file.
- -a: Path to the outputted AOF file.
- --help: Help command.

**Example:**
```
./redis-dump  127.0.0.1:6379 -o dump.rdb
```



