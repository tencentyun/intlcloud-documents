## Overview

Hadoop Distcp (Distributed copy) is a tool used for large inter- and intra-cluster copying. It uses MapReduce to effect its distribution, error handling and recovery, and reporting. With MapReduce parallel processing capabilities, it migrates massive data fast through map tasks, each of which will copy a partition of the files specified under the source path.

Since Hadoop-COS implements the semantics of Hadoop Distributed File System (HDFS), it can help you easily migrate data between COS and HDFS. This document will describe how to do so.

## Prerequisites

1. The [Hadoop-COS] (https://intl.cloud.tencent.com/document/product/436/6884) plugin has been installed on the Hadoop cluster, and the access key for COS has been configured correctly. You can use the following Hadoop command to check if COS access is normal:
```shell
hadoop fs -ls cosn://examplebucket-1250000000/
```
If a correct list of COS buckets is returned, Hadoop-COS works well, and you can begin the practice below.
2. The COS account must have read and write permissions for the destination path in COS bucket.

## Directions

### Copying files from HDFS to COS bucket

Use Hadoop Distcp to migrate files in the `/ test` directory of the local HDFS cluster to the COS bucket `hdfs-test-1250000000`.

![](https://main.qcloudimg.com/raw/e20dce07b83846362d02b3c6a1987558.jpg)

1. Run the following command to start the migration:

```shell
hadoop distcp hdfs://10.0.0.3:9000/test cosn://hdfs-test-1250000000/
```

Hadoop Distcp starts MapReduce tasks to copy the files, and outputs a brief report like so:
![](https://main.qcloudimg.com/raw/39e84dcb98386f343ad81fcc48f78af1.jpg)

2. Run the `hadoop fs -ls -R cosn://hdfs-test-1250000000/` command to list directories and files that have just been migrated to the bucket `hdfs-test-1250000000`.

![](https://main.qcloudimg.com/raw/ca34582214652ad77afe99322e6894fc.png)

### Copying files from COS bucket to a local HDFS cluster

Hadoop Distcp is a tool that supports copying data between different clusters and file systems. To copy COS files to local HDFS, simply using the object path in COS bucket as the source path and the HDFS file path as the destination path.

```shell
hadoop distcp cosn://hdfs-test-1250000000/test hdfs://10.0.0.3:9000/
```

### Using the Distcp command line to migrate data between HDFS and COS

>With this command line, you can migrate data from HDFS to COS, and vice versa.

Run the following command:
```plaintext
hadoop distcp -Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem -Dfs.cosn.bucket.region=ap-XXX  -Dfs.cosn.userinfo.secretId=AK**XXX  -Dfs.cosn.userinfo.secretKey=XXXX  -libjars /home/hadoop/hadoop-cos-2.6.5-shaded.jar  cosn://bucketname-appid/test/ hdfs:///test/
```

Parameter description:

- Dfs.cosn.impl: is always `org.apache.hadoop.fs.CosFileSystem`.
- Dfs.cosn.bucket.region: bucket region which you can view in the COS console.
- Dfs.cosn.userinfo.secretId: SecretId in the bucket owner’s account; can be accessed from the [API Key Management](https://console.cloud.tencent.com/capi) page.
- Dfs.cosn.userinfo.secretKey: secretKey in the bucket owner’s account; can be accessed from the [API Key Management](https://console.cloud.tencent.com/capi) page.
- libjars: specifies the location of Hadoop-COS jar file. Download this file from the `dep` directory on [Github](https://github.com/tencentyun/hadoop-cos).

>For any other parameters, see [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884).


## Additional Hadoop distcp Parameters

Hadoop Distcp supports a variety of parameters. For example, you can use `-m` to specify the maximum number of Map tasks for parallel replication, and` -bandwidth` to limit the maximum bandwidth used by each map. For more information, see the Apache Hadoop Distcp documentation [DistCp Guide](https://hadoop.apache.org/docs/current/hadoop-distcp/DistCp.html).


