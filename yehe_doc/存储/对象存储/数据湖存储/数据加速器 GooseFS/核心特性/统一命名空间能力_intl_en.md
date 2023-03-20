## Overview

The unified namespace capability of GooseFS integrates the access semantics of different underlying storage systems through a transparent naming mechanism, providing users with a unified interactive view for data management.

Leveraging this capability, GooseFS connects and communicates with different underlying storage systems, such as local file systems, Tencent Cloud Object Storage (COS), and Tencent Cloud HDFS (CHDFS), and provides unified access APIs and file protocols for upper-layer businesses. In this way, the business side only needs to call the access APIs provided by GooseFS to access data stored in different underlying storage systems.

![](https://main.qcloudimg.com/raw/6ef8e2899bbd704f7c05c7d0526624b1.png)

The figure above shows the working principle of the unified namespace. You can use GooseFS's namespace creation instruction `create ns` to mount specified file directories of COS and CHDFS to GooseFS, and then use the `gfs://` unified schema to access data. Details are as follows:

- COS contains 3 buckets in total: bucket-1, bucket-2, and bucket-3. bucket-1 contains the BU_A and BU_B directories, and both bucket-1 and bucket-2 are mounted to GooseFS.
- CHDFS contains 4 directories: BU_E, BU_F, BU_G, and BU_H. All of them are mounted to GooseFS, except BU_H.
- Among GooseFS file operations, the BU_A and BU_E directories can be accessed using the unified schema `gfs://`, and the files are cached in the local file system of GooseFS.
-  The BU_A and BU_E directories stored in the underlying file systems (COS and HDFS) have been mounted to GooseFS. If files are cached on GooseFS, they can be accessed through the unified schema `gfs://` (for example, `hadoop fs ls gfs://BU_A`), and they can also be accessed through the namespace of each remote file system (for example, `hadoop fs ls cosn://bucket-1/BU_A`).
- If the files are not cached on GooseFS, they cannot be accessed through the unified schema `gfs://` because the files are not cached in the local file system of GooseFS, but they can still be accessed through the namespace of the underlying storage systems.

## Using the Unified Namespace Capability

You can use the `create ns` instruction to create a namespace in GooseFS and map underlying storage systems to GooseFS. Currently supported underlying storage systems include COS, CHDFS, and local HDFS. The procedure for creating a namespace is similar to that for mounting a file volume disk in a Linux file system. With the namespace created, GooseFS can provide clients with a file system with uniform access semantics. The current operation instruction set for GooseFS namespaces is as follows:

>!
>- We recommend that you avoid using permanent keys in the configuration. Configuring sub-account keys or temporary keys can help improve your business security. When authorizing a sub-account, grant only the permissions of the operations and resources that the sub-account needs, which helps avoid unexpected data leakage.
>- If you must use a permanent key, we recommend that you limit ITS permission scope. This can improve the security by limiting its executable operations, resource scope, and conditions (access IP, etc.).
>

```plaintext
$ goosefs ns
Usage: goosefs ns [generic options]
         [create <namespace> <CosN/Chdfs path> <--wPolicy <1-6>> <--rPolicy <1-5>> [--readonly] [--shared] [--secret fs.cosn.userinfo.secretId=<AKIDxxxxxxx>] [--secret fs.cosn.userinfo.secretKey=<xxxxxxxxxx>] [--attribute fs.ofs.userinfo.appid=1200000000][--attribute fs.cosn.bucket.region=<ap-xxx>/fs.cosn.bucket.endpoint_suffix=<cos.ap-xxx.myqcloud.com>]]
         [delete <namespace>]                                      
         [help [<command>]]                                        
         [ls [-r|--sort=option|--timestamp=option]]                
         [setPolicy [--wPolicy <1-6>] [--rPolicy <1-5>] <namespace>]
         [setTtl [--action delete|free] <namespace> <time to live>]
         [stat <namespace>]                                        
         [unsetPolicy <namespace>]                                 
         [unsetTtl <namespace>] 
```

The instructions are described as follows:

| Instruction        | Description                                                         |
| ----------- | ------------------------------------------------------------ |
| create      | Creates a namespace and maps a remote storage system (UFS) to the namespace. When creating the namespace, you can set cache read and write policies. You need to pass in an authorized key (`secretId` and `secretKey`). |
| delete      | Deletes a specified namespace.                                       |
| ls          | Lists the detailed information of a specified namespace, including the UFS path, creation time, cache policy, and TTL information. |
| setPolicy   | Sets the cache policy of a specified namespace.                             |
| setTtl      | Sets TTL for a specified namespace.                                 |
| stat        | Provides the description of a specified namespace, including the mount point, UFS path, creation time, cache policy, TTL information, persistence status, user group, ACL, last access time, and modification time. |
| unsetPolicy | Resets the cache policy of a specified namespace.                             |
| unsetTtl    | Resets the TTL of a specified namespace.                                 |

### Creating or Deleting Namespaces
By creating a namespace in GooseFS, you can cache frequently accessed hot data from a remote storage system to a local high-performance storage node to provide high-performance data access for local computing businesses. The following shows how to map the COS bucket `example-bucket`, the `example-prefix` directory in the bucket, and the CHDFS to the `test_cos`, `test_cos_prefix`, and `test_chdfs` namespaces respectively.

```plaintext
# Map the COS bucket `example-bucket` to the `test_cos` namespace
$ goosefs ns create test_cos cosn://example-bucket-1250000000/ --wPolicy 1 --rPolicy 1 --secret fs.cosn.userinfo.secretId=AKIDxxxxxxx --secret fs.cosn.userinfo.secretKey=xxxxxxxxxx --attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.bucket.endpoint_suffix=cos.ap-guangzhou.myqcloud.com 

# Map the `example-prefix` directory in the COS bucket `example-bucket` to the `test_cos_prefix` namespace
$ goosefs ns create test_cos_prefix cosn://example-bucket-1250000000/example-prefix/ --wPolicy 1 --rPolicy 1 --secret fs.cosn.userinfo.secretId=AKIDxxxxxxx --secret fs.cosn.userinfo.secretKey=xxxxxxxxxx --attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.bucket.endpoint_suffix=cos.ap-guangzhou.myqcloud.com

# Map the CHDFS `f4ma0l3qabc-Xy3` to the `test_chdfs` namespace
$ goosefs ns create test_chdfs ofs://f4ma0l3qabc-Xy3/ --wPolicy 1 --rPolicy 1 --attribute fs.ofs.userinfo.appid=1250000000
```

After successful creation, you can use the `goosefs fs ls` instruction to view the directory details:
```plaintext
$ goosefs fs ls /test_cos
```

You can use the `delete` instruction to delete unwanted namespaces:

```plaintext
$ goosefs ns delete test_cos
Delete the namespace: test_cos
```

### Setting the cache policy
You can use `setPolicy` and `unsetPolicy` to set the cache policy of a namespace. The instruction set is as follows:
```plaintext
$goosefs ns setPolicy [--wPolicy <1-6>] [--rPolicy <1-5>] <namespace>
```
The parameters are described as follows:
- wPolicy: write cache policy. Up to 6 write cache policies are supported.
- rPolicy: read cache policy. Up to 5 read cache policies are supported.
- namespace: specified namespace

The read and write cache policies currently supported by GooseFS are as follows:

**Write cache policies**

| Policy Name      | Behavior                                                         | Corresponding Write_Type | Data Security | Write Efficiency |
| :------------ | :---------------------------------- | :--------- | :-----  | :-----  |
| MUST_CACHE (1) | Data is stored only in GooseFS and is not written to the remote storage system. | MUST_CACHE | Unreliable     | High     |
| TRY_CACHE (2) | If the cache has space, data is written to GooseFS. Otherwise, data is written directly to underlying storage systems. | TRY_CACHE | Unreliable | Medium |
| CACHE_THROUGH (3) | Data is cached as much as possible and simultaneously written to remote storage systems.                    | CACHE_THROUGH | Reliable       | Low    |
| THROUGH (4)       | Data is not stored in GooseFS, but written directly to the remote storage system.                   | THROUGH | Reliable       | Medium     |
| ASYNC_THROUGH (5) | Data is written to GooseFS and asynchronously purged to remote storage systems.                 | ASYNC_THROUGH | Weak reliability     | High     |

>? 
>- `Write_Type` indicates the file cache policy specified when the user calls the SDK or API to write data to GooseFS. It takes effect only for a single file.
>- If you want to change the configured write cache policy, you need to carefully evaluate the importance of the cached data. If the data is important, we recommend that you ensure that the cached data has been persisted; otherwise, it may be lost. For example, after the write cache is changed from `MUST_CACHE` to `CACHE_THROUGH`, if the `persist` command is not called to persist the data, the data that is about to be eliminated cannot be written to the underlying layer and will be lost.

**Read cache policies**

| Policy Name                      | Behavior                                                         | Metadata Sync | Corresponding Read_Type | Data Consistency | Read Efficiency                  | Whether to Cache Data |
| :---------------------------- | :----------------------------------------------------------- | :--------- | ------------- | :--------- | :---------------------- | :----------- |
| NO_CACHE (1)                 | Data is not cached and is directly read from remote storage systems instead.                     | NO         | NO_CACHE      | Strong     | Low                      | No           |
| CACHE (2)                    | <li>Metadata access behavior: if a cache is hit, the metadata in the master shall prevail. Metadata is not proactively synchronized from the underlying layer.</li><li>Data stream access behavior: the data stream `Read_Type` is `CACHE`.</li> | Once       | CACHE         | Weak     | Hit: high<br/>Not hit: low | Yes           |
| CACHE_PROMOTE (3)            | <li>Metadata access behavior: same as `CACHE`.</li><li>Data stream access behavior: the data stream `Read_Type` is `CACHE_PROMOTE`.</li> | Once       | CACHE_PROMOTE | Weak     | Hit: high<br/>Not hit: low | Yes           |
| CACHE_CONSISTENT_PROMOTE (4) | <li>Metadata access behavior: sync the metadata in the remote storage system (UFS) each time before a read operation. If the data does not exist in the UFS, report the `Not Exists` exception.</li><li>Data stream access behavior: the data stream `Read_Type` is `CACHE_PROMOTE`. If a cache is hit, data is cached to the hottest cache medium.</li> | Always     | CACHE         | Strong     | Hit: medium<br/>Not hit: low | Yes           |
| CACHE_CONSISTENT (5)         | <li>Metadata access behavior: same as `CACHE_CONSISTENT_PROMOTE`. </li><li>Data stream access behavior: the data stream `Read_Type` is `CACHE`. That is, when a cache is hit, data is not moved between different media layers.</li> | Always     | CACHE_PROMOTE | Strong     | Hit: medium<br/>Not hit: low | Yes           |

>? `Read_Type` indicates the file cache policy specified when the user calls the SDK or API to read data from GooseFS. It takes effect only for a single file.
>  

Based on current big data business practices, we recommend the following combinations of read and write cache policies:

| Write Cache Policy                      | Read Cache Policy                                                         | Policy Combination Performance |
| :---------------------------- | :----------------------------------------------------------- | :--------- |
| CACHE_THROUGH (3) | CACHE_CONSISTENT (5) | Strong data consistency between the cache and remote storage systems |
| CACHE_THROUGH (3) | CACHE (2) | Write: strong consistency; read: eventual consistency |
| ASYNC_THROUGH (5) | CACHE_CONSISTENT (5) | Write: eventual consistency; read: strong consistency |
| ASYNC_THROUGH (5) | CACHE (2) | Read/Write: eventual consistency |
| MUST_CACHE (1) | CACHE (2) | Data is read from the cache only. |

The following example shows how to set the read and write cache policies of the `test_cos` namespace to `CACHE_THROUGH` and CACHE_CONSISTENT` respectively:
```plaintext
$ goosefs ns setPolicy --wPolicy 3 --rPolicy 5 test_cos
```

>!In addition to specifying cache policies when creating namespaces, you can also configure global cache policies by setting `Read_Type` or `Write_Type` for specific files when reading or writing files, or by using the `Properties` configuration file. If multiple policies exist at the same time, their priority order is as follows: custom priority > namespace read and write policies > global cache policy configured in the configuration file. For the read policy, the combination of the custom `Read_Type` and the namespace's `DirReadPolicy` takes effect. That is, the custom `Read_Type` is used as the data stream read policy, and the namespace policy is used for metadata. 
>
> For example, GooseFS contains a COSN namespace whose read policy is `CACHE_CONSISTENT` and the namespace contains a `test.txt` file. When the client reads the `test.txt` file, `Read_Type` is specified as `CACHE_PROMOTE`. Then the entire read behavior is to sync metadata and perform `CACHE_PROMOTE`.
> 

To reset the read and write cache policies, you can use the `unsetPolicy` instruction. The following shows how to reset the read and write cache policies for the `test_cos` namespace:
```plaintext
$ goosefs ns unsetPolicy test_cos
```


### Setting TTL

Time to Live (TTL) is used to manage data cached on the local nodes of GooseFS. Setting TTL allows a specified operation, such as `delete` or `free`, to be performed on the cached data after a specified period of time. The instruction for setting TTL is as follows:

```plaintext
$ goosefs ns setTtl [--action delete|free] <namespace> <time to live>
```

The parameters are described as follows:
- action: operation performed after the cache duration expires. Currently, `delete` and `free` are supported. The `delete` operation deletes data from the cache and UFS, while the `free` operation deletes data only from the cache.
- namespace: specified namespace
- time to live: data cache duration, in milliseconds

The following example shows how to set the policy of the `test_cos` namespace to delete data only from the cache after 60 seconds:

```plaintext
$ goosefs ns setTtl --action free test_cos 60000
```

## Metadata management

This section describes how GooseFS manages metadata, including metadata synchronization and updates. GooseFS provides users with unified namespace capability. Users can access files on different underlying storage systems using a unified `gfs://` path. You only need to specify the paths of the underlying storage systems. We recommend that you use GooseFS as a unified data access layer to uniformly read and write data from GooseFS to ensure metadata consistency.

### Metadata synchronization overview

You can configure the metadata synchronization interval in the `conf/goosefs-site.properties` configuration file:

```plaintext
goosefs.user.file.metadata.sync.interval=<INTERVAL>
```


The metadata synchronization interval parameter supports 3 types of input values:

- -1: metadata is not updated after it is first loaded into GooseFS.
- 0: GooseFS updates metadata after each read/write operation.
- Positive integer: GooseFS periodically updates metadata at a specified interval.

You can choose an appropriate synchronization interval based on your number of nodes, the I/O distance between your GooseFS cluster and the underlying storage system, and the type of the underlying storage system. Usually:

- The greater the number of nodes in a GooseFS cluster, the greater the metadata synchronization delay.
- The greater the distance between the GooseFS cluster and the underlying storage system, the greater the metadata synchronization delay.
- The impact of the underlying storage system on the metadata synchronization delay depends on the QPS load. The higher the QPS load, the less the synchronization delay.

### Metadata synchronization management

## Configuration methods

1. Configuration via CLI
You can set the metadata synchronization interval in command line interface (CLI) mode:
```plaintext
goosefs fs ls -R -Dgoosefs.user.file.metadata.sync.interval=0 <path to sync>
```
2. Configuration via the configuration file
For a large-scale GooseFS cluster, you can use the `goosefs-site.properties` configuration file to batch configure the metadata synchronization interval for the master nodes in the cluster, and other nodes will adopt this interval by default.
```plaintext
goosefs.user.file.metadata.sync.interval=1m
```

>! Many businesses choose to distinguish the purpose of data by directory, and the data access frequencies of different directories are not all the same. You can set different metadata synchronization intervals for different directories. For some directories that change frequently, the metadata synchronization interval can be set to a shorter time (such as 5 minutes). For directories that change little or do not change, the synchronization interval can be set to `-1`, so that GooseFS will not automatically synchronize the metadata of the directories.
>

#### Recommended configuration

You can set different metadata synchronization intervals based on business access modes:

<table>
   <tr>
      <td colspan=2>Access Mode</td>
      <td>Metadata Synchronization Interval</td>
      <td>Description</td>
   </tr>
   <tr>
      <td colspan=2>All file requests go through GooseFS</td>
      <td>-1</td>
      <td>-</td>
   </tr>
   <tr>
      <td rowspan=2>Most file requests go through GooseFS</td>
      <td>HDFS is used as UFS</td>
      <td>Hot update or update by path is recommended</td>
      <td>If the HDFS updates frequently, you are advised to set the update interval to `-1` to prohibit updates.</td>
   </tr>
   <tr>
      <td>COS is used as UFS</td>
      <td>Configuring update intervals by path is recommended</td>
      <td rowspan=3>Configuring different update intervals for different directories can alleviate the pressure of metadata synchronization.</td>
   </tr>
   <tr>
      <td rowspan=2>File upload requests generally do not go through GooseFS</td>
      <td>HDFS is used as UFS</td>
      <td>Configuring update intervals by path is recommended</td>
   </tr>
   <tr>
      <td>COS is used as UFS</td>
      <td>Configuring update intervals by path is recommended</td>
   </tr>
</table>
