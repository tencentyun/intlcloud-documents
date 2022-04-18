## Overview

In COS, you can enable metadata acceleration to gain the HDFS protocol access capability. After metadata acceleration is enabled, COS generates a mount point for your bucket. Then you can download the [HDFS client](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) and use the mount point in the client to mount COS. This document introduces how to mount a bucket with metadata acceleration enabled to a computing cluster.

## Prerequisites

- [Java 1.8](https://www.oracle.com/java/technologies/downloads/) is installed on the computing cluster's machine or container to be mounted.
- The computing cluster's machine or container to be mounted is authorized with the access permission. You need to specify the VPC and IP that can be accessed in the HDFS permission configuration.

## Directions

1. Download the [Hadoop client installation package](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar).
2. Place the installation package in the directory corresponding to the computing job. For an EMR cluster, it can be synced to the `/usr/local/service/hadoop/share/hadoop/common/lib/` directory of all nodes.
3. Edit the `core-site.xml` file to add the following basic configuration:
```
<!--Implementation class of CHDFS-->
<property>
		 <name>fs.AbstractFileSystem.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>

<!--Implementation class of CHDFS-->
<property>
		 <name>fs.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>

<!--Temporary directory of the local cache. For data read/write, data will be written to the local disk when the memory cache is insufficient. This path will be created automatically if it does not exist-->
<property>
		 <name>fs.ofs.tmp.cache.dir</name>
		 <value>/data/chdfs_tmp_cache</value>
</property>

<!--Your appId, which can be obtained in the Tencent Cloud console at https://console.cloud.tencent.com/developer-->      
<property>
		 <name>fs.ofs.user.appid</name>
		 <value>1250000000</value>
</property>

<!--Flush semantics. Defaults to `false` (async flush). See the data visibility and persistence details in the figure below -->      
<property>
		 <name>fs.ofs.upload.flush.flag</name>
		 <value>false</value>
</property>

```
4. Sync `core-site.xml` to all Hadoop nodes.
>?For an EMR cluster, you only need to modify the HDFS configuration in component management in the EMR console for the above steps 3 and 4.
>
5. Use the `hadoop fs` command line tool to run the `hadoop fs -ls ofs://${bucketname-appid}/` command. Here, `bucketname-appid` is the mount address, i.e., bucket name. If the file list is output properly, the COS bucket has been mounted successfully.
6. You can also use other configuration items of Hadoop or MR tasks to run data tasks on the bucket with metadata acceleration enabled. For an MR task, you can change the default input and output file systems of the task to the corresponding bucket through `-Dfs.defaultFS=ofs://${bucketname-appid}/`.

## Scenario Description

### Data visibility and persistence

With metadata acceleration enabled, COS can be used as a cloud distributed file system. When a file is opened using the Hadoop client tool, the client will asynchronously flush the file when a certain size (usually 4 MB) is reached and write the data to the COS bucket on the public cloud. If the upper-layer computing service proactively calls the flush API of the data output stream, **this call to the flush API is ignored by default (this behavior is different from the general sync flush semantics)**, and the client waits for the data to be written to reach a certain amount before asynchronously flushing the data. The client force executes sync flush when `Close` is called finally. After successful processing of 'Close', the data is persisted successfully and can be read properly in the future.

The Hadoop client tool uses async flush by default because cloud access delay is higher than local disk access delay. Async flush reduces the interaction with the cloud and prevents flush operations from blocking user write operations, significantly improving write performance and reducing job time. The risk point is that if the `Close` API is not proactively called in the end, unflushed data may be lost.

Therefore, **for data that needs to be written in real time to ensure immediate visibility and persistence to the cloud, such as `Hbase Wal Log` and `Journal` logs, enable sync flush by referring to the description of the configuration item `fs.ofs.upload.flush.flag`.**

## Configuration Items

|        Configuration Item      |                             Description                             |  Default Value   | Required |
| :------------------------------| :----------------------------------------------------| :-------| :------ |
|       fs.ofs.tmp.cache.dir        |   Stores temporary data    |    None     |    Yes    |
|       fs.ofs.map.block.size       | The client divides data into blocks when writing the data, and this configuration item specifies the data block size, in bytes. The default value is 128 MB (this item only affects map segmentation and has nothing to do with the size of the underlying storage block of CHDFS) | 134217728 |    No    |
| fs.ofs.data.transfer.thread.count |               Number of parallel threads when the client transfers data                |    32     |    No    |
| fs.ofs.block.max.memory.cache.mb  | Size of the memory buffer used by the client plugin in MB (which accelerates both reads and writes) |    16     |    No    |
|  fs.ofs.block.max.file.cache.mb   |  Size of the disk buffer used by the CHDFS plugin in MB (which accelerates writes)  |    256    |    No    |
|   fs.ofs.prev.read.block.count    | Number of data blocks read ahead during reads (the block size is generally 4 MB). (For random read scenarios, decrease the value as needed. For sequential read scenarios, increase the value and the size of the memory buffer as needed.) |     4     |    No    |
|  fs.ofs.prev.read.block.release.enable| Specifies whether to release the buffer of the last data block that has been read. For sequential read scenarios, enable this option. For random read scenarios, if certain data is frequently read, you are advised to disable this option. Valid values: `true` (enabled), `false` (disabled) | `true` | No |
|      fs.ofs.plugin.info.log       |          Specifies whether to print client debugging logs. Logs are printed at the info level. Valid values: `true` (enabled), `false` (disabled) |   false   |    No    |
|      fs.ofs.upload.flush.flag     | Specifies whether to flush data synchronously when the output stream flush API is called during data writes. The default value is `false` (async flush). If sync flush is required, set this configuration item to `true`. | false | No |

