Alluxio users often have existing applications accessing their existing storage systems (Under-FileSystem). Alluxio can be added to existing ecosystems, but one thing that must always be changed is the URI used by the application. The Transparent-URI feature allows users to access their existing storage systems without changing URIs at the application level.

## Supported Versions and URI Configuration
1. Supported service component versions: Alluxio v2.5.0 and above.
2. Supported product versions: Hadoop 2.x standard EMR v2.5.1 and above; Hadoop 3.x standard EMR v3.2.0 and above.
3. In order to use Alluxio Transparent-URI, a new Hadoop compatible file system client implementation should be configured. This new ShimFileSystem will replace existing FileSystem whenever the client is configured for receiving foreign URIs. The APIs of Hadoop FileSystem (a Hadoop compatible compute framework) define the mapping from FileSystem scheme to FileSystem implementation. To configure ShimFileSystem, make sure that the following items are configured in the `core-site` file:

| Configuration Item | Value |
| ------------------------------- | ----------------------------------------- |
| fs.cosn.impl | com.qcloud.emr.CosNShimFileSystem |
| fs.AbstractFileSystem.cosn.impl | com.qcloud.emr.CosNShimAbstractFileSystem |
| fs.cosn.userinfo.appid | $appId |

>?
>- Once ShimFileSystem is configured, master will need to route URIs that are native to external storage system, to Alluxio namespace. This requires COSN to have been mounted to Alluxio namespace.
>- You can use the EMR configuration delivery feature in EMR-Alluxio to disable Transparent-URI.

## Mounting
The `mount` command is one of Alluxio's most distinctive commands. It is similar to Linux's `mount` command, through which users can load disks, SSDs and other storage devices to the local file system of Linux. In Alluxio, the concept of mounting is further extended to the distributed system level, that is, users can mount one or more other storage systems/cloud storage services (such as HDFS and COS) to the Alluxio distributed file system using the `mount` command. So they can run distributed applications on Alluxio, such as Spark, Presto, and MapReduce, without any adaptation or even knowledge of the specific data access protocol and path. Users only need to know the path corresponding to the data in the Alluxio file system. It greatly facilitates application development and maintenance.
![](https://main.qcloudimg.com/raw/b5d3e96ce6c17866480a36e231c52517.png)

#### EMR-Alluxio uses HDFS as the root mount point by default.
Beginning from EMR-Alluxio v2.5.1, Alluxio's UFS supports the COSN protocol. COS UFS has relatively poor read/write performance and is unstable. In order to solve this issue, the community provides the underlying COSN UFS. Both COS UFS and COSN UFS are used to access Tencent Cloud COS. COSN UFS is a great improvement compared with COS UFS. Its read/write performance are twice as good as that of COS UFS, and it has better stability. Therefore, COSN UFS is strongly recommended. The maintenance for COS UFS will stop after EMR-Alluxio v2.6.0.

Example of mounting COSN UFS:
```
  alluxio fs mount --option fs.cosn.userinfo.secretId=xx \ 
        --option fs.cosn.userinfo.secretKey=xx \ 
        --option fs.cosn.bucket.region=ap-xx \ 
        --option fs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \ 
        --option fs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \ 
        --option fs.cosn.userinfo.appid=xx \ 
        /cosn cosn://COS_BUCKET/path
```
Configure the COS information in each `--option`.

| Configuration Item  | Description |
| -------------------------------- | ----------------------------------------- |
| fs.cosn.userinfo.secretId | COS secret ID |
| fs.cosn.userinfo.secretKey | COS secret key |
| fs.cosn.impl | Its value is always `org.apache.hadoop.fs.CosFileSystem`. |
| fs.AbstractFileSystem.cosn.impl  | Its value is always `org.apache.hadoop.fs.CosN`. |
| fs.cosn.bucket.region cos region | Region name such as `ap-beijing` |
| fs.cosn.userinfo.appid  | Root account's AppID |
| COS_BUCKET COS BUCKET | Bucket name without the AppID suffix |

 
