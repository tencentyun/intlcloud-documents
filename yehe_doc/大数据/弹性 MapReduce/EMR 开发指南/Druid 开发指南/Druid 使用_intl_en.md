EMR allows you to deploy an E-MapReduce Druid cluster as an independent cluster based on the following considerations:
- Use case: E-MapReduce Druid can be used without Hadoop to adapt to different business use cases.
- Resource preemption: E-MapReduce Druid has high requirements for the memory, especially with the Broker and Historical nodes. The resource usage of E-MapReduce Druid is not scheduled by Hadoop YARN; therefore, resource preemption tends to occur during operations.
- Cluster size: As an infrastructure, Hadoop generally has a large size, while E-MapReduce Druid is relatively small. When they are deployed in the same cluster, resources may be wasted due to their different sizes. Therefore, separate deployment is more flexible.

## Purchase suggestions
To purchase a Druid cluster, select Druid as the cluster type when creating the EMR cluster. The Druid cluster has built-in Hadoop HDFS and YARN services integrated with Druid, which are recommended for testing only. **We strongly recommend you use a dedicated Hadoop cluster in the production environment.**
To disable the built-in Hadoop services for the Druid cluster, go to the [EMR console](https://console.cloud.tencent.com/emr), select the target service pane on the **Cluster services** page, and click **Operation > Pause service** to suspend the service.


## Configuring connectivity between Hadoop and Druid clusters
This section describes how to configure the connectivity between the Hadoop and Druid clusters. If you use the built-in Hadoop cluster in the Druid cluster (which is not recommended for the production environment), they can be properly connected with no additional settings required, and you can skip this section.

If you want to store the index data in the HDFS of another independent Hadoop cluster (which is recommended for the production environment), you need to configure the connectivity between the two clusters in the following steps:
1. Make sure that the Druid and Hadoop clusters can properly communicate with each other.
The two clusters should be in the same VPC. If they are in different VPCs, the two VPCs should be able to communicate with each other (through CCN or Peering Connection, for example).
2. Copy the `core-site.xml`, `hdfs-site.xml`, `yarn-site.xml`, and `mapred-site.xml` files in `/usr/local/service/hadoop/etc/hadoop` in the Hadoop cluster and paste them in `/usr/local/service/druid/conf/druid/_common` on each node in the E-MapReduce Druid cluster.
>!As the Druid cluster has a built-in Hadoop cluster, the relevant soft links to the files above already exist in the Druid path. You need to delete them first before copying the configuration files of another Hadoop cluster. In addition, you need to make sure that the file permissions are correct so that the files can be accessed by the `hadoop` user.
3. Modify the `common.runtime.properties` configuration file in Druid configuration management, save the change, and restart the Druid cluster services.
 - druid.storage.type: It defaults to `hdfs` and does not need to be modified
 - druid.storage.storageDirectory:
```
If the target Hadoop cluster is non-HA: hdfs://{namenode_ip}:4007
If the target Hadoop cluster is HA: hdfs://HDFSXXXXX
Configure the full path, which can be found in the `fs.defaultFS` configuration item in the `core-site.xml` file of the target Hadoop cluster.
```

## Using COS
E-MapReduce Druid can use COS as the deep storage. This section describes how to configure COS as the deep storage of the Druid cluster.

First, you need to make sure that COS has been activated for both the Druid cluster and the target Hadoop cluster. You can activate COS when purchasing the clusters or configure COS in the EMR console after purchasing them.

1. Modify the `common.runtime.properties` configuration file in Druid configuration management:
	- druid.storage.type: `hdfs`
	- druid.storage.storageDirectory: `cosn://{bucket_name}/druid/segments`
You can create the `segments` directory on COS and set its permissions in advance.

2. Modify the `core-site.xml` configuration file in HDFS configuration management:
	- Set `fs.cosn.impl` to `org.apache.hadoop.fs.CosFileSystem`.
	- Add a new configuration item `fs.AbstractFileSystem.cosn.impl` and set it to `org.apache.hadoop.fs.CosN`.
3. Put the JAR packages related to [hadoop-cos](https://github.com/tencentyun/hadoop-cos/releases) (such as `cos_api-bundle-5.6.69.jar` and `hadoop-cos-2.8.5-8.1.6.jar`) into the `/usr/local/service/druid/extensions/druid-hdfs-storage`, `/usr/local/service/druid/hadoopdependencies/hadoop-client/2.8.5`, and `/usr/local/service/hadoop/share/hadoop/common/lib/` directories on each node of the cluster.

Save the configuration and restart the Druid cluster services.

## Modifying Druid parameters
After you create the E-MapReduce Druid cluster, a set of configuration items will be generated automatically. However, we recommend you modify the memory configuration as needed to achieve the optimal performance. You can do so on the [Configurations]https://intl.cloud.tencent.com/document/product/1026/31109) page in the EMR console.

When modifying the configuration, make sure that the modification is correct:
```
MaxDirectMemorySize >= druid.processing.buffer.sizeByte *(druid.processing.numMergeBuffers + druid.processing.numThreads + 1) 
```
Modification suggestion:
```
druid.processing.numMergeBuffers = max(2, druid.processing.numThreads / 4)
druid.processing.numThreads =  Number of cores - 1 (or 1)
druid.server.http.numThreads = max(10, (Number of cores * 17) / 16 + 2) + 30
```
For more information on the configuration, see [Configuration reference](https://druid.apache.org/docs/0.17.0/configuration/index.html#common-configurations).

## Using a router as a query node
Currently, a Druid cluster deploys the Broker process on the EMR master node by default. As there are many processes deployed on the master node, they may interfere with each other, which may lead to insufficient memory and compromise the query efficiency. In addition, many businesses require that the query nodes and core nodes be separately deployed. In this case, you can add one or more router nodes in the console and install the Broker processes so as to scale out the query nodes of the Druid cluster.

## Accessing the web
You can access the Druid cluster in the console through the port 18888 on the master node and configure the public IP on your own. After opening port 18888 in the security group and setting the bandwidth, you can access the cluster at `[http://{masterIp}:18888]()`.
