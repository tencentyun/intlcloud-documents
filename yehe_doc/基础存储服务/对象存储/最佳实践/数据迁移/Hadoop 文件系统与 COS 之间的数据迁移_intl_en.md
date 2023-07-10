## Overview

Hadoop DistCp (Distributed copy) is a tool used for large inter- and intra-cluster copying. It uses MapReduce to perform distribution, error handling, recovery, and reporting. With the parallel processing capabilities of MapReduce, Hadoop DistCp can quickly perform large-scale data migration through map tasks, each of which copies a portion of the files specified under the source path.

Since Hadoop-COS implements the semantics of the Hadoop Distributed File System (HDFS), Hadoop DistCp can help you easily migrate data between COS and HDFS. This document outlines this process below.

## Prerequisites

1. The [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884) plugin has been installed on the Hadoop cluster, and the access key for COS has been configured correctly. You can use the following Hadoop commands to check if COS access is normal:
```shell
hadoop fs -ls cosn://examplebucket-1250000000/
```
If the files in the COS bucket can be listed correctly, it means that Hadoop-COS has been installed and configured correctly, and the following steps can be performed.
2. The COS access account must have read and write permission for the destination path of the COS bucket.

>!
>- You can authorize sub-accounts read/write permissions for resources in the COS bucket as needed. You are advised to authorize by referring to [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) and [Setting Sub-user Permissions](https://intl.cloud.tencent.com/document/product/598/32650). The common preset policies are as follows:
>  - [DataFullControl](https://console.cloud.tencent.com/cam/policy/detail/5294998&QcloudCOSDataFullControl&2): full control over data, including the permission to read, write, as well as delete files, and list the file list.
>  - [QcloudCOSDataReadOnly](https://console.cloud.tencent.com/cam/policy/detail/5295051&QcloudCOSDataReadOnly&2): read-only permission
>  - [QcloudCOSDataWriteOnly](https://console.cloud.tencent.com/cam/policy/detail/5295044&QcloudCOSDataWriteOnly&2): write-only permission
>- The custom monitoring feature requires Cloud Monitoring to have permission to report metrics and read API operations. Please grant the [QcloudMonitorFullAccess](https://console.cloud.tencent.com/cam/policy/detail/276210&QcloudMonitorFullAccess&2) permission with caution.

## Directions

### Copying files from HDFS to a COS bucket

Use Hadoop DistCp to migrate files in the `/ test` directory of the local HDFS cluster to the COS bucket `hdfs-test-1250000000`.

![](https://main.qcloudimg.com/raw/e20dce07b83846362d02b3c6a1987558.jpg)

1. Run the following command to start the migration:

```shell
hadoop distcp hdfs://10.0.0.3:9000/test cosn://hdfs-test-1250000000/
```

Hadoop DistCp starts MapReduce tasks to copy the files, and outputs a brief report like so:
![](https://main.qcloudimg.com/raw/39e84dcb98386f343ad81fcc48f78af1.jpg)

2. Run the `hadoop fs -ls -R cosn://hdfs-test-1250000000/` command to list the directories and files that have just been migrated to the bucket `hdfs-test-1250000000`.

![](https://main.qcloudimg.com/raw/ca34582214652ad77afe99322e6894fc.png)

### Copying files from a COS bucket to a local HDFS cluster

Hadoop DistCp is a tool that supports copying data between different clusters and file systems. To copy COS files to a local HDFS cluster, simply use the object path in the COS bucket as the source path and the HDFS file path as the destination path.

```shell
hadoop distcp cosn://hdfs-test-1250000000/test hdfs://10.0.0.3:9000/
```

### Using the DistCp command line to migrate data between HDFS and COS

>?With this command line, you can migrate data from HDFS to COS, and vice versa.

Run the following command:
```plaintext
hadoop distcp -Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem -Dfs.cosn.bucket.region=ap-XXX  -Dfs.cosn.userinfo.secretId=AK**XXX  -Dfs.cosn.userinfo.secretKey=XXXX  -libjars /home/hadoop/hadoop-cos-2.6.5-shaded.jar  cosn://bucketname-appid/test/ hdfs:///test/
```

Parameter description:

- Dfs.cosn.impl: Always set it to `org.apache.hadoop.fs.CosFileSystem`.
- Dfs.cosn.bucket.region: bucket region. You can view the region on the bucket list page of the COS console.
- Dfs.cosn.userinfo.secretId: Enter the `SecretId` of the bucket owner’s account. The value can be obtained at [Manage API Key](https://console.cloud.tencent.com/capi).
- Dfs.cosn.userinfo.secretKey: Enter the `SecretKey` of the bucket owner’s account. The value can be obtained at [Manage API Key](https://console.cloud.tencent.com/capi).
- libjars: specifies the location of the Hadoop-COS JAR package. You download the package from the `dep` directory at [GitHub repository](https://github.com/tencentyun/hadoop-cos).

>?For other parameters, please see [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884).


## Additional Hadoop DistCp Parameters

Hadoop DistCp supports a variety of parameters. For example, you can use `-m` to specify the maximum number of concurrent Map tasks, and` -bandwidth` to limit the maximum bandwidth used by each map. For more information, please see [Apache Hadoop DistCp Guide](https://hadoop.apache.org/docs/current/hadoop-distcp/DistCp.html).


