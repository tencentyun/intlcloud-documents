
This document describes how to mount a CHDFS instance. After creating a CHDFS instance and a mount point, you can mount the instance to the mount point.

## Prerequisites
- The target server or container has Java 1.8 installed.
- The target server or container and the mount point are in the same VPC.
- The VPC IP of the target server or container matches the address authorized by a permission rule in the specified permission group of the mount point.

## Directions
1. Download the [CHDFS for Hadoop](https://github.com/tencentyun/chdfs-hadoop-plugin) JAR package.
2.	Place the JAR package in the corresponding directory. For an EMR cluster, it can be synced to the `/usr/local/service/hadoop/share/hadoop/common/lib/` directory of all nodes.
3.Edit the `core-site.xml` file to add the following basic configuration:
```
<!--Implementation class of CHDFS-->
<property>
		 <name>fs.AbstractFileSystem.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>
<property>
		 <name>fs.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>
<!--Temporary directory of the local cache. For data read/write, data will be written to the local disk when the memory cache is insufficient. This path will be created automatically if it does not exist-->
<property>
		 <name>fs.ofs.tmp.cache.dir</name>
		 <value>/data/chdfs_tmp_cache</value>
</property>
<!--appId-->      
<property>
		 <name>fs.ofs.user.appid</name>
		 <value>1250000000</value>
</property>
```
4.	Sync `core-site.xml` to all Hadoop nodes.
>?For an EMR cluster, you only need to modify the HDFS configuration in component management in the EMR console for the above steps 3 and 4.
5.	Use the `hadoop fs` command line tool to run the `hadoop fs –ls ofs://${mountpoint}/` command. Here, `mountpoint` is the mount address. If the file list is output properly, the CHDFS instance has been mounted successfully.
6.	You can also use other configuration items of Hadoop or MR tasks to run data tasks on CHDFS. For an MR task, you can change the default input and output file systems of the task to `CHDFS` through `-Dfs.defaultFS=ofs://${mountpoint}/`.

## Other Configuration Items

|        Configuration Item      |                             Description                             |  Default Value   | Required |
| :------------------------------| :----------------------------------------------------| :-------| :------ |
|       fs.ofs.tmp.cache.dir        |   Stores temporary data    |    None     |    Yes    |
|       fs.ofs.map.block.size       | Block size of the CHDFS file system in bytes. The default value is 128 MB (this item only affects map segmentation and has nothing to do with the size of the underlying storage block of CHDFS) | 134217728 |    No    |
| fs.ofs.data.transfer.thread.count |               Number of parallel threads when CHDFS transfers data                |    32     |    No    | 
| fs.ofs.block.max.memory.cache.mb  | Size of the memory buffer used by the CHDFS plugin in MB (which accelerates both reads and writes) |    16     |    No    |
|  fs.ofs.block.max.file.cache.mb   |  Size of the disk buffer used by the CHDFS plugin in MB (which accelerates writes)  |    256    |    No    |
|   fs.ofs.prev.read.block.count    | Number of CHDFS blocks read ahead during reads (the size of the underlying block of CHDFS is generally 4 MB)|     4     |    No    |
|      fs.ofs.plugin.info.log       |          Specifies whether to print plugin debugging logs. Logs are printed at the info level. Valid values: true, false |   false   |    No    |

