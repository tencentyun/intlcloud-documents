## Product Release Overview
EMR consists of open-source applications in a series of big data ecosystems. It offers six [cluster types](https://intl.cloud.tencent.com/document/product/1026/31094) for you to deploy as needed. 

## Product Release Number Format
1. EMR version numbers are in the format of `EMR va.b.c` as detailed below:

	The meanings of `a` for different clusters are as follows:
	
	- For Hadoop clusters, `a` indicates the Hadoop versions supported by the current version. When `a` is `1` or `2`, Hadoop v2.x is supported; when `a` is `3`, Hadoop v3.x is supported.
	- For Druid clusters, `a` indicates the Druid versions supported by the current version. When `a` is `1`, Druid v0.17.x is supported.
	- For ClickHouse clusters, `a` indicates the ClickHouse versions supported by the current version. When `a` is `1`, ClickHouse v19.x and v20.x are supported.
	- For Kafka clusters, `a` indicates the Kafka versions supported by the current version. When `a` is `1`, Kafka v1.x is supported.
	- For Doris clusters, `a` indicates the Doris versions supported by the current version. When `a` is `1`, Doris v0.13x is supported.
	- For StarRocks clusters, `a` indicates the StarRocks versions supported by the current version. When `a` is `1`, StarRocks v2.x is supported.
 `b` indicates that the version has new components or supports component version upgrade.
 `c` indicates feature optimization.

>!
>- The components and their versions bundled with each EMR version are fixed. Currently, neither selecting multiple versions of a component nor changing a component version in one EMR version is supported. For example, Hadoop v2.8.5 and Spark v3.2.1 are built into EMR v2.7.0.
>- Once a version of EMR is selected for cluster creation, the EMR and component version used by the cluster will not be automatically upgraded. For example, if EMR v2.7.0 is selected, then Hadoop will always be v2.8.5, and Spark will always be v3.2.1. Even if EMR is upgraded to v2.8.0, Hadoop is upgraded to a higher version, and Spark is upgraded to v3.3.0 afterward, the previously created cluster will not be affected, and only new clusters will use the new versions.
>- When you upgrade the cluster through data migration, for example, from EMR v2.6.0 to EMR v2.7.0, in order to avoid issues such as version incompatibility or environment changes, be sure to test the tasks to be migrated and ensure that they can work properly in the new software environment.
>- EMR v2.4.0 comes with Kona (based on OpenJDK8). We have developed and improved Kona based on the characteristics of cloud scenarios.
