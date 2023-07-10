본문은 주로 Docker를 통해 GooseFS 배포하는 방법에 대해 설명합니다. 

## 준비 사항

1. Docker 19.03.14 혹은 그 이상의 버전을 설치합니다. 
2. CentOS 7 버전 이상이어야 합니다. 
3. GooseFS docker 이미지를 획득해야 합니다. 예: goosefs:v1.0.0

## 설치 방법

1. ufs 디렉터리를 생성하고 로컬 기기의 디렉터리를 GooseFS 루트 디렉터리에 마운트합니다. 
```shell
mkdir /tmp/goosefs_ufs 
```
2. master 프로세스를 실행합니다.

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

 <dx-alert infotype="explain" title="설명">
- -Dgoosefs.master.hostname: master 주소를 설정 합니다. 
- -Dgoosefs.master.mount.table.root.ufs: GooseFS 루트 디렉터리 마운트 포인트를 설정합니다. 
- -v /tmp/goosefs_ufs:/opt/data: 로컬 디렉터리를 docker 컨테이너 안에 매핑합니다. 
- --net=host: docker가 host 네트워크를 사용합니다. 
</dx-alert>

3. worker 프로세스를 실행합니다. 

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

## 작업 예시

1. 컨테이너 확인. 

```shell
[root@VM-0-7-centos ~]# docker ps | grep goosefs
0bda1cac76f4        goosefs:v1.0.0      "/entrypoint.sh mast…"   32 minutes ago      Up 32 minutes                           goosefs-master
b6260f9a0134        goosefs:v1.0.0     "/entrypoint.sh work…"   About an hour ago   Up About an hour                        goosefs-worker1
```

2. 컨테이너로 이동. 
``` shell
docker exec -it 0bda1cac76f4 /bin/bash
```
3. COS 디렉터리 마운트.

```shell
goosefs fs mount --option fs.cosn.userinfo.secretId={secretId} \
    --option fs.cosn.userinfo.secretKey={secretKey} \
    --option fs.cosn.bucket.region=ap-beijing \
    --option fs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
    --option fs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
    /cosn {cos버킷}
```

4. 디렉터리 확인.

```shell
[goosefs@VM-0-7-centos goosefs-1.0.0-SNAPSHOT-noUI-noHelm]$ goosefs fs ls /
drwxrwxrwx  goosefs        goosefs                      1       PERSISTED 01-01-1970 08:00:00:000  DIR /cosn
drwxr-xr-x  root           root                         0       PERSISTED 06-25-2021 11:01:24:000  DIR /my 
```

5. worker 노드 확인.

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
