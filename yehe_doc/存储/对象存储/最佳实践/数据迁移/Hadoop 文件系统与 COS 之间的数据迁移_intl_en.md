## Overview

Hadoop Distcp (Distributed copy) is a tool used for large inter- and intra-cluster copying. It uses MapReduce to perform distribution, error handling, recovery, and reporting. With the parallel processing capabilities of MapReduce, Hadoop Distcp can quickly perform large-scale data migration through map tasks, each of which copies a portion of the files specified under the source path.

Since Hadoop-COS implements the semantics of the Hadoop Distributed File System (HDFS), Hadoop Distcp can help you easily migrate data between COS and HDFS. This document outlines this process below.

## Prerequisites

1. The [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884) plugin has been installed on the Hadoop cluster, and the access key for COS has been configured correctly. You can use the following Hadoop command to check if there are any issues accessing COS:
```shell
hadoop fs -ls cosn://examplebucket-1250000000/
```
If a correct list of COS buckets is returned, there are no issues with Hadoop-COS, and you can begin the steps outlined below.
2. The COS account must have read and write permissions for the destination path of COS bucket.

## Directions

### Copying files from HDFS to a COS bucket

Use Hadoop Distcp to migrate files in the `/ test` directory of the local HDFS cluster to the COS bucket `hdfs-test-1250000000`.

![](https://main.qcloudimg.com/raw/e20dce07b83846362d02b3c6a1987558.jpg)

1. Run the following command to start the migration:

```shell
hadoop distcp hdfs://10.0.0.3:9000/test cosn://hdfs-test-1250000000/
```

Hadoop Distcp starts MapReduce tasks to copy the files, and outputs a brief report like so:
![](https://main.qcloudimg.com/raw/39e84dcb98386f343ad81fcc48f78af1.jpg)

2. Run the `hadoop fs -ls -R cosn://hdfs-test-1250000000/` command to list the directories and files that have just been migrated to the bucket `hdfs-test-1250000000`.

![](https://main.qcloudimg.com/raw/ca34582214652ad77afe99322e6894fc.png)

### Copying files from a COS bucket to a local HDFS cluster

Hadoop Distcp is a tool that supports copying data between different clusters and file systems. To copy COS files to a local HDFS cluster, simply use the object path in the COS bucket as the source path and the HDFS file path as the destination path.

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

- Dfs.cosn.impl is always `org.apache.hadoop.fs.CosFileSystem`.
- Dfs.cosn.bucket.region: bucket region; you can view the region on the bucket list page of the COS console.
- Dfs.cosn.userinfo.secretId: Enter the secretId of the bucket owner’s account; this value can be accessed from the [API Key Management](https://console.cloud.tencent.com/capi) page.
- Dfs.cosn.userinfo.secretKey: Enter the secretKey of the bucket owner’s account; this value can be accessed from the [API Key Management](https://console.cloud.tencent.com/capi) page.
- libjars: specifies the location of the Hadoop-COS jar file. Download this file from the `dep` directory which you can find on [Github](https://github.com/tencentyun/hadoop-cos).

>For any other parameters, see [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884).


## Additional Hadoop distcp Parameters

Hadoop Distcp supports a variety of parameters. For example, you can use `-m` to specify the maximum number of concurrent Map tasks, and` -bandwidth` to limit the maximum bandwidth used by each map. For more information, see the [Apache Hadoop DistCp Guide](https://hadoop.apache.org/docs/current/hadoop-distcp/DistCp.html).


