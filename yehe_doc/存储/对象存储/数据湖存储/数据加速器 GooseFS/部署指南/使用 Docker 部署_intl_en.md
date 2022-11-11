This document describes how to use Docker to deploy GooseFS.

## Preparations

1. You have installed Docker 19.03.14 or a later version.
2. You have installed CentOS 7 or a later version
3. You have obtained a GooseFS docker image, such as goosefs:v1.0.0.

## Installation

1. Create a directory called `ufs` to mount the local directory to the root directory of GooseFS:
```shell
mkdir /tmp/goosefs_ufs 
```
2. Run the master process:

```shell
docker run -d  --rm \
--net=host \
--name=goosefs-master \
-v /tmp/goosefs_ufs:/opt/data \
-e GOOSEFS_JAVA_OPTS=" \
-Dgoosefs.master.hostname=localhost \
-Dgoosefs.master.mount.table.root.ufs=/opt/data" \
goosefs:v1.0.0 master
```

 <dx-alert infotype="explain" title="Note">
- -Dgoosefs.master.hostname: sets the master address.
- -Dgoosefs.master.mount.table.root.ufs: sets the mount point in the root directory of GooseFS.
- -v /tmp/goosefs_ufs:/opt/data: maps the local directory to the docker container.
- --net=host: Docker uses the host’s network.
</dx-alert>
3. Run the worker process.

```shell
docker run -d --rm \
--net=host \
--name=goosefs-worker1 \
--shm-size=1G \
-e GOOSEFS_JAVA_OPTS=" \
-Dgoosefs.worker.memory.size=1G \
-Dgoosefs.master.hostname=localhost" \
goosefs:v1.0.0 worker
```

## Operation Example

1. View the container:
```shell
[root@VM-0-7-centos ~]# docker ps | grep goosefs
0bda1cac76f4        goosefs:v1.0.0      "/entrypoint.sh mast…"   32 minutes ago      Up 32 minutes                           goosefs-master
b6260f9a0134        goosefs:v1.0.0     "/entrypoint.sh work…"   About an hour ago   Up About an hour                        goosefs-worker1
```
2. Go to the container:
``` shell
docker exec -it 0bda1cac76f4 /bin/bash
```
3. Mount the COS directory:

```shell
goosefs fs mount --option fs.cosn.userinfo.secretId={secretId} \
    --option fs.cosn.userinfo.secretKey={secretKey} \
    --option fs.cosn.bucket.region=ap-beijing \
    --option fs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
    --option fs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
    /cosn {COS bucket}
```
4. View the directory:
```shell
[goosefs@VM-0-7-centos goosefs-1.0.0-SNAPSHOT-noUI-noHelm]$ goosefs fs ls /
drwxrwxrwx  goosefs        goosefs                      1       PERSISTED 01-01-1970 08:00:00:000  DIR /cosn
drwxr-xr-x  root           root                         0       PERSISTED 06-25-2021 11:01:24:000  DIR /my 
```
5. View the worker node:

```shell

 [goosefs@VM-0-7-centos goosefs-1.0.0-SNAPSHOT-noUI-noHelm]$ goosefs fsadmin report capacity
 Capacity information for all workers: 
    Total Capacity: 1024.00MB
        Tier: MEM  Size: 1024.00MB
    Used Capacity: 0B
        Tier: MEM  Size: 0B
    Used Percentage: 0%
    Free Percentage: 100%

 Worker Name      Last Heartbeat   Storage       MEM
 172.31.0.7       0                capacity      1024.00MB
                                  used          0B (0%)
```
