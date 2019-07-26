EMR consists of a series of open-source applications in the big data ecosystem. Each version of EMR contains a specific set of open-source programs. When you create a cluster, you can choose the most appropriate EMR version based on your actual needs.
>
>- EMR is upgraded on a regular basis with versions such as EMR v1.3.1, EMR v2.0.1, and EMR v2.1.0.
>- The components and their versions bundled with each EMR version are fixed. Currently, neither selecting multiple versions of a component nor changing a component version in one EMR version is supported. For example, Hadoop v2.7.3 and Spark v2.2.1 are built into EMR v2.0.1.
>- Once a version of EMR is selected for cluster creation, the EMR and components used by the cluster will not be automatically upgraded. For example, if EMR v2.0.1 is selected, then Hadoop will always be v2.7.3, and Spark will always be v2.2.1. Even if you subsequently upgrade EMR to v2.1.0 where Hadoop v2.8.4 and Spark v2.3.2 are included, the previously created cluster will not be affected, and only new clusters will use the new versions.
>- When you upgrade the cluster through data migration, for example, from EMR v2.0.1 to EMR v2.1.0, in order to avoid issues such as version incompatibility or environment changes, be sure to test the tasks to be migrated and ensure that they can work properly in the new software environment.

The components and their versions included in each EMR version are as follows:

| Component Name | EMR v1.3.1 | EMR v2.0.1 | EMR v2.1.0 |
|---------|---------|---------|---------|
| Release date |   - |   - | May 2019 |
| Flink | 1.2.0 | 1.2.0 | 1.4.2 |
| Ganglia | 3.7.2 | 3.7.2 | 3.7.2 |
| Hadoop | 2.7.3 | 2.7.3 | 2.8.4 |
| Hbase | 1.2.4 |  1.3.1 |1.3.1 |
| Hive | 2.1.1|  2.3.2 |2.3.3 |
| Hue | 3.12.0 | 3.12.0 | 4.4.0 |
| Ooize | 4.3.1 |  4.3.1 |4.3.1 |
| Presto |  0.161 |0.188 | 0.215 |
| Ranger | - |  0.7.1 |0.7.1 |
| Spark | 2.0.2 |  2.2.1 |2.3.2 |
| Sqoop | 1.4.6 | 1.4.6 | 1.4.7 |
| Storm | 1.1.0 | 1.1.0 | 1.1.0 |
| Tez | 0.8.5 | 0.8.5 | 0.8.5 |
| Zookeeper | 3.4.9 | 3.4.9 | 3.4.9 |
| Flume |  - |  - | 1.8.0 |
| Alluxio |	-	| -	| 1.8.1|
| Knox	| 1.2.0	| 1.2.0 |	-|

