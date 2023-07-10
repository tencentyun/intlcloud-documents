## Overview

Based on the open-source Alluxio framework, GooseFS provides a powerful distributed cache ability to unify cross-platform data and improve the overall I/O throughput.

It can be implemented as follows:

- Remote storage for namespaces: Connect namespaces to different external underlying storage such as COS and CHDFS for unlimited and persistent storage. With CosN’s compute-storage separation solution, GooseFS offers scalability and high availability for big data storage.
- GooseFS local cache: GooseFS leverages the distributed cache ability of the master and workers to store the cached and temporary data generated at the application layer in the memory and disk of the local application node. Each local node is configurable. The remote persistent storage layer connected to namespaces will use the same client to serve users’ reads/writes.

You can configure the cache policy to decide whether to use the local cache or remote storage for namespaces.

![](https://main.qcloudimg.com/raw/c6ee0f55529fec5d60043577c3d1211d.png)

GooseFS supports local cache and remote storage for namespaces to provide an all-around storage separated solution and create data affinity for application nodes.

## GooseFS Cache Configuration

You can open the `goosefs-site.properties` file to view the GooseFS cache configurations, which include cache levels (single-level and multi-level storage), cache replacement policies (LRU and LRFU), and more.

### 1. Cache level

GooseFS provides single-level and multi-level caches. Single-level cache uses only one memory device, while multi-level cache uses various storage devices to meet the needs of different business loads and provide satisfactory I/O performance. By default, GooseFS uses single-level storage. If there are multiple storage devices, cache replacement will affect performance and thus **single-level storage** is recommended. You can choose a memory device such as MEM, SSD, or HDD according to your I/O requirements.

You can modify `levels` in the `goosefs-site.properties` configuration file to change the cache level, where `1` indicates using only one level of storage and `3` indicates 3 levels.

```plaintext
goosefs.worker.tieredstore.levels=1
```

You can also modify `alias` in `goosefs-site.properties` to change the storage device used for a cache level.

```plaintext
goosefs.worker.tieredstore.level{x}.alias=MEM
```

>!”x” in level{x} is the index of the storage level. For example, `level0` indicates single-level storage. 

**1.1 Single-level storage**

Common configurations for single-level storage are as follows:


```plaintext
goosefs.worker.tieredstore.levels=1
goosefs.worker.tieredstore.level0.alias=HDD
goosefs.worker.ramdisk.size=16GB
goosefs.worker.memory.size=100GB
goosefs.worker.tieredstore.level0.dirs.path=/data/GooseFSWorker,/data1/GooseFSWorker,/data2/GooseFSWorker,/data3/GooseFSWorker,/data4/GooseFSWorker
goosefs.worker.tieredstore.level0.dirs.mediumtype=MEM,MEM,MEM,SSD,SSD
goosefs.worker.tieredstore.level0.dirs.quota=16GB,16GB,16GB,100GB,100GB
```





Configuration items:

- ramdisk.size: memory size for workers. The value must be smaller than `memory`. GooseFS will allocate memory from the total memory for each worker according to the specified value.
- memory.size: total memory of the GooseFS system. The specified size of memory will be automatically used from the storage device. The value must be smaller than the size of the physical memory of the storage device.
- dirs.path: directories that GooseFS allocates storage devices for. This parameter must be used together with `dirs.mediumtype`. In the example above, `/data/GooseFSWorker` is attached to the MEM storage device, and `/data4/GooseFSWorker` is attached to an SSD. Note that the directory sequence must correspond to the storage device sequence.
- dirs.mediumtype: storage device used for the specified directories. This parameter must be used together with `dirs.path`. By default, `MEM` and `SSD` are valid values. If other storage devices such as HDD are attached, you can configure them as needed.
- dirs.quota: space allocated for the specified directories. The values must correspond to the directory sequence. In the example above, each of `/data/GooseFSWorker`, `/data1/GooseFSWorker`, and `/data2/GooseFSWorker` are allocated 16 GB of MEM, and both `data3/GooseFSWorker` and `/data4/GooseFSWorker` are allocated 100 GB of SSD.

**1.2 Multi-level storage**

Multi-level storage reads and writes data blocks differently from single-level storage. In single-level mode, data reads/writes use the same storage device. However, in multi-level mode, data is first written to the highest level of storage device. If any data needs to be read, it will be moved to the highest level of storage device. Details are described below.

- **Data writes**: New data blocks will be written to the highest level of storage device by default. If the highest level of storage device is used up, data will be moved to the next storage level. If storage capacities of all storage devices are used up, older data will be replaced according to the cache replacement policies you set. If expired data cannot be replaced and the available memory is used up, data cannot be written.
- **Data reads**: In multi-level storage mode, cold data will be moved to the lower-level of storage device imperceptibly. If the data is read again, it will be moved back to the highest storage level.


>!
>- GooseFS will clear a specified amount of data according to the cache replacement policies configured. The amount can be specified with `goosefs.worker.tieredstore.free.ahead.bytes`, and the default value is `0`.
>- In multi-level storage mode, data reads may cause data movement from a lower storage level to the highest one and compromise performance. Therefore, **you are advised to use single-level storage** in most cases.

Common configuration items:

```plaintext
goosefs.worker.tieredstore.levels
goosefs.worker.tieredstore.level{x}.alias
goosefs.worker.tieredstore.level{x}.dirs.path
goosefs.worker.tieredstore.level{x}.dirs.mediumtype
goosefs.worker.tieredstore.level{x}.dirs.quota
```

In the example above, `x` indicates the index of the cache level. In most cases, you can use three levels (corresponding MEM, SSD, and HDD). The example below uses two levels (MEM and SSD) and allocates 100 GB for each level:

```plaintext
goosefs.worker.tieredstore.levels=2
goosefs.worker.tieredstore.level0.alias=MEM
goosefs.worker.tieredstore.level0.dirs.path=/data/GooseFSWorker
goosefs.worker.tieredstore.level0.dirs.mediumtype=MEM
goosefs.worker.tieredstore.level0.dirs.quota=100GB
goosefs.worker.tieredstore.level1.alias=SSD
goosefs.worker.tieredstore.level1.dirs.path=/data1/GooseFSWorker
goosefs.worker.tieredstore.level1.dirs.mediumtype=SSD
goosefs.worker.tieredstore.level1.dirs.quota=100GB
```


You can configure an unlimited number of storage levels with GooseFS, but their names (alias) must be unique. If you use three levels, it will be easy to distinguish them if you name them MEM, SSD, and HDD.

### 2. Cache replacement policies

GooseFS supports two cache replacement policies:

- LRUAnnotator: least-recently-used (LRU) (default)
- LRFUAnnotator: combines the least-recently-used (LRU) and least-frequently-used (LFU) schemes. You can set weights of LRU and LFU using `goosefs.worker.block.annotator.lrfu.step.factor` and `goosefs.worker.block.annotator.lrfu.attenuation.factor` to decide how these two policies should take effect together.
  - If the weight of least-recently-used is set the maximum value, it will function in the same way as `LRUAnnotator`.

You can use `goosefs.worker.block.annotator.class` to specify the cache replacement policies, where the policy names should be correctly set as follows:

```plaintext
goosefs.worker.block.annotator.LRUAnnotator
goosefs.worker.block.annotator.LRFUAnnotator
```



## Data Lifecycle

The lifecycle described here is for data in GooseFS rather than data in the remote UFS. You can manage data lifecycle with the following four operations:

- free: deletes the specified directories or files from GooseFS (data in the UFS will be intact). This operation is mainly used to free GooseFS cache space for other hotter data.
- load: loads directories/files in the UFS to GooseFS. This operation is mainly used to restore cold data for higher I/O performance.
- persist: writes GooseFS data to the UFS to store data persistently and avoid data loss.
- Time to Live (TTL): sets the lifecycle for directories/files in GooseFS. If data has expired, it will be deleted from GooseFS and the UFS. You can also delete data only in GooseFS or only free the disk space.

### 1. Freeing data from GooseFS

Run the `free` command to free data from GooseFS. In the example below, the data status becomes 0% in GooseFS after the freeing operation.

```plaintext
$ goosefs fs free /data/test.txt
/data/test.txt was successfully freed from GooseFS space.
$ goosefs fs ls /data/test.txt
-rw-rw-rw-  hadoop         hadoop                      14       PERSISTED 03-11-2021 11:46:15:000 0% /data/test.txt
```

`/data/test.txt` in the example can be replaced with any valid GooseFS path. If data is stored in the remote UFS, you can run the `load` command to reload the data.

>!You are advised to set cache replacement policies to automatically clear GooseFS historical data.

### 2. Load data to GooseFS

Run the `load` command to load data to GooseFS. In the example below, the data has been 100% loaded.

```plaintext
$ goosefs fs load /data/test.txt
/data/test.txt loaded
$ goosefs fs ls /data/test.txt
-rw-rw-rw-  hadoop         hadoop                      14       PERSISTED 03-11-2021 11:46:15:000 100% /data/test.txt
```


`/data/test.txt` in the example can be replaced with any valid GooseFS path. To load data from a local file system, use the `copyFromLocal` command. Note that data loaded from a local file system will not be stored to the remote UFS. By default, data will be cached to GooseFS at the first access. Therefore, you don’t need to run the `load` command in most cases. However, if you need your data loaded into the cache in advance, you can run this command.

### 3. Storing GooseFS data persistently

Run the `persist` command to save the data to the remote UFS:

```plaintext
$ goosefs fs persist /data/test.txt
$ goosefs fs ls /data/test.txt
-rw-rw-rw-  hadoop         hadoop                      14       PERSISTED 03-11-2021 11:46:15:000 100% /data/test.txt
```


`/data/test.txt` in the example above can be replaced with any valid GooseFS path. You are advised to configure cache replacement policies to automatically store data persistently.

### 4. Adding TTL

GooseFS allows you to add a time to live (TTL) value for any directory or file in a namespace. TTL ensures that your data can be deleted as scheduled to free space for new files and make full use of the local disk. The TTL values of GooseFS files and directories can be the metadata so that these TTL values will still take effect even if the cluster is restarted. The checker program in the background will check TTL values periodically and clear expired data automatically.

The checker’s interval and action can be set in `goosefs-site.preperties`. In the example below, the checker’s interval is set to 10 minutes, and the action is set to `FREE`.

```plaintext
goosefs.master.ttl.checker.interval=10m
goosefs.user.file.create.ttl.action=FREE
```

After the configuration, GooseFS background threads will inspect expired files every 10 minutes. If any expired file is found during an inspection cycle, the file’s cache will be freed when the next cycle completes. For example, if a file is found expired in the cycle that ends at 00:00:00, the file’s cache will be cleared at 00:10:00.

>!The default unit of the interval is ms (millisecond). You can use a unit such as s (second), m (minute), or h (hour) when you set the input parameter. For more information, please see the configuration description.

## Data Replication

Data replication is classified into active replication and passive replication.

### 1. Passive replication

In GooseFS, each file has one or more data blocks spread across the cluster. By default, GooseFS automatically adjusts the number of replicas for data blocks according to the load and capacity. Passive replication is performed when:

- The same block is read by multiple clients at the same time. As a result, multiple blocks reside in different workers.
- When local reads are prioritized, but the data is not found from the local environment, remote reads will be initialized, and the data will be saved to the local worker.
- If the number of replicas generated by passive replication is greater than the configured quantity, the excess will be deleted asynchronously, which is unperceivable to users.

### 2. Active replication

Active replication is implemented by setting the number of replicas for a file. If the number of blocks is smaller than the configured quantity, blocks will be made up asynchronously. If there are excessive blocks, excessive replicas will be deleted. You can run the following command to configure active replication:

```plaintext
$ goosefs fs setReplication  [-R] [--max | --min ] <path>
```

Parameters are described as follows:

- max: the maximum number of replicas (default value: `-1`, indicating no upper limit). If this parameter is set to `0`, the file will not be cached in GooseFS. Usually, you can set this parameter to a positive integer. After the configuration, GooseFS will check the replica quantity and delete the excessive ones.
- min: the minimum number of replicas (default value: `0`, indicating no replica will be retained when the data expires). Usually, you can set this parameter to a positive integer, which must be **smaller than `max`**. After the configuration, GooseFS will check the replica quantity and make up the quantity automatically if the replica quantity is smaller than the configured value.
- path: a directory or a file path
- R: recursively replicates all files and sub-directories of a directory (if `path` is set to a directory) following `min` and `max`.

You can run the `stat` command to view the replication of a file. In the example below, `replicationMax` of the `/data/test.txt` file is set to `-1`, which means that the file will be deleted once it expires.

```plaintext
$ goosefs fs stat /data/test.txt
/data/test.txt is a file path.
FileInfo{fileId=50331647, fileIdentifier=null, name=test.txt, path=/data/test.txt, ufsPath=hdfs://172.16.16.16:4007/data/test.txt, length=0, blockSizeBytes=134217728, creationTimeMs=1618193473555, completed=true, folder=false, pinned=false, pinnedlocation=[], cacheable=true, persisted=true, blockIds=[], inMemoryPercentage=100, lastModificationTimesMs=1616763603692, ttl=-1, lastAccessTimesMs=1616763603692, ttlAction=DELETE, owner=hadoop, group=supergroup, mode=420, persistenceState=PERSISTED, mountPoint=false, replicationMax=-1, replicationMin=0, fileBlockInfos=[], mountId=1, inGooseFSPercentage=100, ufsFingerprint=TYPE|FILE UFS|hdfs OWNER|hadoop GROUP|supergroup MODE|420 CONTENT_HASH|(len:0,_modtime:1616763603692) , acl=user::rw-,group::r--,other::r--, defaultAcl=}
This file does not contain any blocks.
```


## Querying Cache Usage

GooseFS will record the local cache and storage usage. You can run the commands below to view the running status of GooseFS for local cache management and maintenance.

- View the cache usage, in bytes:

```plaintext
$ goosefs fs getUsedBytes
Used Bytes: 0
```


- View the total cache capacity, in bytes:

```plaintext
$ goosefs fs getCapacityBytes
Capacity Bytes: 1610612736000
```


- View the cache usage report:

```plaintext
$ goosefs fsadmin report
GooseFS cluster summary: 
    Master Address: 172.16.16.16:19998
    Web Port: 19999
    Rpc Port: 19998
    Started: 04-12-2021 10:52:05:255
    Uptime: 0 day(s), 1 hour(s), 28 minute(s), and 57 second(s)
    Version: 2.5.0-SNAPSHOT
    Safe Mode: false
    Zookeeper Enabled: false
    Live Workers: 3
    Lost Workers: 0
    Total Capacity: 1500.00GB
        Tier: HDD  Size: 1500.00GB
    Used Capacity: 0B
        Tier: HDD  Size: 0B
    Free Capacity: 1500.00GB
```
