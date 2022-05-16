## Deprecated EMR Versions
As the earlier product versions under a Hadoop cluster couldn't use the new features from the community due to the low versions of open-source components, the sale of EMR v1.3.1, v2.0.1, and v2.1.0 ended on March 31, 2022. Existing clusters on those versions can still be scaled out. We recommend you use EMR v2.6.0 to create a cluster as it contains the latest stable Hadoop 2.x version.


## EMR Standard Edition Changelog
EMR Standard currently supports the following cluster types: Hadoop, Druid, ClickHouse, Kafka, Doris, and StarRocks.
<dx-accordion>
::: Hadoop v2.x Standard supports the component versions listed in the following table:

| Component	| EMR v2.6.0	| EMR v2.5.1	| EMR v2.5.0	| EMR v2.4.0	| EMR v2.3.0	| EMR v2.2.0|
| :------------------------- | :---------- | :---------- | :---------- | :---------- | :---------- | :---------- |
| Release Date	| July 2021	| April 2021| 	September 2020	| August 2020| 	May 2020| 	March 2020|
| HDFS (required)	| 2.8.5	| 2.8.5	| 2.8.5	| 2.8.5	| 2.8.5	| 2.8.5|
| YARN (required)	| 2.8.5	| 2.8.5	| 2.8.5	| 2.8.5	| 2.8.5	| 2.8.5|
| ZooKeeper (required)	| 3.6.1	| 3.6.1	| 3.6.1	| 3.6.1	| 3.5.5	| 3.5.5|
| OpenLDAP (required)	| 2.4.44	| -	| -	| -| 	-| 	-|
| Knox (required)	| 1.2.0	| 1.2.0	| 1.2.0	| 1.2.0| 	1.2.0	| 1.2.0|
| Tez	| 0.9.2	| 0.9.2| 	0.9.2	| 0.9.2| 	0.9.2	| 0.9.2|
| Hive	| 2.3.7| 	2.3.7| 	2.3.7	| 2.3.7	| 2.3.5| 	2.3.5|
| Spark	| 3.0.2	| 3.0.0	| 3.0.0	| 3.0.0	| 2.4.3	| 2.4.3|
| Livy	| 0.8.0	| 0.7.0	| 0.7.0| 	0.7.0	| 0.7.0	| 0.7.0|
| Kyuubi	| 1.4.1| 	-| 	-| 	-	| -| 	-|
| Kylin	| 2.5.2	| 2.5.2	| 2.5.2| 	2.5.2	| 2.5.2	| 2.5.2|
| Presto	| -	| -	| -| 	-| 	0.228| 	0.228|
| PrestoSQL	| 332	| 332| 	332| 	332| 	-| 	-|
| Kudu	| 1.12.0	| 1.12.0| 	1.12.0	| 1.12.0	| -| 	-|
| Impala	| 3.4.0	| 2.10.0| 	2.10.0	| 2.10.0| 	2.10.0| 	2.10.0|
| Storm	| 1.2.3	| 1.2.3	| 1.2.3| 	1.2.3	| 1.2.3	| 1.2.3|
| Flink	| 1.12.1	| 1.10.0	| 1.10.0	| 1.10.0	| 1.9.2	| 1.9.2|
| HBase	| 1.4.9	| 1.4.9	| 1.4.9| 	1.4.9	| 1.4.9	| 1.4.9|
| Phoenix (integrated in HBase) | 	4.14.0	| 4.13.0	| 4.13.0| 	4.13.0| 	4.13.0	| 4.13.0|
| Alluxio	| 2.5.0| 	2.5.0	| 2.3.0| 	1.8.1	| 1.8.1	| 1.8.1|
| Iceberg	| 0.11.0	| -	| -| 	-| 	-| 	-|
| Hudi	| 0.7.0| 	-	| -	| -	| 0.5.1| 	0.5.1|
| Hue	| 4.6.0	| 4.6.0| 	4.6.0| 	4.6.0	| 4.6.0	| 4.6.0|
| Oozie	| 5.1.0	| 5.1.0	| 5.1.0| 	5.1.0	| 5.1.0| 	5.1.0|
| Zeppelin	| 0.9.1| 	0.8.2| 	0.8.2| 	0.8.2	| 0.8.2| 	0.8.2|
| Superset	| 0.35.2	| 0.35.2| 	0.35.2	| 0.35.2| 	0.35.2	| 0.35.2|
| TensorFlow on Spark	| 1.4.4	| 1.4.4	| 1.4.4	| 1.4.4	| 1.4.4	| -|
| Jupyter (installed with TensorFlow)	| 4.6.3	| 4.6.3	| 4.6.3| 	4.6.3| 	4.6.3	| -|
| Sqoop	| 1.4.7	| 1.4.7| 	1.4.7| 	1.4.7	| 1.4.7	| 1.4.7|
| Flume	| 1.9.0	| 1.9.0| 	1.9.0	| 1.9.0	| 1.9.0| 	1.9.0|
| Ranger| 	1.2.0| 	1.2.0| 	1.2.0| 	1.2.0	| 1.2.0	| 1.2.0|
| Kerberos (selectable only during creation)	| 1.15.0	| 1.15.0	| 1.15.0| 	1.15.0	| 1.15.0	| 1.15.0|
| Ganglia	| 3.7.2	| 3.7.2	| 3.7.2	| 3.7.2| 	3.7.2| 	3.7.2|

:::
::: Hadoop v3.x Standard supports the component versions listed in the following table:

| Component	| EMR v3.3.0	| EMR v3.2.1	| EMR v3.2.0	| EMR v3.1.0	| EMR v3.0.0|
| :------------------------- | :---------- | :---------- | :---------- | :---------- | :---------- |
| Release Date	| September 2021	| July 2021	| April 2021	| December 2020	| November 2019|
| HDFS (required)	| 3.2.2	| 3.2.2	| 3.2.2| 	3.1.2	| 3.1.2|
| YARN (required)	| 3.2.2	| 3.2.2	| 3.2.2	| 3.1.2	| 3.1.2|
| ZooKeeper (required)	| 3.6.1	| 3.6.1	| 3.6.1	| 3.6.1	| 3.4.9|
| OpenLDAP (required)	| 2.4.44	| 2.4.44| 	-| 	-| 	-|
| Knox (required) | 	1.2.0	| 1.2.0	| 1.2.0	| 1.2.0	| 1.2.0|
| Tez	| 0.10.1	| 0.10.0	| 0.10.0	| 0.9.2	| 0.9.2|
| Hive	| 3.1.2	| 3.1.2	| 3.1.2	| 3.1.1| 	3.1.1|
| Spark	| 3.0.2	| 3.0.2	| 3.0.2	| 2.4.3| 	2.4.3|
| Livy	| 0.8.0	| -| 	-| 	-| 	-|
| Kyuubi	| 1.1.0| 	-| 	-| 	-| 	-|
| Kylin	| 4.0.1	|	-| 	-| 	-| 	-|
| Presto	| -	| -	| -	| -	| 0.222|
| PrestoSQL	| 350	| 350	| 350	| 332| 	-|
| Impala	| 3.4.0	| 3.4.0	| 3.4.0	| 3.4.0	| 2.10.0|
| Kudu	| 1.15.0	| 1.13.0	| 1.13.0	| 1.13.0| 	-|
| HBase	| 2.3.5	| 2.3.3	| 2.3.3	| 2.3.3	| 2.2.0|
| Phoenix (integrated in HBase)	| 5.1.2	| 5.0.0	| 5.0.0	| 5.0.0	| -|
| Flink	| 1.12.1	| 1.12.1	| 1.12.1	| 1.10.0| 	1.8.1|
| Hue| 	4.10.0	| 4.4.0	| 4.4.0	| 4.4.0	| 4.4.0|
| Oozie	| 5.1.0	| 5.1.0	| 5.1.0| 	5.1.0	| 5.1.0|
| Zeppelin| 	0.9.1	| 0.9.1	| 0.9.1	| 0.8.2| 	-|
| Superset	| 1.4.1	| -| 	-	| -| 	-|
| Alluxio	| 2.5.0| 	2.5.0| 	2.5.0	| 2.3.0	| 1.8.1|
| Iceberg	| 0.11.0	| 0.11.0| 	0.11.0| 	-| 	-|
| Hudi	| 0.8.0	| -| 	-| 	-	| -|
| Flume	| 1.9.0	| 1.9.0| 	1.9.0| 	1.9.0| 	1.9.0|
| Sqoop	| 1.4.7	| 1.4.7	| 1.4.7	| 1.4.7	| 1.4.7|
| Ranger	| 2.1.0| 	2.1.0| 	2.1.0	| 2.0.0| 	2.0.0|
| Kerberos (selectable only during creation)	| 1.15.1	| 1.51.1	| 1.51.1| 	1.15.1	| 1.15.1|
| Ganglia	| 3.7.2| 	-| 	-| 	-| 	-|


:::
::: Druid clusters support the component versions listed in the following table:

| Component  | Druid v1.0.0 |
| --------------------- | ------------- |
| Release Date  | April 2020       |
| HDFS (required)    | 2.8.5         |
| YARN (required)    | 2.8.5         |
| Druid (required)     | 0.17.0        |
| ZooKeeper (required) | 3.5.5         |
| Knox (required)      | 1.2.0         |
| Superset              | 0.35.2        |
| Ganglia               | 3.7.2         |

:::
::: ClickHouse clusters support the component versions listed in the following table:

| Component 	| ClickHouse v1.2.0	| ClickHouse v1.1.0	| ClickHouse v1.0.0|
| ---------------------- | ------------------ | ------------------ |------------------ |
| Release Date	| September 2020	| May 2020	| April 2020|
| ClickHouse (required)	| 20.7.2.30	| 20.3.10.75	| 19.16.12.49|
| ZooKeeper (required)	| 3.4.9	| 3.4.9	| 3.4.9|
| Superset	| 0.35.2	| 0.35.2| 	-|


:::
::: Kafka clusters support the component versions listed in the following table:

| Component	| Kafka v1.0.0|
| ------------------------ | ------------- |
| Release Date	| May 2021 |
| Kafka (required)	| 1.1.1|
| KafkaManager (required)	| 2.0.0.2|
| Knox (required)	| 1.2.0|
| ZooKeeper (required)	| 3.6.1|

:::
::: Doris clusters support the component versions listed in the following table:

| Component	| Doris v1.2.0	| Doris v1.1.0		| Doris v1.0.0|
| ----------------- | ------------- |  ----------------- | ------------- |
| Release Date	| January 2022	| September 2021		| May 2021|
| Doris (required)	| 0.15.0	| 0.14.0		| 0.13.0|
| Knox (required)	| 1.2.0	| 1.2.0		| 1.2.0|
:::
::: StarRocks clusters support the component versions listed in the following table:

| Component	| StarRocks v1.0.0|
| ----------------- | ------------- |
| Release Date	| March 2022|
| StarRocks (required)	| 2.0.0|
| Knox (required)	| 1.2.0|
:::
</dx-accordion>


## EMR TianQiong Edition Changelog

Currently, EMR TianQiong supports Hadoop clusters only. It has integrated the enhanced edition of Spark and Tencent's proprietary JDK Kona.

<dx-accordion>
:::  Hadoop v2.x TianQiong supports the component versions listed in the following table:

| Component	| EMR TianQiong v1.0.0|
| --------------------- | -------------------- |
| Release Date	| November 2020|
| HDFS (required)	| 2.8.5|
| YARN (required)	| 2.8.5|
| ZooKeeper (required)	| 3.6.1|
| Knox (required)	| 1.2.0|
| Tez	| 0.9.2|
| Hive	| 2.3.7|
| Spark	| 3.0.1 **(Enhanced)**|
| Livy	| 0.7.0|
| Kylin	| 2.5.2|
| PrestoSQL	| 332|
| Impala	| 2.10.0|
| Kudu	| 1.12.0|
| HBase	| 1.4.9|
| Phoenix (integrated in HBase)	| 4.13.0|
| Storm	| 1.2.3|
| Flink	| 1.10.0|
| Hue	| 4.6.0|
| Oozie	| 5.1.0|
| Superset| 	0.35.2|
| Alluxio	| 2.3.0|
| Hudi	| 0.5.1|
| Sqoop	| 1.4.7|
| Flume	| 1.9.0|
| TensorFlow on Spark | 	1.4.4|
| Jupyter (installed with TensorFlow)	| 4.6.3|
| Ranger	| 1.2.0|
| Kerberos (selectable only during creation)	| 1.15.0|
| Ganglia	| 3.7.2|


:::
</dx-accordion>
