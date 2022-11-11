## Metadata Acceleration Overview

COS offers the metadata acceleration feature to provide high-performance file system capabilities. Metadata acceleration leverages the powerful metadata management feature of Cloud HDFS (CHDFS) at the underlying layer to allow using file system semantics for COS access. The designed system metrics can reach a bandwidth of up to 2.4 GB/s, over 100,000 queries per second (QPS), and a latency of milliseconds. Buckets with metadata acceleration enabled can be widely used in scenarios such as big data, high-performance computing, machine learning, and AI. For more information on metadata acceleration, see [Metadata Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/43305).

## Benefits of HDFS Access

In the past, big data access based on COS was mainly implemented through the Hadoop-COS tool. The tool internally adapts Hadoop Compatible File System (HCFS) APIs to COS RESTful APIs to access data in COS. The difference in metadata organization between COS and file systems leads to varying metadata operation performance, which affects the big data analysis performance. Buckets with metadata acceleration enabled are fully compatible with the HCFS protocol and can be accessed directly by using native HDFS APIs. This saves the overheads of converting the HDFS protocol to COS protocol and provides native HDFS features such as efficient directory rename (as an atomic operation), file atime, and mtime update, efficient directory DU statistics, and POSIX ACL permission support.

<span id="1"></span>
## Creating Bucket and Configuring the HDFS Protocol

1. Create a COS bucket and enable metadata acceleration for it.

After the bucket is created, go to the **File List** page of the bucket, where you can upload and download files.
2. On the left sidebar, click **Performance Configuration** > **Metadata Acceleration**, and you can see that metadata acceleration is enabled.
When you create a bucket that **requires metadata acceleration to be enabled**, you need to perform the corresponding **authorization** operation as prompted. After you click **Authorize**, the HDFS protocol will be automatically enabled, and you can see the default bucket mount target information.
>?If the system prompts that the corresponding HDFS file system is not found, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
3. In the **HDFS Permission Configuration** column, click **Add Permission Configuration**.

4. Select the VPC where the computing cluster resides in the **VPC Name** column, enter the IP address or range that needs to be opened in the **Node IP** column, select **Can edit** or **Can view** as the access type, and click **Save**.
>? The HDFS permission configuration is different from the native COS permission system. If you use HDFS to access a COS bucket, we recommend you configure HDFS permission to authorize servers in a specified VPC to access the COS bucket and enjoy the same permission experience as that of native HDFS.


## Configuring Computing Cluster to Access COS

### EMR environment

The EMR environment has already been seamlessly integrated with COS, and you only need to complete the following steps:
1. Find an EMR server and run the following command on it to check the version of the HDFS client package in the EMR environment. Make sure that the version is 2.7 or later.
```
find / -name "chdfs*"
```
Check whether the version of the `chdfs` package in the search result is 2.7 or later.
2. If the client package needs to be updated, perform the following steps:
 1. Download the script files of the updated JAR package at:
    - [update_cos_jar.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar.sh)
    - [update_cos_jar_common.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar_common.sh)
 2. Run the following command to put the two scripts in the `/root` directory of the server to add the execution permission to `update_cos_jar.sh`:
```
sh update_cos_jar.sh  https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7  
```
Replace the parameter with the bucket in the corresponding region, such as `https://hadoop-jar-guangzhou-1259378398.cos.ap-guangzhou.myqcloud.com/hadoop_plugin_network/2.7` in Guangzhou region.
Perform the above steps on each EMR node until all JAR packages are replaced.
3. Configure `core-site.xml` in the EMR console by adding a new configuration item `fs.ofs.bucket.region`. It specifies the COS region where the bucket resides, such as `ap-shanghai`.
>!The `fs.ofs.bucket.region` parameter is required. It specifies the COS region where the bucket resides, such as `ap-shanghai`.
>
4. Restart resident services such as YARN, Hive, Presto, and Impala.


### Self-built Hadoop/CDH environments
1. Download the [client installation package](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) version 2.7 or later for access over the HDFS protocol.
2. Place the installation package in the `classpath` path of each server in the Hadoop cluster, such as `/usr/local/service/hadoop/share/hadoop/common/lib/` (which may vary by component).
2. Configure `core-site.xml` in the computing cluster as instructed in [Mounting CHDFS](https://intl.cloud.tencent.com/document/product/1106/41965).
3. Restart resident services such as YARN, Hive, Presto, and Impala.

>!The `fs.ofs.bucket.region` parameter is required. It specifies the COS region where the bucket resides, such as `ap-shanghai`.
>

### Verifying environment

After all environment configuration steps are completed, you can verify the environment in the following ways:
- Use the Hadoop command line on the client to check whether mounting is successful.
![](https://qcloudimg.tencent-cloud.cn/raw/90264cdfe35753b95d48db5ab6675629.png)
- Log in to the [COS console](https://console.cloud.tencent.com/cos) to check whether the files and directories in the bucket file list are consistent.


## Ranger Permission Configuration

By default, the native POSIX ACL mode is adopted for authentication for the HDFS protocol. If you need to use Ranger authentication, configure as follows:

### EMR environment

1. The EMR environment has integrated the COS Ranger Service, so you can select it when purchasing an EMR cluster.
2. In the HDFS authentication mode of the HDFS protocol, select the Ranger authentication mode and configure the corresponding address information of Ranger.
 - For CHDFS, add the new configuration item `fs.ofs.ranger.enable.flag` in `core-site.xml` and set it to `true`.
 - For COSN, add the new configuration item `fs.cosn.credentials.provider` and set it to `org.apache.hadoop.fs.auth.RangerCredentialsProvider`.
 - If you have any questions about Ranger, see [FAQs](https://intl.cloud.tencent.com/document/product/1106/41958).

### Self-built Hadoop/CDH environments

1. Configure the Ranger service to access COS over the HDFS protocol. For more information, see [CHDFS Ranger Permission System Solution](https://intl.cloud.tencent.com/document/product/1106/41973).
2. In the HDFS authentication mode of the HDFS protocol, select the Ranger authentication mode and configure the corresponding address information of Ranger.
 - For CHDFS, add the new configuration item `fs.ofs.ranger.enable.flag` in `core-site.xml` and set it to `true`.
 - For COSN, add the new configuration item `fs.cosn.credentials.provider` and set it to `org.apache.hadoop.fs.auth.RangerCredentialsProvider`.
 - If you have any questions about Ranger, see [FAQs](https://intl.cloud.tencent.com/document/product/1106/41958).

## Others

In a big data scenario, you can access a bucket with metadata acceleration enabled over the HDFS protocol in the following steps:

1. Configure the HDFS mount target information in `core-stie.xml` as instructed in [Creating Bucket and Configuring HDFS Protocol](#1).
2. Access the bucket with components such as Hive, MR, and Spark. For more information, see [Mounting COS Bucket in Computing Cluster](https://intl.cloud.tencent.com/document/product/436/46199).
3. By default, the native POSIX ACL mode is adopted for authentication. If you need to use Ranger authentication, see [CHDFS Ranger Permission System Solution](https://intl.cloud.tencent.com/document/product/1106/41973).



