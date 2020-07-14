## Overview
Download [redis-port (Linux 64-bit)](https://main.qcloudimg.com/raw/47154504189a8941250f57b60f1e2fcb/redis-port.tgz).

redis-port is a collection of open-source tools mainly used for database sync, data import, and data export between Redis nodes and supports cross-version Redis data migration. The toolkit contains the following tools:
- redis-sync: it is used for data migration between Redis instances.
- redis-restore: it supports importing Redis backup files (in RDB format) to specified Redis instances.
- redis-dump: it supports backing up Redis data in RDB format.
- redis-decode: it supports decoding Redis RDB backup files into readable files.

## Compatible Versions
- Source instances on Redis 2.8, 3.0, 3.2, 4.0, and 5.0 are supported.
- Target instances on Redis 2.8, 3.0, 3.2, 4.0, and 5.0 and in all editions of TencentDB are supported, including Redis Community Edition and CKV Edition.


## Online Migration Through redis-sync
**How it works**
- redis-sync has two modules which are simulated as replication nodes to sync data from the source instance and translate the replicated data into write commands to update the target instance.
- Data replication is done in two phases: full sync and incremental sync.

**Parameter description:**
- -n: number of concurrent write tasks. You are recommended to leave it empty or set it to CPU core quantity * 2.
- -m: source instance address in the format of `"password"@ip:port` or `ip:port` (in password-free mode).
- -t: target instance address in the format of `"password"@ip:port` or `ip:port` (in password-free mode).
- --tmpfile=FILE: temporary filename.
- --tmpfile-size=SIZW: maximum size of the temporary file.
- --help: help command.

**Sample:**
```
./redis-sync -m 127.0.0.1:6379 -t "xxx2018"@10.0.5.8:6379
```

**Output log**:

```
[root@VM_5_16_centos bin]# ./redis-sync -m 127.0.0.1:6379 -t "xxx2018"@10.0.5.8:6379
2019/02/21 09:56:00 sync.go:76: [INFO] sync: master = "127.0.0.1:6379", target = "xxx2018@10.0.5.8:6379"
2019/02/21 09:56:01 sync.go:103: [INFO] +
2019/02/21 09:56:01 sync.go:109: [INFO] sync: runid = "f63e2ad58e2fcc15c8cc122f15778389a012c1a4", offset = 18576271
2019/02/21 09:56:01 sync.go:110: [INFO] sync: rdb file = 9063349 (8.64mb)
2019/02/21 09:56:01 sync.go:208: [INFO] sync: (r/f,s/f,s) = (read,rdb.forward,rdb.skip/rdb.forward,rdb.skip)
2019/02/21 09:56:02 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(1703936/71754,0/0,0) ~ (1.62mb/-,-/-,-) ~ speed=(1.62mb/71754,0/0,0)
2019/02/21 09:56:03 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(3407872/153850,0/0,0) ~ (3.25mb/-,-/-,-) ~ speed=(1.62mb/82096,0/0,0)
2019/02/21 09:57:54 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(80487526/411969,0/1587212,0) ~  (76.76mb/-,-/-,-) ~ speed=(0/0,0/0,0)
```

**Use instructions**:
- The database capacity of the target instance should be greater than that of the source instance; otherwise, the migration will fail.
- If migration is interrupted for reasons such as network failure, you need to empty the target instance first and then perform migration again; otherwise, there may be dirty data.
- The progress of migration is displayed in the log, where "sync: rdb = 9063349 - [100.00%]" indicates that full data has been synced and incremental data sync is in progress, while "speed=(0/0,0/0,0)" indicates that incremental data has been synced.
- You can stop data sync and migration by pressing Ctrl + C or through other means.

## Importing Data Through redis-restore
redis-restore supports importing Redis backup files (in RDB format) on Redis 2.8, 3.0, 3.2, 4.0, and 5.0 as well as AOF files into specified Redis instances.

**Parameter description:**
- -n: number of concurrent write tasks. You are recommended to leave it empty or set it to CPU core quantity * 2.
- -i: RDB file path.
- -t: target instance address in the format of `"password"@ip:port` or `ip:port` (in password-free mode).
- -a: AOF file path.
- --db=DB: database ID of the target Redis instance for backup file import, which should be the same as that of the source instance.
- --unixtime-in-milliseconds=EXPR: the key expiration time value is updated in the process of data import.
- --help: help command.

**Sample:**
```
./redis-restore dump.rdb -t 127.0.0.1:6379
```


## Backing up Data Through redis-dump
redis-dump supports backing up Redis data into RDB files and incremental data into AOF files.
>TencentDB for Redis currently does not support backing up data through redis-dump. You can back up and download data in the TencentDB for Redis Console or through APIs. However, you can use redis-dump to back up your self-built Redis instances.

**Parameter description:**
- -n: number of concurrent write tasks. You are recommended to leave it empty or set it to CPU core quantity * 2.
- -m: Redis instance address in the format of `"password"@ip:port` or `ip:port` (in password-free mode).
- -o: path of the output RDB file.
- -a: path of the output AOF file.
- --help: help command.

**Sample:**
```
./redis-dump  127.0.0.1:6379 -o dump.rdb
```

