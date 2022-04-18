
## Metadata Acceleration Overview

COS launched the metadata acceleration feature to provide high-performance file system features. Metadata acceleration leverages of the powerful metadata management feature of Cloud HDFS (CHDFS) at the underlying layer to allow users to use file system semantics to access COS. The system design metrics can reach a bandwidth of up to 2.4 GB/s, over 100,000 queries per second (QPS), and a latency of milliseconds. Buckets with metadata acceleration enabled can be widely used in scenarios such as big data, high-performance computing, machine learning, and artificial intelligence. For more information about metadata acceleration, see [Metadata Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/43305).

## Benefits of HDFS Access

In the past, big data access based on COS is mainly implemented based on the Hadoop-COS tool. The Hadoop-COS tool internally adapts HCFS APIs to COS RESTful APIs to access data on COS. The difference in metadata organization between COS and file systems leads to the difference in metadata operation performance, which affects big data analysis performance. Buckets with metadata acceleration enabled are fully compatible with the HCFS protocol and can be accessed directly by using native HDFS APIs, saving the overhead of converting the HDFS protocol to COS protocol, and providing native HDFS features such as efficient directory rename (as an atomic operation), file atime and mtime update, efficient directory DU statistics, and POSIX ACL permission support.


## Preparations

1. Create a COS bucket and enable metadata acceleration for it.

2. After the bucket is created, go to the **File List** page of the bucket. You can upload or download files in the console.

3. Choose **Performance Configuration** > **Metadata Acceleration** in the left sidebar, and you can see that metadata acceleration is enabled. If this is the first time you create a bucket that **requires metadata acceleration**, perform the corresponding authorization operations as instructed. After you click **Authorize**, HDFS access is enabled by default, and you can view the information of the default bucket mount point.

>?If the system indicates that the corresponding HDFS file system is not found, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
4. After HDFS access is enabled, you need to configure VPC access permission. On the HDFS permission configuration tab page, click the button for adding permission configuration. In the VPC name column, select the address of the VPC where the computing cluster resides. In the node IP column, enter the IP or IP range to be opened in the VPC IP range. Set the access type to read/write or read-only. Then click **Save**.

>? The HDFS permission configuration is different from the native COS permission system. If you use HDFS to access a COS bucket, you are advised to configure HDFS permission to authorize machines in a specified VPC to access the COS bucket to achieve the same permission experience as that of the native HDFS.
5. By default, the HDFS protocol uses the native POSIX ACL mode for authentication. If you want to use Ranger authentication, you can select the Ranger authentication mode under HDFS authentication mode and configure Ranger addresses.

>?For how to configure the Ranger service and use the Ranger service to access COS via HDFS, see [here](https://intl.cloud.tencent.com/document/product/1106/41973).
>
6. After creating the environment, you need to configure `core-site.xml` for the computing cluster. For more information, see [here](https://intl.cloud.tencent.com/document/product/1106/41965). If you are using Tencent Cloud EMR, you can use the default EMR configuration directly without extra configuration.
>!The `fs.ofs.bucket.region` parameter is required. It specifies the COS region where the bucket resides, for example, `ap-shanghai`.
>
7. Download the [client installation package](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) for HDFS access. Ensure that the installation package is of version 2.7 or later. Place the downloaded installation package to the correct `classpath` path (example path: `/usr/local/service/hadoop/share/hadoop/common/lib/`; the path varies depending on component) on each server in the Hadoop cluster. Then restart resident services such as Yarn, Hive, Presto, and Impala.
8. After environment configuration is completed, you can check whether the HDFS file system is mounted successfully in the Hadoop command-line interface (CLI).
![](https://qcloudimg.tencent-cloud.cn/raw/90264cdfe35753b95d48db5ab6675629.png)
9. You can log in to the [COS console](https://console.cloud.tencent.com/cos) to check whether the files are directories on the bucket file list are consistent.

## Accessing COS via HDFS

In a big data scenario, you can perform the following steps to access a bucket with metadata acceleration enabled using HDFS:

1. In `core-stie.xml`, configure HDFS related mount point information as shown in the Preparations part.
2. Access the bucket using components such as Hive, MR, and Spark. For more information, see [Mounting a COS Bucket in a Computing Cluster](https://intl.cloud.tencent.com/document/product/436/46199).
3. By default, the native POSIX ACL mode is adopted for authentication. If you need to use Ranger authentication, see [Ranger principles and practices](https://cloud.tencent.com/document/product/1105/53307).


