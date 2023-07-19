## Deprecated EMR Versions
We have deprecated some earlier EMR versions because their open-source components are too old to support new features of their communities. You can't create new clusters with deprecated versions, but you can still scale in or out existing clusters.
Deprecated EMR on CVM versions:
- Hadoop cluster type: EMR v1.3.1, EMR v2.0.1, EMR v2.1.0, EMR v2.2.0, EMR v2.4.0, EMR v2.5.1, EMR v3.0.0, EMR v3.2.0, and EMR-TianQiong v1.0.0.
- Druid cluster type: Druid v1.0.0.

For full-feature access and better stability, we recommend you create clusters with the latest stable version of each cluster type.




## EMR on CVM Release Notes
EMR on CVM supports four cluster types: Hadoop, Druid, Kafka, and StarRocks. For Hadoop clusters, the Standard edition and JDK 11-Beta edition are available.
<dx-accordion>
::: Hadoop Standard v2.x supports the following component versions:

| Component | EMR v2.7.0| EMR v2.6.0|  EMR v2.5.0|  EMR v2.3.0| 
| :------------------------- |  :---------- | :---------- |:---------- | :---------- | 
| Release time | July 2022 | July 2021 | September 2020 | May 2020 | 
| HDFS (required) |2.8.5|2.8.5|2.8.5|2.8.5|
| YARN (required)| 2.8.5| 2.8.5| 2.8.5| 2.8.5| 
| ZooKeeper (required) | 3.6.3| 3.6.1| 3.6.1| 3.5.5| 
| OpenLDAP (required) | 2.4.44| 2.4.44| -| -| 
| Knox (required) | 1.6.1| 1.2.0| 1.2.0| 1.2.0| 
| Tez| 0.10.1| 0.9.2| 0.9.2| 0.9.2| 
| Hive| 2.3.9| 2.3.7| 2.3.7| 2.3.5| 
| Spark| 3.2.1| 3.0.2| 3.0.0| 2.4.3| 
| Livy| 0.8.0| 0.8.0| 0.7.0| 0.7.0| 
| Kyuubi| 1.4.1| 1.4.1| -| -| 
| Kylin| 4.0.1| 2.5.2| 2.5.2| 2.5.2| 
| Presto| -| -| -| 0.228| 
| Trino (PrestoSQL)| 385| 332| 332| -| 
| Kudu| 1.15.0| 1.12.0| 1.12.0| -| 
| Impala| 3.4.0| 3.4.0| 2.10.0| 2.10.0| 
| Storm| 1.2.3| 1.2.3| 1.2.3| 1.2.3| 
| Flink| 1.14.3| 1.12.1| 1.10.0| 1.9.2| 
| HBase| 2.4.5| 1.4.9| 1.4.9| 1.4.9| 
| Phoenix (integrated in HBase) | 5.1.2| 4.14.0| 4.13.0| 4.13.0| 
| Alluxio| 2.8.0| 2.5.0| 2.3.0| 1.8.1| 
| Iceberg| 0.13.0| 0.11.0| -| -| 
| Hudi| 0.11.0| 0.7.0| -| 0.5.1| 
| Hue| 4.10.0| 4.6.0| 4.6.0| 4.6.0| 
| Oozie| 5.2.1| 5.1.0| 5.1.0| 5.1.0| 
| Zeppelin| 0.10.1| 0.9.1| 0.8.2| 0.8.2| 
| Superset| 1.4.1| 0.35.2| 0.35.2| 0.35.2| 
| TensorFlowSpark| 1.4.4| 1.4.4| 1.4.4| 1.4.4| 
| Jupyter (installed with TensorFlow) | 4.6.3| 4.6.3| 4.6.3| 4.6.3| 
| Sqoop| 1.4.7| 1.4.7| 1.4.7| 1.4.7| 
| Flume| 1.9.0| 1.9.0| 1.9.0| 1.9.0| 
| Ranger| 2.1.0| 1.2.0| 1.2.0| 1.2.0| 
| Kerberos (selectable only during cluster creation) | 1.15.0| 1.15.0| 1.15.0| 1.15.0| 
| Ganglia| 3.7.2| 3.7.2| 3.7.2| 3.7.2| 
| GooseFS| 1.2.0| -| -| -| 


:::
::: Hadoop Standard v3.x supports the following component versions:

| Component              | EMR v3.5.0 | EMR v3.4.0| EMR v3.3.0| EMR v3.2.1|  EMR v3.1.0| 
| :------------------------- |  :---------- |:---------- | :---------- | :---------- | :---------- | 
| Release time   | October 2022     | April 2022     | September 2021     | July 2021     | December 2020     | 
|  HDFS (required) | 3.2.2| 3.2.2|3.2.2| 3.2.2| 3.1.2| 
|YARN (required) | 3.2.2| 3.2.2|3.2.2| 3.2.2| 3.1.2| 
| ZooKeeper (required)| 3.6.3| 3.6.3| 3.6.1| 3.6.1| 3.6.1| 
| OpenLDAP (required) | 2.4.44| 2.4.44| 2.4.44| 2.4.44|  -| 	
| Knox (required)     | 1.6.1| 1.6.1 | 1.2.0| 1.2.0|  1.2.0| 
| Tez                   | 0.10.2| 0.10.1| 0.10.1| 0.10.0|  0.9.2| 
| Hive |3.1.3|3.1.2|  3.1.2| 3.1.2|  3.1.1| 	
| Spark | 3.2.2|3.2.1 |3.0.2| 3.0.2|2.4.3| 	
| Livy| 0.8.0| 0.8.0|0.8.0| -|  -| 	
| Kyuubi| 1.6.0|1.4.1 | 1.1.0| -|  -| 	
| Kylin| 4.0.1| 4.0.1|4.0.1|-|  -| 
| Presto|-| -| -| -|  -| 
| Trino (PrestoSQL) |389 | 372 (renamed Trino) | 350| 350| 332| 	 
| Impala| 4.1.0|4.0.0 | 3.4.0| 3.4.0| 3.4.0| 
| Kudu| 1.16.0|1.15.0| 1.15.0| 1.13.0|  1.13.0| 
| HBase| 2.4.5 |2.4.5 | 2.3.5| 2.3.3| 2.3.3| 2.3.3| 
| Phoenix (integrated in HBase) |  5.1.2| 5.1.2|5.1.2| 5.0.0| 5.0.0| 
| Flink| 1.14.5|1.14.3| 1.12.1| 1.12.1|  1.10.0| 	
| Hue | 4.10.0| 4.10.0|4.10.0| 4.4.0|  4.4.0| 
| Oozie|5.2.1| 5.1.0| 5.1.0| 5.1.0| 5.1.0| 
| Zeppelin| 0.10.1 | 0.10.1 | 0.9.1| 0.9.1|  0.8.2| 	
| Superset|1.5.1| 1.4.1|1.4.1| -| -| 	
| Alluxio|2.8.0|2.8.0 |2.5.0| 2.5.0| 2.3.0| 
| Iceberg| 0.13.1 | 0.13.1 | 0.11.0| 0.11.0|  -| 	
| Hudi|0.12.0| 0.11.0 | 0.8.0| -|  -| 
| Flume|1.10.0| 1.9.0| 1.9.0| 1.9.0|  1.9.0| 	
| Sqoop| 1.4.7| 1.4.7|1.4.7| 1.4.7| 1.4.7| 
| Ranger|2.3.0| 2.1.0| 2.1.0| 2.1.0|  2.0.0| 
| Kerberos (selectable only during cluster creation) | 1.15.1| 1.15.1| 1.15.1| 1.51.1| 1.15.1| 
|Ganglia| 3.7.2|3.7.2|3.7.2| -|  -| 	
|Delta Lake|2.0.0|-|-|-|-|
|GooseFS|1.3.0|1.2.0|-|-|-|


:::
::: Hadoop JDK11-Beta supports the following component versions:
EMR v4.x is a beta version based on the JDK 11 environment, so all components are also based on the JDK 11 environment. Currently, you can only create Hadoop clusters with this version.

Component                  | EMR v4.0.0 |
| ---------------------------- | ---------- |
| Release time                     | March 2023    |
| HDFS (required)                | 3.2.2      |
| YARN (required)               | 3.2.2      |
| ZooKeeper (required)    | 3.6.3         |
| OpenLDAP (required)        | 2.4.44     |
| Knox (required)      | 1.6.1      |
| Tez                    | 0.10.2     |
| Hive                    | 3.1.3      |
| Spark                        | 3.2.2      |
| Livy                    | 0.8.0      |
| Kyuubi                       | 1.6.0      |
| Kylin                   | 4.0.1      |
| Presto                       | -          |
| Trino (PrestoSQL)           | 389        |
| Impala                 | 4.1.0      |
| Kudu                | 1.16.0     |
| HBase                   | 2.4.5      |
| Phoenix (integrated in HBase)| 5.1.2      |
| Flink                 | 1.14.5     |
| Hue                     | 4.10.0     |
| Oozie                        | 5.2.1      |
| Zeppelin                     | 0.10.1     |
| Superset            | 1.5.1      |
| Alluxio                | 2.8.0      |
| Iceberg     | 0.13.1     |
| Hudi                     | 0.12.0     |
| Flume                | 1.10.0     |
| Sqoop                 | 1.4.7                |
| Ranger             | 2.3.0      |
| Kerberos (selectable only during cluster creation)  | 1.15.1     |
| Ganglia               | 3.7.2         |
|Delta Lake     | 2.0.0      |
| GooseFS               | 1.3.0      |

:::
::: Druid clusters support the following component versions:

| Component | Druid v1.1.0| 
| ---------------------- | ------------------ |
| Release time | August 2022| 
| HDFS (required)    | 2.8.5         | 
| YARN (required)	| 2.8.5| 
| Druid (required)     | 0.23.0        | 
| ZooKeeper (required)    | 3.6.3         | 
| Knox (required)  | 1.2.0   | 
| Superset              | 1.4.1        | 
| Ganglia	| 3.7.2| 


:::
::: Kafka clusters support the following component versions:

| Component| Kafka v2.0.0| Kafka v1.0.0| 
| ------------------------ | ------------- | ------------- |
| Release time | March 2023     | May 2021     | 
| Kafka (required)       |2.4.1| 1.1.1| 
| KafkaManager (required) |2.0.0.2|  2.0.0.2| 
| Knox (required) | 1.2.0| 1.2.0| 
| ZooKeeper (required) |3.6.3| 3.6.1| 

:::
::: StarRocks clusters support the following component versions:

| Component | StarRocks v1.4.0 | StarRocks v1.3.0| StarRocks v1.2.0| StarRocks v1.1.0|
| --------------------- | ---------------- | ---------------- | ---------------- |---------------- |
| Release time | April 2023 | March 2023| November 2022 | August 2022 |
| StarRocks (required) | 2.5.3 | 2.4.3            | 2.3.2            | 2.2.2            |
| Knox (required) | 1.2.0| 1.2.0| 1.2.0| 1.2.0|

:::
</dx-accordion>

## EMR on TKE Release Notes

Component                  | EMR v4.0.0 |
| --------- | ---------- |
| Release time | May 2023      |
| Spark                        | 3.2.2      |
| Kyuubi                       | 1.6.0      |
| ZooKeeper | 3.6.3      |
| OpenLDAP  | 2.4.44     |
| Knox      | 1.6.1      |
| Tez                    | 0.10.2     |
| Hive                    | 3.1.3      |
| Trino | 389        |
| Ranger             | 2.3.0      |
| Hue                     | 4.10.0     |
| RSS       | 0.6.0      |

