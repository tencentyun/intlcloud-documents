Elastic MapReduce (EMR) consists of a series of open-source applications in the big data ecosystem. EMR supports five types of clusters: Hadoop, Druid, ClickHouse, Kafka, and Doris. Each EMR version contains a specific set of open-source applications. When you create a cluster, you can choose the most appropriate EMR version based on your actual needs.

EMR comes with two component editions. One is the Standard edition, which is based on the stable open source community component edition to provide services. To keep your EMR clusters consistent with the evolution of the community, you are advised to choose the Standard edition. The other one is the TianQiong edition, which has incorporated Tencent Cloud's proprietary, mature, and stable features on the basis of the stable open source community component edition for better performance and stability. Please choose an edition that suits your business when you purchase a cluster. It is not recommended to switch between the two editions after the cluster is launched.

EMR version numbers are in the format of `EMR va.b.c` as detailed below:

- The meanings of `a` for different clusters are as follows:
 -For Hadoop clusters, `a` indicates the Hadoop versions supported by the current version. When `a` is `1` or `2`, Hadoop v2.X is supported; when `a` is `3`, Hadoop v3.X is supported.
 - For Druid clusters, `a` indicates the Druid versions supported by the current version. When `a` is `1`, Druid v0.17.X is supported.
 - For ClickHouse clusters, `a` indicates the ClickHouse versions supported by the current version. When `a` is `1`, ClickHouse v19.X and v20.X are supported.
 - For Kafka clusters, `a` indicates the Kafka versions supported by the current version. When `a` is `1`, Kafka v1.X is supported.
 - For Doris clusters, `a` indicates the Doris versions supported by the current version. When `a` is `1`, Doris v0.13X is supported.
- `b` indicates that the version has new components or supports component version upgrade.
- `c` indicates feature optimization.


>!
>- The components and their versions bundled with each EMR version are fixed. Currently, neither selecting multiple versions of a component nor changing a component version in one EMR version is supported. For example, Hadoop v2.7.3 and Spark v2.2.1 are built into EMR v2.0.1.
>- Once a version of EMR is selected for cluster creation, the EMR and component version used by the cluster will not be automatically upgraded. For example, if EMR v2.0.1 is selected, then Hadoop will always be v2.7.3, and Spark will always be v2.2.1. Even if EMR is upgraded to v2.1.0, Hadoop is upgraded to v2.8.4, and Spark is upgraded to v2.3.2 afterward, the previously created cluster will not be affected, and only new clusters will use the new versions.
>- When you upgrade the cluster through data migration, for example, from EMR v2.0.1 to EMR v2.1.0, in order to avoid issues such as version incompatibility or environment changes, be sure to test the tasks to be migrated and ensure that they can work properly in the new software environment.
>- EMR v2.4.0 comes with Kona (based on OpenJDK8). We have developed and improved Kona based on the characteristics of cloud scenarios.


Hadoop cluster is available in Standard Edition and TianQiong Edition. For more information on the differences between the two editions, please see [EMR TianQiong Introduction](https://intl.cloud.tencent.com/document/product/1026/38962).

## EMR Standard

Currently, EMR Standard supports the Hadoop, Druid, ClickHouse, Kafka, and Doris clusters.
<dx-accordion>
::: Hadoop v2.X Standard supports the component versions listed in the following table:

| Component | EMR v1.3.1 | EMR v2.0.1 | EMR v2.1.0 | EMR v2.2.0 | EMR v2.3.0 | EMR v2.4.0 |EMR v2.5.0 | EMR v2.5.1 | EMR v2.6.0 |
| -------------------------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Release Date                   | -           | -           | May 2019     | March 2020     | May 2020     | August 2020     | September 2020     | April 2021     | July 2021     |
| Hadoop (required)     | 2.7.3       | 2.7.3       | 2.8.4       | 2.8.5       | 2.8.5       | 2.8.5       | 2.8.5       | 2.8.5 | 2.8.5   |
| Spark_Hadoop           | 2.7 2.0.2    | 2.7 2.2.1    | 2.8 2.3.2    | 2.8 2.4.3    | 2.8 2.4.3    | 2.8 3.0.0    | 2.8 3.0.0    | -           | -           |
| Spark                      | -           | -           | -           | -           | -           | -           | -           | 3.0.0       | 3.0.2       |
| Hive                       | 2.1.1       | 2.3.2       | 2.3.3       | 2.3.5       | 2.3.5       | 2.3.7       | 2.3.7       | 2.3.7       | 2.3.7       |
| Tez                        | 0.8.5       | 0.8.5       | 0.8.5       | 0.9.2       | 0.9.2       | 0.9.2       | 0.9.2       | 0.9.2       | 0.9.2       |
| Presto                     | 0.161       | 0.188       | 0.215       | 0.228       | 0.228       | -           | -           | -           | -           |
| PrestoSQL                  | -           | -           | -           | -           | -           | 332         | 332         | 332         | 332         |
| Storm                      | 1.1.0       | 1.1.0       | 1.1.0       | 1.2.3       | 1.2.3       | 1.2.3       | 1.2.3       | 1.2.3       | 1.2.3       |
| Flink                      | 1.2.0       | 1.2.0       | 1.4.2       | 1.9.2       | 1.9.2       | 1.10.0      | 1.10.0      | 1.10.0      | 1.12.1      |
| HBase                      | 1.2.4       | 1.3.1       | 1.3.1       | 1.4.9       | 1.4.9       | 1.4.9       | 1.4.9       | 1.4.9       | 1.4.9       |
| Phoenix (integrated in HBase) | 4.8.1       | 4.11.0      | 4.13.0      | 4.13.0      | 4.13.0      | 4.13.0      | 4.13.0      | 4.13.0      | 4.14.0      |
| Ganglia                    | 3.7.2       | 3.7.2       | 3.7.2       | 3.7.2       | 3.7.2       | 3.7.2       | 3.7.2       | 3.7.2       | 3.7.2       |
| Hue                        | 3.12.0      | 3.12.0      | 4.4.0       | 4.6.0       | 4.6.0       | 4.6.0       | 4.6.0       | 4.6.0       | 4.6.0       |
| Sqoop                      | 1.4.6       | 1.4.6       | 1.4.7       | 1.4.7       | 1.4.7       | 1.4.7       | 1.4.7       | 1.4.7       | 1.4.7       |
| Oozie                      | 4.3.1       | 4.3.1       | 4.3.1       | 5.1.0       | 5.1.0       | 5.1.0       | 5.1.0       | 5.1.0       | 5.1.0       |
| Ranger                     | -           | 0.7.1       | 0.7.1       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       |
| ZooKeeper (required)  | 3.4.9       | 3.4.9       | 3.4.9       | 3.5.5       | 3.5.5       | 3.6.1       | 3.6.1       | 3.6.1       | 3.6.1       |
| Flume                      | -           | -           | 1.8.0       | 1.9.0       | 1.9.0       | 1.9.0       | 1.9.0       | 1.9.0       | 1.9.0       |
| Impala                     | -           | -           | -           | 2.10.0      | 2.10.0      | 2.10.0      | 2.10.0      | 2.10.0      | 3.4.0       |
| Kylin                      | -           | -           | -           | 2.5.2       | 2.5.2       | 2.5.2       | 2.5.2       | 2.5.2       | 2.5.2       |
| Zeppelin                   | -           | -           | -           | 0.8.2       | 0.8.2       | 0.8.2       | 0.8.2       | 0.8.2       | 0.9.1       |
| Alluxio                    | -           | -           | 1.8.1       | 1.8.1       | 1.8.1       | 1.8.1       | 2.3.0       | 2.5.0       | 2.5.0       |
| Knox (required)           | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       |
| Kerberos                   | -           | -           | 1.15.0      | 1.15.0      | 1.15.0      | 1.15.0      | 1.15.0      | 1.15.0      | 1.15.0      |
| Hudi                       | -           | -           | -           | 0.5.1       | 0.5.1       | -           | -           | -           | 0.7.0       |
| Superset                   | -           | -           | -           | 0.35.2      | 0.35.2      | 0.35.2      | 0.35.2      | 0.35.2      | 0.35.2      |
| Livy                       | -           | -           | -           | 0.7.0       | 0.7.0       | 0.7.0       | 0.7.0       | 0.7.0       | 0.8.0       |
| TensorFlowSpark            | -           | -           | -           | -           | 1.4.4       | 1.4.4       | 1.4.4       | 1.4.4       | 1.4.4       |
| Jupyter                    | -           | -           | -           | -           | 4.6.3       | 4.6.3       | 4.6.3       | 4.6.3       | 4.6.3       |
| Kudu                       | -           | -           | -           | -           | -           | 1.12.0      | 1.12.0      | 1.12.0      | 1.12.0      |
| OpenLDAP (required)         | -           | -           | -           | -           | -           | -           | -           | -           | 2.4.44      |

:::
::: Hadoop v3.X Standard supports the component versions listed in the following table:

| Component              | EMR v3.0.0 | EMR v3.1.0 | EMR v3.2.0 | EMR v3.2.1 | EMR v3.3.0 |
| :-------------------- | :---------- | :---------- | :---------- | :---------- | :---------- |
| Release Date   | November 2019     | December 2020     | April 2021     | July 2021     | September 2021     |
| Hadoop (required)        | 3.1.2       | -           | -           | -           | 3.2.2       |
| HDFS (required)          | -           | 3.1.2       | 3.2.2       | 3.2.2       | 3.2.2       |
| Yarn (required)          | -           | 3.1.2       | 3.2.2       | 3.2.2       | 3.2.2       |
| Spark_ Hadoop         | 3.12.4.3    | -           | -           | -           | -           |
| Spark                 | -           | 2.4.3       | 3.0.2       | 3.0.2       | 3.0.2       |
| Hive                  | 3.1.1       | 3.1.1       | 3.1.2       | 3.1.2       | 3.1.2       |
| Tez                   | 0.9.2       | 0.9.2       | 0.10.0      | 0.10.0      | 0.10.1      |
| Presto                | 0.222       | -           | -           | -           |             |
| PrestoSQL             | -           | 332         | 350         | 350         | 350         |
| Flink                 | 1.8.1       | 1.10.0      | 1.12.1      | 1.12.1      | 1.12.1      |
| HBase                 | 2.2.0       | 2.3.3       | 2.3.3       | 2.3.3       | 2.3.5       |
| Hue                   | 4.4.0       | 4.4.0       | 4.4.0       | 4.4.0       | 4.10.0      |
| Sqoop                 | 1.4.7       | 1.4.7       | 1.4.7       | 1.4.7       | 1.4.7       |
| Oozie                 | 5.1.0       | 5.1.0       | 5.1.0       | 5.1.0       | 5.1.0       |
| Ranger                | 2.0.0       | 2.0.0       | 2.1.0       | 2.1.0       | 2.1.0       |
| ZooKeeper (required) | 3.4.9       | 3.6.1       | 3.6.1       | 3.6.1       | 3.6.1       |
| Flume                 | 1.9.0       | 1.9.0       | 1.9.0       | 1.9.0       | 1.9.0       |
| Impala                | 2.10.0      | 3.4.0       | 3.4.0       | 3.4.0       | 3.4.0       |
| Alluxio               | 1.8.1       | 2.3.0       | 2.5.0       | 2.5.0       | 2.5.0       |
| Knox (required)      | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       |
| Kudu                  | -           | 1.13.0      | 1.13.0      | 1.13.0      | 1.15.0      |
| Kerberos              | 1.15.1      | 1.15.1      | 1.51.1      | 1.51.1      | 1.15.1      |
| Zeppelin              | -           | 0.8.2       | 0.9.1       | 0.9.1       | 0.9.1       |
| Iceberg               | -           | -           | 0.11.0      | 0.11.0      | 0.11.0      |
| OpenLDAP (required)  | -           | -           | -           | 2.4.44      | 2.4.44      |
| Hudi                  | -           | -           | -           | -           | 0.8.0       |
| Kyuubi                | -           | -           | -           | --          | 1.1.0       |
| Livy                  | -           | -           | -           | -           | 0.8.0       |
| Ganglia               | -           | -           | -           | -           | 3.7.2       |

:::
::: Druid clusters support the component versions listed in the following table:

| Component  | Druid v1.0.0 |
| --------------------- | ------------- |
| Release Date  | April 2020       |
| Hadoop (required)    | 2.8.5         |
| Druid (required)     | 0.17.0        |
| ZooKeeper (required) | 3.5.5         |
| Knox (required)      | 1.2.0         |
| Superset              | 0.35.2        |
| Ganglia               | 3.7.2         |

:::
::: ClickHouse clusters support the component versions listed in the following table:

| Component | ClickHouse v1.0.0 | ClickHouse v1.1.0 |
| ---------------------- | ------------------ | ------------------ |
| Release Date   | April 2020                  | May 2020                 |
| ClickHouse (required) | 19.16.12.49        | 20.3.10.75         |
| ZooKeeper (required)  | 3.4.9              | 3.4.9              |
| Superset               | -                  | 0.35.2             |

:::
::: Kafka clusters support the component versions listed in the following table:

| Component  | Kafka v1.0.0 |
| ------------------------ | ------------- |
| Release Date                 | May 2021       |
| Kafka (required)        | 1.1.1         |
| KafkaManager (required) | 2.0.0.2       |
| Knox (required)         | 1.2.0         |
| ZooKeeper (required)    | 3.6.1         |

:::
::: Doris clusters support the component versions listed in the following table:

| Component          | Doris v1.0.0 |
| ----------------- | ------------- |
| Release Date                 | May 2021       |
| Doris (required) | 0.13.0        |
| Knox (required)  | 1.2.0         |

:::
</dx-accordion>


## EMR TianQiong

Currently, EMR TianQiong supports Hadoop clusters only. It has integrated the enhanced edition of Spark and Tencent's proprietary JDK Kona.

<dx-accordion>
:::  Hadoop v2.X TianQiong supports the component versions listed in the following table:**

| Component | EMR TianQiong v1.0.0 |
| --------------------- | -------------------- |
| Release Date  | November 2020      |
| Hadoop (required)    | 2.8.5                |
| Spark      | 3.0.1 **(Enhanced)**      |
| Hive                  | 2.3.7                |
| Tez                   | 0.9.2                |
| PrestoSQL             | 332                  |
| Storm                 | 1.2.3                |
| Flink                 | 1.10.0               |
| HBase                 | 1.4.9                |
| Phoenix               | 4.13.0               |
| Ganglia               | 3.7.2                |
| Hue                   | 4.6.0                |
| Sqoop                 | 1.4.7                |
| Oozie                 | 5.1.0                |
| Ranger                | 1.2.0                |
| ZooKeeper (required) | 3.6.1                |
| Flume                 | 1.9.0                |
| Impala                | 2.10.0               |
| Kylin                 | 2.5.2                |
| Alluxio               | 2.3.0                |
| Knox (required)      | 1.2.0                |
| Kerberos              | 1.15.0               |
| Hudi                  | 0.5.1                |
| Superset              | 0.35.2               |
| Livy                  | 0.7.0                |
| TensorFlowSpark       | 1.4.4                |
| Jupyter               | 4.6.3                |
| Kudu                  | 1.12.0               |

:::
</dx-accordion>
