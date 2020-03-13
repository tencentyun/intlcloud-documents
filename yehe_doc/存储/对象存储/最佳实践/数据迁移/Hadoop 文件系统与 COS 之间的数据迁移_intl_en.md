## Introduction

Hadoop Distcp (Distributed copy) is a tool for large-scale data copying within or between Hadoop file systems. It implements file distribution, error handling, and report generation based on Map/Reduce. Due to the parallel processing capabilities of Map/Reduce, each Map job is responsible for copying files in its source path, fully utilizing cluster resources to quickly complete large-scale data migration between clusters or Hadoop file systems.

Because Hadoop-COS implements the semantics of the Hadoop file system, the Hadoop Distcp tool can be used to facilitate two-way data migration between COS and other Hadoop file systems. The following uses HDFS as an example to introduce how to use Hadoop Distcp tools to complete the data migration between Hadoop file systems and COS.

## Prerequisites

1. The [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884) plugin has been installed on the Hadoop cluster, and the access key for COS has been configured correctly. You can use the following Hadoop commands to check if COS access is normal:
```shell
hadoop fs -ls -R cosn://examplebucket-1250000000/
```
If the file list in COS Bucket can be listed correctly, it means that Hadoop-COS has been installed and configured correctly, and the following steps can be performed.
2. The COS access account must have read and write permissions to the destination path in COS bucket.

## Steps

### Copy data from HDFS to COS bucket

Use Hadoop Distcp to migrate files in the `/ test` directory of the local HDFS cluster to the hdfs-test-1250000000 COS bucket.

![](https://main.qcloudimg.com/raw/e20dce07b83846362d02b3c6a1987558.jpg)

1. Run the following command to start the migration:

```shell
hadoop distcp hdfs://10.0.0.3:9000/test cosn://hdfs-test-1250000000/
```

Hadoop Distcp will start MapReduce to perform the file copying job, and output simple report information after completion, as shown in the figure below:
![](https://main.qcloudimg.com/raw/39e84dcb98386f343ad81fcc48f78af1.jpg)

2. Run the `hadoop fs -ls -R cosn://hdfs-test-1250000000/` command to list directories and files that have just been migrated to the bucket hdfs-test-1250000000.

![](https://main.qcloudimg.com/raw/ca34582214652ad77afe99322e6894fc.png)

### Copy files from buckets in COS to a local HDFS cluster

Hadoop Distcp is a tool that supports copying data between different clusters and file systems. Therefore, using the object path in COS bucket as the source path and the HDFS file path as the destination path allows you to copy data files in COS to the local HDFS:

```shell
hadoop distcp cosn://hdfs-test-1250000000/test hdfs://10.0.0.3:9000/
```

## Additional Hadoop distcp parameters

The Hadoop distcp tool supports a variety of operating parameters. For example, you can use `-m` to specify the maximum number of Map jobs for parallel replication, and` -bandwidth` to limit the maximum bandwidth used by each map. For details, refer to the official document of the Apache Hadoop distcp tool: [DistCp Guide](https://hadoop.apache.org/docs/current/hadoop-distcp/DistCp.html).

