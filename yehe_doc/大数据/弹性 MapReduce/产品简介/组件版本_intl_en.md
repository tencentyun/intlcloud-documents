EMR consists of a series of open-source applications in the big data ecosystem. Each version of EMR contains a specific set of open-source programs. When you create a cluster, you can choose the most appropriate EMR version based on your actual needs.

EMR version numbers are in the format of `EMR va.b.c` as detailed below:
- `a` indicates the Hadoop version supported by the current version; for example, `a` of 1 or 2 means that Hadoop v2.X is supported.
- `b` indicates that the version has new components or supports component version upgrade.
- `c` represents feature optimization.

>
>- The components and their versions bundled with each EMR version are fixed. Currently, neither selecting multiple versions of a component nor changing a component version in one EMR version is supported. For example, Hadoop v2.7.3 and Spark v2.2.1 are built into EMR v2.0.1.
>- Once a version of EMR is selected for cluster creation, the EMR and components used by the cluster will not be automatically upgraded. For example, if EMR v2.0.1 is selected, then Hadoop will always be v2.7.3, and Spark will always be v2.2.1. Even if you subsequently upgrade EMR to v2.1.0 where Hadoop v2.8.4 and Spark v2.3.2 are included, the previously created cluster will not be affected, and only new clusters will use the new versions.
>- When you upgrade the cluster through data migration (for example, from EMR v2.0.1 to EMR v2.1.0), in order to avoid issues such as version incompatibility or environment changes, be sure to test the tasks to be migrated and ensure that they can work properly in the new software environment.

The following EMR versions support Hadoop v2.X:

| Component Name | EMR v1.3.1 | EMR v2.0.1 | EMR v2.1.0 | EMR v2.2.0 |
| --------- | ----------- | ----------- | ----------- | ----------- |
| Release date  |  -         |  -         | May 2019     | March 2020     |
| Hadoop    | 2.7.3       | 2.7.3       | 2.8.4       | 2.8.5       |
| Spark     | 2.0.2       | 2.2.1       | 2.3.2       | 2.4.3       |
| Hive      | 2.1.1       | 2.3.2       | 2.3.3       | 2.3.5       |
| Tez       | 0.8.5       | 0.8.5       | 0.8.5       | 0.9.2       |
| Presto    | 0.161       | 0.188       | 0.215       | 0.228       |
| Storm     | 1.1.0       | 1.1.0       | 1.1.0       | 1.2.3       |
| Flink     | 1.2.0       | 1.2.0       | 1.4.2       | 1.9.2       |
| HBase     | 1.2.4       | 1.3.1       | 1.3.1       | 1.4.9       |
| Phoneix   | 4.8.1       | 4.11.0      | 4.13.0      | 4.13.0      |
| Ganglia   | 3.7.2       | 3.7.2       | 3.7.2       | 3.7.2       |
| Hue       | 3.12.0      | 3.12.0      | 4.4.0       | 4.6.0       |
| Sqoop     | 1.4.6       | 1.4.6       | 1.4.7       | 1.4.7       |
| Ooize     | 4.3.1       | 4.3.1       | 4.3.1       | 5.1.0       |
| Ranger    | -           | 0.7.1       | 0.7.1       | 1.2.0       |
| ZooKeeper | 3.4.9       | 3.4.9       | 3.4.9       | 3.5.5       |
| Flume     | -           | -           | 1.8.0       | 1.9.0       |
| Impala    | -           | -           | -           | 2.10.0      |
| Kylin     | -           | -           | -           | 2.5.2       |
| Zeppelin  | -           | -           | -           | 0.8.2       |
| Alluxio   | -           | -           | 1.8.1       | 1.8.1       |
| Knox      | 1.2.0       | 1.2.0       | 1.2.0       | 1.2.0       |
| Kerberos  | -           | -           | 1.15.0      | 1.15.0      |
| Hudi      | -           | -           | -           | 0.5.1       |
| Superset  | -           | -           | -           | 0.35.2      |
| Livy      | -           | -           | -           | 0.7.0       |

The following EMR versions support Hadoop v3.X:

| Component Name | EMR v3.0.0 |
| --------- | ----------- |
| Release date  | January 2019      |
| Hadoop    | 3.1.2       |
| Spark     | 2.4.3       |
| Hive      | 3.1.1       |
| Tez       | 0.9.2       |
| Presto    | 0.222       |
| Flink     | 1.8.1       |
| HBase     | 2.2.0       |
| Hue       | 4.4         |
| Sqoop     | 1.4.7       |
| Ooize     | 5.1.0       |
| Ranger    | 2.0.0       |
| ZooKeeper | 3.4.9       |
| Flume     | 1.9.0       |
| Alluxio   | 1.8.1       |
| Knox      | 1.2.0       |



