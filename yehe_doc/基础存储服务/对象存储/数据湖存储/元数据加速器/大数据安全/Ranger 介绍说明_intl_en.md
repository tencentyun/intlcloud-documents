## Background

COS Ranger Service is a big data permission control solution based on Tencent Cloud storage-computing separation. It features fine granularity, compatibility with Hadoop Ranger, and a pluggable architecture and helps you centrally manage big data components and manage the storage permissions in the cloud. For more information on the service and its architecture scheme, see [COS Ranger Permission System Solution](https://intl.cloud.tencent.com/document/product/436/39144).

COS Ranger Service has been widely used since its launch. However, as customers have diverse businesses and a complex background, some questions have arisen. To answer them, this document describes the service as well as its version details and precautions.

## Version Description

### Components

Its components include Ranger-Plugin, COS Ranger Server, COS Ranger Client (i.e., Hadoop-Ranger-Client), and COSN Ranger Interface.

#### Ranger-Plugin

It provides a service definition plugin on the Ranger server based on the Ranger protocol (for more information, see [Ranger Stacks - How to add a custom plugin?](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=53741207)) and description of the COS service on the Ranger side. After this plugin is deployed, you can enter the COS permission policies such as path, bucket, user, and group access policies on the Ranger control page.  

#### COS Ranger Server

It integrates the Ranger client, periodically syncs permission policies from the Ranger server, and verifies the permission locally after receiving an authentication request. In addition, it also provides `DelegationToken` generation and renewal APIs in Hadoop.

In the EMR environment, it is installed in `/usr/local/service/cosranger/lib` by default. For example, in the package name `cos-ranger-service-5.1.2-jar-with-dependencies.jar`, `5.1.2` is the version number of COS Ranger Server.

#### COS Ranger Client

The Hadoop SDK plugin loads COS Ranger Client dynamically according to the configuration in the `core-site.xml` file and forwards the permission verification requests to COS Ranger Server.  

In the EMR environment, it is installed in `/usr/local/service/hadoop/share/hadoop/common/lib` by default. For example, in the package name `hadoop-ranger-client-for-hadoop-2.8.5-5.0.jar`, `2.8.5` is the Hadoop version number, and `5.0` is the package version number.

#### COSN Ranger Interface

This plugin is defined by the common data and APIs of COS Ranger Server and COS Ranger Client.

In the EMR environment, it is installed in `/usr/local/service/hadoop/share/hadoop/common/lib`. For example, in the package name `cosn-ranger-interface-1.0.4.jar`, `1.0.4` is the version number of COSN Ranger Interface.

You can get the above JAR packages from [GitHub](https://github.com/tencentyun/cos-ranger-service). For other components such as COS Ranger Client packages for Impala and Presto, contact the EMR team.  

The above components will be installed automatically when you purchase the Ranger and COS Ranger components in the EMR console. You can also install them by yourself as instructed in [CHDFS Ranger Permission System Solution](https://intl.cloud.tencent.com/document/product/1106/41973).

### Release notes 

Versions can be divided into two types by core architecture: **ZooKeeper-dependent service registration and discovery** and **ZooKeeper-independent service registration and discovery**. COS Ranger Server provides the service for COS Ranger Client to call.  
- If COS Ranger Client discovers the service address of COS Ranger Server through ZooKeeper, you need to configure the ZooKeeper address, which is a feature specific to a **ZooKeeper-dependent version**.
- If COS Ranger Client doesn't depend on ZooKeeper to discover the COS Ranger Server service, you only need to configure `qcloud.object.storage.ranger.service.address` to directly specify the service address of COS Ranger Server, which is a feature specific to a **ZooKeeper-independent version**.

### Version mappings

| Component | ZooKeeper-Dependent Service Registration and Discovery | ZooKeeper-Independent Service Registration and Discovery |
| ---- | --- | ---- |
| COS Ranger Server | v5.0.9 or earlier | v5.1.1 or later |
| COS Ranger Client |  v3.9 or earlier | v4.1 or later |
| COSN Ranger Interface | v1.0.3 | v1.0.4 or later |

>! If you use a version that **doesn't depend on ZooKeeper for service registration and discovery**, COS Ranger Server must be on v5.1.1 or later (**v5.1.2** is recommended), COS Ranger Client must be on v4.1 or later (**v5.0** is recommended), and COSN Ranger Interface must be on v1.0.4 or later.
>

### Version compatibility

Versions can be mapped based on the above two types. However, as versions may not be divided into the two types due to diverse customers with a complex background, the compatibility relationships between components are as listed below. Components on the same row are compatible with each other.

| COS Ranger Client Version   | COS Ranger Server Version  | COSN Ranger Interface Version | Dependency on ZooKeeper for Service Registration and Discovery  |
|  -----------------------|  ----------------------  | ------------------------ | ------|
|   v3.9 or earlier       |    v5.0.9 or earlier     |       v1.0.3             |  Yes |
|   v3.9 or earlier       |    v5.1.1 or later     |       v1.0.4             |  Yes |
|   v4.1 or later       |    v5.1.1 or later     |       v1.0.4             |  No |
|   v5.0 or later       |    v5.0.9 or earlier     |       v1.0.4             |  Yes |
|   v5.0 or later       |    v5.1.1 or later     |       v1.0.4             |  No |


>!
> - COS Ranger Client 5.0 is compatible with all versions of COS Ranger Server.
> - COS Ranger Client 4.1 is compatible with only COS Ranger Server 5.1.1 or later.
> - Though COS Ranger Client 3.x is compatible with all versions of COS Ranger Server, it can only depend on ZooKeeper to discover the COS Ranger Server service (the shortcomings of ZooKeeper-dependent versions are as detailed below).
> - The COS Ranger Client and COSN Ranger Interface packages must be placed in the same directory for the Hadoop SDK plugin to load dynamically.
> 

### Notes

- Ranger verification needs to be enabled for the metadata acceleration bucket or CHDFS file system in the console.
- If you use a version that **depends on ZooKeeper for service registration and discovery**, you need to set `qcloud.object.storage.zk.address` to the ZooKeeper address (separate multiple addresses by comma) in `core-site.xml`.
- If you use COS Ranger Server 5.1.1 or 5.1.2 but COS Ranger Client 3.x, you still need to depend on ZooKeeper for service registration and discovery, so you need to set `qcloud.object.storage.zk.address` to the ZooKeeper address (separate multiple addresses by comma such as `10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181`) in `core-site.xml`.
- If you use a version that **doesn't depend on ZooKeeper for service registration and discovery**, you need to set `qcloud.object.storage.ranger.service.address` to the service address of COS Ranger Server (separate multiple addresses by comma such as `127.0.0.1:9999,128.0.0.1:9999`) in `core-site.xml`.
- To use the OFS protocol for access, you need to set `fs.ofs.ranger.enable.flag` to `true` in `core-site.xml`.
- To use the COSN protocol for access, you need to set `fs.cosn.credentials.provider` to `org.apache.hadoop.fs.auth.RangerCredentialsProvider` in `core-site.xml`.

### COSN configuration

| Configuration Item  | Description | Example |
| --- | --- | --- |
| qcloud.object.storage.zk.address | ZooKeeper address for COS Ranger Server registration | 10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181  |
| qcloud.object.storage.ranger.service.address | COS Ranger Server RPC service address | 127.0.0.1:9999,128.0.0.1:9999 |
| fs.ofs.ranger.enable.flag | Ranger toggle when the OFS protocol is used | true |
| fs.cosn.credentials.provider | Ranger authentication class path when the COSN protocol is used | org.apache.hadoop.fs.auth.RangerCredentialsProvider |
| fs.cosn.posix.bucket.use_ofs_ranger.enabled | Whether to use CHDFS Ranger authentication | The default value is `false`, which indicates COSN Ranger authentication.<br>If it is set to `true`, CHDFS Ranger authentication is used.<br>Note: This configuration item is added to Hadoop-COS 8.1.7 or later.  |


### Configuration items

| Component Version | Configuration Item |
| --- | --- |
| COS Ranger Server 5.0.9 or earlier<br>COS Ranger Client 3.9 or earlier or 5.0<br>Access over the OFS protocol | qcloud.object.storage.zk.address<br> fs.ofs.ranger.enable.flag |
| COS Ranger Server 5.0.9 or earlier<br>COS Ranger Client 3.9 or earlier or 5.0<br>Access over the COSN protocol | qcloud.object.storage.zk.address<br> fs.cosn.credentials.provider |
| COS Ranger Server 5.1.1 or 5.1.2<br>COS Ranger Client 4.1 or later<br>Access over the OFS protocol | qcloud.object.storage.ranger.service.address<br> fs.ofs.ranger.enable.flag |
| COS Ranger Server 5.1.1 or 5.1.2<br>COS Ranger Client 4.1 or later<br>Access over the COSN protocol | qcloud.object.storage.ranger.service.address<br> fs.cosn.credentials.provider|

>!
> - To access the metadata acceleration bucket over the COSN protocol and use CHDFS Ranger for authentication, set `fs.cosn.posix.bucket.use_ofs_ranger.enabled` to `true` and make sure that Hadoop-COS is on v8.1.7 or later.
> - If you add or modify the above configuration items, you need to restart big data components such as ResourceManager/NodeManager in YARN, HiveMetaStore/HiveServer2 in Hive, and applications in Impala and Presto.
> 

### Recommended versions

| Component | Version Number |
| ---| ---|
| cos-ranger-server| >= v5.1.2 |
| cos-ranger-client| >= v5.0   |
| cosn-ranger-interface| >= v1.0.4|


### Recommendation description

The above versions are recommended for the following reasons:

- ZooKeeper is used only for master election but not for service registration and discovery, which greatly alleviates the pressure on ZooKeeper during big data jobs. As during each big data job, a large number of tasks access ZooKeeper to discover the COS Ranger Server service, bringing a huge pressure on ZooKeeper and affecting the stability of other big data components.
- The `hadoop-ranger-client` package on v5.0 is compatible with early versions of COS Ranger Server packages, which makes it easier for old users to upgrade COS Ranger Server.
- On COS Ranger Server versions earlier than 5.1.2, the obtained leader IP may be different from the IP in the leader latch. Moreover, the information that COS Ranger Server registers with ZooKeeper will be simplified to facilitate subsequent extension or upgrade.
- Several bugs are fixed.


## Authentication FAQs

### What should I do if the error `IOException: init fs.ofs.ranger.client.impl failed` is reported?

- If `Caused by: java.io.IOException: invalid zk address null` is displayed, you need to set `qcloud.object.storage.zk.address` to the ZooKeeper address (separate multiple addresses by comma such as `10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181`) in `core-site.xml`.
- If `Caused by: java.io.IOException: ranger client is null, maybe ranger server for qcloud object storage is not deployed!` is displayed, refer to the next question.

### What should I do if the error `ranger client is null, maybe ranger server for qcloud object storage is not deployed!` is reported?

Below are the error causes:
- If the `hadoop-ranger-client` package is on v3.8 or earlier, the ZooKeeper watch may be lost. In this case, we recommend you upgrade the package to v5.0.
- Check the configuration item `qcloud.object.storage.zk.address` or `qcloud.object.storage.ranger.service.address`.
- Check whether the COS Ranger Server service and process are normal.

### What should I do if the error `Expect ranger service addresses: [127.0.0.1:6080,128.0.0.1:6080], but actual ranger service address` is reported?

![](https://qcloudimg.tencent-cloud.cn/raw/5cc5ce4451bbe5bfe91835befd1a49db.png)

- This error occurs because Ranger verification is enabled for the metadata acceleration bucket or CHDFS in the console but not on the client.
- To use the OFS protocol for access, you need to set `fs.ofs.ranger.enable.flag` to `true` in `core-site.xml`.
- To use the COSN protocol for access, you need to set `fs.cosn.credentials.provider` to `org.apache.hadoop.fs.auth.RangerCredentialsProvider` in `core-site.xml`.

### What should I do if the `RangerQcloudObjectStorageClient` class is not found?

![](https://qcloudimg.tencent-cloud.cn/raw/6558d81d1269320c53379c44c7f254ca.png)

- The `cosn-ranger-interface` package is missing. You can get it in the `cosn-ranger-interface` directory on [GitHub](https://github.com/tencentyun/cos-ranger-service).
- Other relevant classes are not found. You can check whether the `cosn-ranger-interface` and `hadoop-ranger-client` packages exist, their versions are matched, and they are placed in the correct path.
- If other relevant classes are not found, it may be caused by the package shade path. In this case, contact us for assistance.

### What should I do if the error `NoSuchMethodError` is reported?

![](https://qcloudimg.tencent-cloud.cn/raw/4b3fdbf027180095ca32292d54a05279.jpg)

This error occurs because the method originally exists but is missing in the loaded class, which may be caused by the following:

- The method is added to the package after version iteration but doesn't exist in earlier versions.
- The class with the same name in another package is loaded.

Run the following command in `/usr/local/service`:
```
find . -name "*.jar" -exec grep -Hls "org/apache/hadoop/fs/cosn/ranger/client/RangerQcloudObjectStorageClientImpl" {} \;
```
Find and delete the relevant package. For another class, simply modify the class path in the above command.

### What should I do if the error `java.lang.ClassCastException org.apache.hadoop.fs.cosn.ranger.protocol.ClientQCloudObjectStorageProtocolProtos$GetSTSRequest cannot be cast to com.google.protobuf.Message` is reported?

Errors similar to this are generally caused by package contamination. The package on an earlier version exists on the server, and the Protobuf protocol is inconsistent, which is generally the same as the Alluxio package contamination below.  

Run the following command in `/usr/local/service`:
```
find . -name "*.jar" -exec grep -Hls "org/apache/hadoop/fs/cosn/ranger/protocol/ClientQCloudObjectStorageProtocolProtos" {} \;
```
Find and delete the relevant package. For another class, simply modify the class path in the above command.

### What should I do if the modified Ranger policy doesn't take effect?

- For a CHDFS policy, decrease the value of `ranger.plugin.chdfs.policy.pollIntervalMs` in milliseconds in the COS Ranger Server configuration file `ranger-chdfs-security.xml`.
- For a COSN policy, decrease the value of `ranger.plugin.cos.policy.pollIntervalMs` in milliseconds in the COS Ranger Server configuration file `ranger-cos-security.xml`.

### What should I do if the group configured for a Ranger policy doesn't take effect?

If the configured user takes effect, you need to contact the EMR team to check group sync. In other cases, contact us for assistance.

### How do I configure a storage path policy rule in a Ranger policy?

Ranger has a simple path verification rule, which is mainly based on string match. If the path rule of the policy is set to `**/a/**` for the file `/a/b/c`, the file cannot be accessed through **/a** or **/a/**, as the SDK will remove **/** at the end and the path will become **/a** in Ranger and cannot match **/a/**. If you access **/a/b** or **/a/b/c**, the prefix of the two paths can match the path rule **/a/** in the policy.

### What should I do if the error `HiveAccessControlException` is reported when I specify the COSN or OFS path in Hive for table creation?

![](https://qcloudimg.tencent-cloud.cn/raw/928c7f08b597170da831dcca0e7edc42.png)

You need to disable URL verification in Hive by configuring the permission to allow URLs in Hive in the Ranger console:

![Ranger Admin](https://qcloudimg.tencent-cloud.cn/raw/8db0474e6ec152f92b61c98f6ac5d83c.png)

>! Note the error log format, which is highly likely to be reported by the Ranger service, and the error occurs because the permission configured by the Ranger admin is incorrect in most cases.

### What should I do if the error `HiveAccessControlException` is reported when I submit a Spark job in an environment that uses Kerberos for authentication?

If the application needs to interact with other secure Hadoop file systems, their URIs need to be explicitly provided to Spark during startup. You can configure the parameter `spark.kerberos.access.hadoopFileSystems=cosn://bucket-appid,ofs://f4mxxxxxxxx-Xxxx.chdfs.ap-guangzhou.myqcloud.com` as instructed in [Spark Security](https://spark.apache.org/docs/latest/security.html).

### What should I do if a table isn't moved to the recycle bin after being dropped in Spark?

If the location is specified when you run CREATE TABLE in Spark, an external table will be created, and its data won't be deleted after it is dropped. For more information, see [Upgrading from Spark SQL 1.6 to 2.0](https://spark.apache.org/docs/latest/sql-migration-guide.html#upgrading-from-spark-sql-16-to-20).

>? The data can be deleted if you run DROP TABLE in Hive on MR.
>

### What should I do if the error `AccessControlException` is reported when Hive executes INSERT statements?

The default engine of Hive is MapReduce. Add the following configuration item to the `yarn-site.xml` file:
```
<property>
    <name>mapreduce.job.hdfs-servers</name>
    <value>
        ofs://f4mxxxxxxx-XXXX,cosn://bucketname-appid,${fs.defaultFS}
    </value>
</property>
```
If the Hive engine is Tez, add the `tez.job.fs-servers` configuration item to the `tez-site.xml` file and set it to the above value.

If you use Beeline to connect to Hive, restart HiveServer2 and load the new `yarn-site` configuration.

### What should I do if an error occurs when I access OFS?

![](https://qcloudimg.tencent-cloud.cn/raw/006df64050758fb2e4551d68335b94dd.png)

The error is returned by the OFS backend. After Ranger is enabled, you need to disable POSIX in the following places:

- CHDFS console

- COS bucket configuration


### What should I do if the error `renew token failed` is reported when I submit a job through the YARN command?

The `-Dmapreduce.job.send-token-conf ` parameter is required to execute the YARN command.

### How do I build COS Ranger?

For more information, see [COS Ranger Permission System Solution](https://intl.cloud.tencent.com/document/product/436/39144) and [CHDFS Ranger Permission System Solution](https://intl.cloud.tencent.com/document/product/1106/41973).

### How do I enable Ranger in EMR?

You can purchase the Ranger and COS Ranger components in the EMR console to eliminate the need of deployment on your own.  
- For CHDFS, add the new configuration item `fs.ofs.ranger.enable.flag` to `core-site.xml` and set it to `true`.
- For COSN, add the new configuration item `fs.cosn.credentials.provider` to `core-site.xml` and set it to:
org.apache.hadoop.fs.auth.RangerCredentialsProvider.

### What should I do if a NodeCache null pointer exception occurs?

Check the `hadoop-ranger-client` version. If it is v3.8, we recommend you upgrade it to v5.0; otherwise, contact us for assistance.
This error occurs because the big data job has a high concurrency, the pressure on ZooKeeper is high, and the ZooKeeper watch is lost.

### What should I do if the error `java.lang.IllegalArgumentException: Failed to specify server's Kerberos principal name` is reported when I run a Hadoop FS command after COS Ranger is enabled?

- Add the following configuration item to `core-site.xml`: `qcloud.object.storage.kerberos.principal`.
- If the error is reported by the HDFS cluster, add the following configuration item to `core-site.xml`: `dfs.namenode.kerberos.principal`.
