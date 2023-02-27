## Overview
COS offers the metadata acceleration feature to provide high-performance file system capabilities. Metadata acceleration leverages the powerful metadata management feature of Cloud HDFS (CHDFS) at the underlying layer to allow using file system semantics for COS access. The designed system metrics can reach a bandwidth of up to 100 GB/s, over 100,000 queries per second (QPS), and a latency of milliseconds. Buckets with metadata acceleration enabled can be widely used in scenarios such as big data, high-performance computing, machine learning, and AI. For more information on metadata acceleration, see [Metadata Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/43305).

COS provides the Hadoop semantics through the metadata acceleration service. Therefore, you can use [COSDistCp](https://intl.cloud.tencent.com/document/product/436/38863) to easily implement two-way data migration between COS and other Hadoop file systems. This document describes how to use COSDistCp to migrate files in the local HDFS to a metadata acceleration bucket in COS.

## Environment Preparations Before Migration

### Migration tools


1. Download the JAR packages of the tools as listed below and place them in the local directory on the node running the migration task in the cluster, such as `/data01/jars`.

<b>EMR environment</b>
 
**Installation notes**

<table>
<thead>
<tr><th>JAR Filename</th><th>Description</th><th>Download Address</th></tr>
</thead>
<tbody>
<tr>
<td>cos-distcp-1.12-3.1.0.jar</td>
<td>COSDistCp package, whose data needs to be copied to COSN.</td>
<td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/38863">COSDistCp</a>.</td>
</tr>
<tr>
<td>chdfs_hadoop_plugin_network-2.8.jar</td>
<td>OFS plugin</td>
<td><a href="https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar">Download</a>.</td>
</tr>
</tbody>
</table>


<b>Self-built environment such as Hadoop or CDH</b>

**Software dependency**

Hadoop 2.6.0 or later and Hadoop-COS 8.1.5 or later are required. The cos_api-bundle plugin version must match the Hadoop-COS version as described in <a href="https://github.com/tencentyun/hadoop-cos/releases">Releases</a>.

**Installation notes**

Install the following plugins in the Hadoop environment:
<table>
<thead>
<tr><th>JAR Filename</th><th>Description</th><th>Download Address</th></tr>
</thead>
<tbody>
<tr>
<td>cos-distcp-1.12-3.1.0.jar</td>
<td>COSDistCp package, whose data needs to be copied to COSN.</td>
<td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/38863">COSDistCp</a>.</td>
</tr>
<tr>
<td>chdfs_hadoop_plugin_network-2.8.jar</td>
<td>OFS plugin</td>
<td><a href="https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar">Download</a></td>
</tr>
<tr>
<td>Hadoop-COS</td>
<td>8.1.5 or later</td>
<td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6884">Hadoop</a>.</td>
</tr>
<tr>
<td>cos_api-bundle</td>
<td>The version needs to match the Hadoop-COS version.</td>
<td><a href="https://github.com/tencentyun/hadoop-cos/releases">Download</a>.</td>
</tr>
</tbody>
</table>

>!
>- Hadoop-COS supports access to metadata acceleration buckets in the format of `cosn://bucketname-appid/` starting from v8.1.5.
> - The metadata acceleration feature can only be enabled during bucket creation and cannot be disabled once enabled. Therefore, carefully consider whether to enable it based on your business conditions. You should also note that legacy Hadoop-COS packages cannot access metadata acceleration buckets.

2. Create a metadata acceleration bucket and configure the HDFS protocol for it as instructed in "Creating Bucket and Configuring the HDFS Protocol" in [Using HDFS to Access Metadata Acceleration-Enabled Bucket](https://intl.cloud.tencent.com/document/product/436/46198).
3. Modify the migration cluster's `core-site.xml` and distribute the configuration to all nodes. If only data needs to be migrated, you don't need to restart the big data component.
<table>
<thead>
<tr><th>Key</th><th>Value</th><th>Configuration File</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td>fs.cosn.trsf.fs.ofs.impl</td>
<td>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</td>
<td>core-site.xml</td>
<td>COSN implementation class, which is required.</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl</td>
<td>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</td>
<td>core-site.xml</td>
<td>COSN implementation class, which is required.</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.tmp.cache.dir</td>
<td>In the format of `/data/emr/hdfs/tmp/`</td>
<td>core-site.xml</td>
<td>Temporary directory, which is required. It will be created on all MRS nodes. You need to ensure that there are sufficient space and permissions.</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.user.appid</td>
<td>`appid` of your COS bucket</td>
<td>core-site.xml</td>
<td>Required</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.ranger.enable.flag</td>
<td>false</td>
<td>core-site.xml</td>
<td>This key is required. You need to check whether the value is `false`.</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.bucket.region</td>
<td>Bucket region</td>
<td>core-site.xml</td>
<td>This key is required. Valid values: eu-frankfurt (Frankfurt), ap-chengdu (Chengdu), and ap-singapore (Singapore).</td>
</tr>
</tbody>
</table>
4. You can verify the migration by accessing the metadata acceleration bucket over the private network as instructed in "Configuring Computing Cluster to Access COS" in [Using HDFS to Access Metadata Acceleration-Enabled Bucket](https://intl.cloud.tencent.com/document/product/436/46198). Use the migration cluster submitter to verify whether COS can be accessed successfully.



## Existing Data Migration

### 1. Determine the directories to be migrated

Generally, HDFS storage data will be first migrated. The directory to be migrated in the source HDFS cluster will be selected, and the target path needs to be the same as the source path.

Suppose you need to migrate the HDFS directory `hdfs:///data/user/target` to `cosn://{bucketname-appid}/data/user/target`.

To ensure that the files in the source directory remain unchanged during migration, the snapshot feature of HDFS will be used to create a snapshot of the source directory (named the current date).

```shell
hdfs dfsadmin -disallowSnapshot hdfs:///data/user/
hdfs dfsadmin -allowSnapshot hdfs:///data/user/target
hdfs dfs -deleteSnapshot hdfs:///data/user/target {current date}
hdfs dfs -createSnapshot hdfs:///data/user/target {current date}
```

Sample successful execution:
![](https://qcloudimg.tencent-cloud.cn/raw/b96ef1500668c059909eb1ced5744a3f.png)

If you don't want to create a snapshot, you can directly migrate the target files in the source directory.

### 2. Use COSDistCp for migration

Start a COSDistCp task to copy files from the source HDFS to the target COS bucket.

A COSDistCp task is essentially a MapReduce task. The printed MapReduce task log will show whether the task is executed successfully. If the task fails, you can view the YARN page and submit the log or exception information to the COS team for troubleshooting. You can use COSDistCp to execute a migration task in the following steps:
(1) Create a temporary directory.
(2) Run a COSDistCp task.
(3) Migrate failed files again.

#### (1) Create a temporary directory

```shell
hadoop fs -libjars /data01/jars/chdfs_hadoop_plugin_network-2.8.jar -mkdir cosn://bucket-appid/distcp-tmp
```

#### (2) Run a COSDistCp task

```shell
nohup hadoop jar /data01/jars/cos-distcp-1.10-2.8.5.jar -libjars  /data01/jars/chdfs_hadoop_plugin_network-2.8.jar --src=hdfs:///data/user/target/.snapshot/{current date}  --dest=cosn://{bucket-appid}/data/user/target   --temp=cosn://bucket-appid/distcp-tmp/ --preserveStatus=ugpt  --skipMode=length-checksum --checkMode=length-checksum --cosChecksumType=CRC32C --taskNumber 6 --workerNumber 32 --bandWidth 200 >> ./distcp.log &
```

The parameters are as detailed below. You can adjust their values as needed.
- --taskNumber=VALUE: Number of copy threads. Example: `--taskNumber=10`.
-  --workerNumber=VALUE: Number of copy threads. COSDistCp will create a copy thread pool for each copy process based on this value set. Example: `workerNumber=4`.
-  --bandWidth: Maximum bandwidth for reading each migrated file (in MB/s). Default value: `-1`, which indicates no limit on the read bandwidth. Example: `--bandWidth=10`.
- --cosChecksumType=CRC32C: CRC32C is used by default, but the HDFS cluster must be able to check `COMPOSITE_CRC32`. The Hadoop version must be 3.1.1 or later; otherwise, you need to change this parameter to `--cosChecksumType=CRC64`.

>!The formula for calculating the total bandwidth limit of COSDistCp migration is: taskNumber * workerNumber * bandWidth. You can set `workerNumber` to `1`, use the `taskNumber` parameter to control the number of concurrent migrations, and use the `bandWidth` parameter to control the bandwidth of a single concurrent migration.

When the copy operation ends, the task log will output statistics on the copy. The counters are as follows:
Here, `FILES_FAILED` indicates the number of failed files. If there is no `FILES_FAILED` counter, all files have been migrated successfully.
```
CosDistCp Counters
        BYTES_EXPECTED=10198247
        BYTES_SKIPPED=10196880
        FILES_COPIED=1
        FILES_EXPECTED=7
        FILES_FAILED=1
        FILES_SKIPPED=5

```

The specific statistics items in the output result are as detailed below:

| Statistics Item | Description |
| --------------- | -------------------------------------------------- |
|  BYTES_EXPECTED | Total size (in bytes) to copy according to the source directory |
|  FILES_EXPECTED | Number of files to copy according to the source directory, including  the directory itself |
| BYTES_SKIPPED | Total size (in bytes) of files that can be skipped (same length or checksum value) |
| FILES_SKIPPED | Number of source files that can be skipped (same length or checksum value) |
| FILES_COPIED | Number of source files that are successfully copied |
| FILES_FAILED | Number of source files that failed to be copied |
| FOLDERS_COPIED  | Number of directories that are successfully copied |
| FOLDERS_SKIPPED  | Number of directories that are skipped |


#### 3. Migrate failed files again

COSDistCp not only solves most problems of inefficient file migration but also allows you to use the `--delete` parameter to guarantee the complete consistency between the HDFS and COS data.

When using the `--delete` parameter, you need to add the `--deleteOutput=/xxx(custom)` parameter but not the `--diffMode` parameter.

```shell
nohup hadoop jar /data01/jars/cos-distcp-1.10-2.8.5.jar -libjars /data01/jars/chdfs_hadoop_plugin_network-2.8.jar --src=--src=hdfs:///data/user/target/.snapshot/{current date} --dest=cosn://{bucket-appid}/data/user/target --temp=cosn://bucket-appid/distcp-tmp/ --preserveStatus=ugpt --skipMode=length-checksum --checkMode=length-checksum --cosChecksumType=CRC32C --taskNumber 6 --workerNumber 32 --bandWidth 200 --delete --deleteOutput=/dele-xx >> ./distcp.log &
```

After execution, the different data between HDFS and COS will be moved to the `trash` directory, and the list of moved files will be generated in the `/xxx/failed` directory. You can run `hadoop fs -rm URL` or `hadoop fs -rmr URL` to delete the data in the `trash` directory.

## Incremental Migration

If any incremental data needs to be migrated afterwards, you only need to repeat the steps of full migration until all data has been migrated.

