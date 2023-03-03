## Overview

In COS, you can enable metadata acceleration to gain the HDFS protocol access capability. After metadata acceleration is enabled, COS generates a mount point for your bucket. Then you can download the [HDFS client](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) and use the mount point in the client to mount COS. This document introduces how to mount a bucket with metadata acceleration enabled to a computing cluster.

>! 
>- Hadoop-COS supports access to metadata acceleration buckets in the format of `cosn://bucketname-appid/` starting from v8.1.5.
> - The metadata acceleration feature can only be enabled during bucket creation and cannot be disabled once enabled. Therefore, **carefully consider** whether to enable it based on your business conditions. You should also note that legacy Hadoop-COS packages cannot access metadata acceleration buckets.
> 

## Prerequisites

- [Java 1.8](https://www.oracle.com/java/technologies/downloads/) is installed on the computing cluster's machine or container to be mounted.
- The computing cluster's machine or container to be mounted is authorized with the access permission. You need to specify the VPC and IP that can be accessed in the HDFS permission configuration.
- Descriptions of JAR dependency packages:
 1. [chdfs_hadoop_plugin_network-2.8.jar](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) v2.7 or later.
 2. [cos_api-bundle.jar](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar) v5.6.69 or later.
 3. [Hadoop-COS](https://github.com/tencentyun/hadoop-cos/releases) v8.1.5 or later.
 4. ofs-java-sdk.jar v1.0.4 or later, which can be automatically pulled without installation required. You can run `hadoop fs ls` to check whether the versions meet the requirements in the directory configured by `fs.cosn.trsf.fs.ofs.tmp.cache.dir`.

## Directions
1. Download the Hadoop client tool installation package from [GitHub](https://github.com/tencentyun/hadoop-cos/releases).
2. Download the POSIX Hadoop client tool installation package from [GitHub](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar).
3. Download the [COS JAVA SDK installation package](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar).
4. Put the installation package in the `classpath` of each node and make sure that the job can be started and loaded normally, such as `$HADOOP_HOME/share/hadoop/common/lib/`.
>! The EMR environment comes with JAR dependency packages, which don't need to be installed manually. You can directly access metadata acceleration buckets through POSIX semantics. If you need to use the S3 protocol for access, change the `fs.cosn.posix_bucket.fs.impl` configuration item as detailed below.
>
5. Edit the `core-site.xml` file by adding the following basic configuration items:
>!
>- We recommend you use a sub-account key or temporary key instead of a permanent key to improve the business security. When authorizing a sub-account, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid unexpected data leakage.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission, including allowed operations, scope of resources, and conditions such as access IP, on the permanent key so as to improve the usage security.

```
<!-- API key information of the account, which can be viewed in the [CAM console](https://console.cloud.tencent.com/capi). -->
<!-- We recommend you use a sub-account key or temporary key for configuration to improve the configuration security. When authorizing a sub-account, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972). -->
<property>
		 <name>fs.cosn.userinfo.secretId/secretKey</name>
		 <value>AKIDxxxxxxxxxxxxxxxxxxxxx</value>
</property>

<!--COSN implementation class-->
<property>
		 <name>fs.AbstractFileSystem.cosn.impl</name>
		 <value>org.apache.hadoop.fs.CosN</value>
</property>

<!--COSN implementation class-->
<property>
		 <name>fs.cosn.impl</name>
		 <value>org.apache.hadoop.fs.CosFileSystem</value>
</property>

<!-- Bucket region in the format of `ap-guangzhou` -->      
<property>
		 <name>fs.cosn.bucket.region</name>
		 <value>ap-guangzhou</value>
</property>

<!-- Local temporary directory, which is used to store temporary files generated during execution. ->      
<property>
		 <name>fs.cosn.tmp.dir</name>
		 <value>/tmp/hadoop_cos</value>
</property>
```
6. Sync `core-site.xml` to all Hadoop nodes.
>?For an EMR cluster, you only need to modify the HDFS configuration in component management in the EMR console for the above steps 3 and 4.
>
7. Run the `hadoop fs -ls cosn://${bucketname-appid}/` command on the `hadoop fs` command line, where `bucketname-appid` is the mount address, i.e., the bucket name. If the file list is displayed normally, the COS bucket has been successfully mounted.
8. You can also use other configuration items of `hadoop` or use an `mr` job to run data processing jobs in COS metadata acceleration buckets. For an `mr` job, you can run `-Dfs.defaultFS=ofs://${bucketname-appid}/` to change the default input/output file system of this job to the specified bucket.

## Configuration Items

>? You can access metadata acceleration buckets through POSIX semantics or S3 protocol. We recommend you use POSIX for better performance.
>

### 1. Required common configuration items

>! No matter how you access a metadata acceleration bucket, you must set the following common configuration items.
>

| Configuration Item | Content | Description |
| ----------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| fs.cosn.userinfo.secretId/secretKey | A value in the format of `AKIDxxxxxxxxxxxxxxxxxxxx` | Enter the API key information of your account, which can be viewed in the [CAM console](https://console.cloud.tencent.com/capi). |
| fs.cosn.impl                        | org.apache.hadoop.fs.CosFileSystem | COSN implementation class for `FileSystem`, which is fixed at `org.apache.hadoop.fs.CosFileSystem`. |
| fs.AbstractFileSystem.cosn.impl     | org.apache.hadoop.fs.CosN          | COSN implementation class for `AbstractFileSystem`, which is fixed at `org.apache.hadoop.fs.CosN`. |
| fs.cosn.bucket.region               | A value in the format of `ap-beijing` | Enter the region information of the bucket to be accessed, such as `ap-beijing` and `ap-guangzhou`. For enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). This parameter is compatible with the legacy parameter `fs.cosn.userinfo.region`. |
| fs.cosn.tmp.dir                     | `/tmp/hadoop_cos` by default                | Set an existing local directory, where temporary files generated during execution will be placed. Meanwhile, be sure to configure sufficient space and permissions for this directory on each node. |



### 2. Required configuration items for POSIX access mode (recommended)

>?
>- In POSIX access mode, in addition to the common configuration items, you also need to add the following items. You can add the `fs.cosn.trsf.` prefix to other optional items as described in [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965) to access metadata acceleration buckets.
>- Note that the configuration items related to legacy Hadoop-COS are no longer applicable.

| Configuration Item | Content | Description |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl | com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter                      |      Implementation class for metadata acceleration bucket access |
| fs.cosn.trsf.fs.ofs.impl                    | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter                |     Implementation class for metadata acceleration bucket access |
| fs.cosn.trsf.fs.ofs.tmp.cache.dir           | A value in the format of `/data/emr/hdfs/tmp/posix-cosn/` | Set an existing local directory such as `"/data/emr/hdfs/tmp/posix-cosn/"`, where temporary files generated during execution will be placed. Meanwhile, be sure to configure sufficient space and permissions for this directory on each node. |
| fs.cosn.trsf.fs.ofs.user.appid              | A value in the format of `12500000000`  | Your `appid`, which is required. |
| fs.cosn.trsf.fs.ofs.bucket.region           | A value in the format of `ap-beijing`  | Your bucket region, which is required. |


### 3. Required configuration items for S3 access mode

The following configuration items are required for the S3 access mode. For other optional parameters, see [Hadoop](https://intl.cloud.tencent.com/document/product/436/6884).

| Configuration Item | Content | Description |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.posix_bucket.fs.impl         | org.apache.hadoop.fs.CosNFileSystem |      This parameter is fixed at `com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter` for the POSIX access mode (default mode) or `org.apache.hadoop.fs.CosNFileSystem` for the S3 access mode, respectively.                                        |


### 5. Notes
1. You cannot use a legacy Hadoop-COS JAR package to access metadata acceleration buckets.
2. To access metadata acceleration buckets in POSIX mode of Hadoop-COS 8.1.5 or earlier, you need to disable ranger verification in the console.

