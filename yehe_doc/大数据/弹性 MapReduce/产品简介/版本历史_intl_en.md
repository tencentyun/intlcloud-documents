## February 2020
| Update | Description | Document |
| ---------------------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| Hive metadatabase can be shared | Hive metadata of a new cluster can be stored in an associated external Hive metadatabase, so it can be shared by multiple Hive clusters to implement data exchange between clusters | [Managing Hive Metadata](https://intl.cloud.tencent.com/document/product/1026/35013) |
| Cluster operation logging is optimized | New display items are added to improve the readability of operation logs | - |
| International edition is launched | The international edition is available in the Beijing, Shanghai, Guangzhou, and Mumbai regions |      -      |


## January 2020

| Update | Description | Document |
| ---------------------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| EMR supports cloud disk encryption | EMR allows CBS users on the allowlist to select cloud disk encryption when creating an EMR cluster | [Cloud Disk Encryption](https://intl.cloud.tencent.com/document/product/362/33139) |
| Task nodes support mounting multiple cloud disks | Task nodes support mounting cloud disks when a cluster is created or scaled |   -   |

## December 2019

| Update | Description | Document |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Configuration distribution is supported | If the configuration of a node is different from that in the current configuration group, the configuration in the configuration group can be distributed to the node | -     |
| CAM resource-level authorization is supported | CAM authorization at the resource level is supported    | -   |
| Association with CHDFS is supported | Association with CHDFS and read/write of data on CHDFS are supported | [Mounting CHDFS](https://intl.cloud.tencent.com/document/product/1026/34525) |
| An AMD model is available |  AMD Standard SA2 is available in the Beijing, Shanghai, and Guangzhou regions | [Standard SA2](https://intl.cloud.tencent.com/document/product/213/11518) |
| Cluster monitoring overview page is launched | The cluster monitoring overview page is added with cluster, server, and service status views | [Cluster Overview](https://intl.cloud.tencent.com/document/product/1026/31117) |
| Metric display granularity can be selected as needed on the service monitoring page  | The service monitoring page is optimized where metric display granularity can be selected as needed | -   |
| Server service deployment and load status views are added to the server monitoring page | The server monitoring page is optimized where server service deployment and load status views are added | -   |

## November 2019

| Update | Description | Document |
| --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| The node specification management feature is launched | Node specification management is supported. Default specifications can be set for different types of nodes based on the billing mode. The default billing mode is pay-as-you-go | [Node Specification Management](https://intl.cloud.tencent.com/document/product/1026/34533) |
| Configuration management supports ZooKeeper, Alluxio, and Flink  | Zookeeper, Alluxio, and Flink are supported in configuration management   | -    |
| The cluster and node tagging feature is launched | Tags can be set for clusters and nodes  | [Tags](https://intl.cloud.tencent.com/document/product/1026/34532) |
| New models are available in the Beijing, Shanghai, and Guangzhou regions | S5, M5, C3, and CN3 models are available in the Beijing, Shanghai, and Guangzhou regions | - |

## October 2019

| Update | Description | Document |
| -------------------- | -------------------------------------------------- | ------------------------------------------------------------ |
| EMR 3.0.0 is released  | EMR 3.0.0 is released with updated versions of main components | [Component Version](https://intl.cloud.tencent.com/document/product/1026/31095) |

## September 2019

| Update | Description | Document |
| ---------------------- | ------------------------------------------------------------ | -------- |
| TencentCloud API fully supports v3.0 | TencentCloud API fully supports v3.0. Output/input parameters of certain existing v3.0 APIs are standardized, and v2.0 APIs are fully supported in v3.0 | -        |
| Console configuration is modified | The escape feature for special characters is disused | -        |
| Cloud Monitor alarm policy is supported | Alarm policies can be configured for key monitoring metrics for servers and services support in Cloud Monitor (in the Elastic MapReduce product category) | -   |

## August 2019

| Update | Description | Document |
| ------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| The software configuration feature is launched | The software configuration feature is launched, which supports creating a cluster by entering custom parameters. The external cluster access feature is provided as well | [Software Configuration](https://intl.cloud.tencent.com/document/product/1026/34530) |
| Remote login ports for new clusters can be customized | The remote login port can be enabled/disabled when a new cluster is purchased  | -  |
| New cluster supports mounting multiple cloud disks | Multiple cloud disks can be mounted to a new cluster   | -        |
| The feature of scaling specified components is launched   | Specified components can be scaled  | -        |
| New component monitoring metrics are added | New monitoring metrics for Spark, Hive, Presto, and ZooKeeper are added | -    |

## July 2019

| Update | Description | Document |
| -------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| The HBase table-level monitoring feature is launched | HBase table-level monitoring is supported, covering the number of read/write requests and storage of each table in HBase | [HBase Table-Level Monitoring](https://intl.cloud.tencent.com/document/product/1026/34528) |
| New models are available | Standard S4 and Standard Network-Optimized SN3ne models are available in the Beijing, Shanghai, and Guangzhou regions | - |
| Monitoring page interactions are optimized and new monitoring metrics are added | Monitoring page interactions are optimized and new monitoring metrics are added | - |
| WebUI proxy address is optimized   | The WebUI proxy address is optimized  | -   |

## June 2019

| Update | Description | Document |
| -------------------------------- | -------------------------------- | ------------------------------------------------------------ |
| The feature of accessing external cluster is launched |  Access to external clusters is supported | -  |
| The bootstrap action setting feature is launched  | Bootstrap actions can be set during cluster configuration | [Setting Bootstrap Actions](https://intl.cloud.tencent.com/document/product/1026/34531) |
| The feature of node-level component parameter configuration distribution is launched | Component parameter configurations can be distributed to the node level | -  |
| The parameter configuration rollback feature is launched | Parameter configuration rollback is supported | [Parameter Configuration Rollback](https://intl.cloud.tencent.com/document/product/1026/34524) |

## May 2019

| Update | Description | Document |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| EMR 2.1.0 is released | EMR 2.1.0 is released with updated versions of main components | [Component Versions](https://intl.cloud.tencent.com/document/product/1026/31095) |
| Kerberos secure cluster is supported | EMR supports the creation of secure clusters, i.e., the open-source components in the cluster are launched in Kerberos secure mode. In this security environment, only authenticated clients can access the services (such as HDFS) of the cluster | [Kerberos Overview](https://intl.cloud.tencent.com/document/product/1026/31163) |
| Monitoring metrics are optimized | Host, HDFS, YARN, and Hbase monitoring metrics are optimized | [Monitoring Metrics](https://intl.cloud.tencent.com/document/product/1026/31121) |
| Console style is optimized | The console style is optimized for an improved interactive experience  | -                                                            |
| CVM and TencentDB naming is optimized | CVM and TencentDB naming is optimized with the EMR cluster serial number for easier locating of the cluster information | -                                                            |
| The public IP of a master node is optional | The public IP address of a master node is changed to optional   | -  |
| The number of common nodes is adjustable as needed  | The number of common nodes can be adjusted as needed   | -        |

## March 2019

| Update | Description | Document |
| ---------- | ------------------------------------------------------------ | -------- |
| New models are available | The I3 model is available in the Beijing, Shanghai, and Guangzhou regions. This model is a CVM allowlist model, and you can purchase it only if you are in the I3 model allowlist | - |
| Router node is supported  | Router nodes are mainly used to relieve the load of master nodes and as task submitters | [Node Types](https://intl.cloud.tencent.com/document/product/1026/31094) |
| Node configuration adjustment is supported | Node configurations can be upgraded | [Configuration Adjustment](https://intl.cloud.tencent.com/document/product/1026/31114) |

## January 2019

| Update | Description | Document |
| -------------------- | ---------------------------------- | ------------------------------------------------------------ |
| Adding new components to existing clusters is support | New components can be added to existing clusters | [Adding Components](https://intl.cloud.tencent.com/document/product/1026/31108) |
