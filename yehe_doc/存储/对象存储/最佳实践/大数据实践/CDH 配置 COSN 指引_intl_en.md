## Overview

CDH (Cloudera’s distribution, including Apache Hadoop) is one of the most popular Hadoop distributions in the industry. This document describes how to use COSN, a flexible, cost-effective big-data solution, in a CDH environment to separate big data computing from storage.

>?In this document, COSN refers to Hadoop-COS, a file system built based on COSN.

The table below shows which big data modules are supported by COSN:

| Module Name | Supported | Service Module to Restart |
| -------- | ----------------------- | -------------------------------------------- |
| Yarn     | Yes                    | NodeManager                             |
| Yarn     | Yes                    | NodeManager                             |
| Hive     | Yes                    | HiveServer and HiveMetastore             |
| Spark    | Yes                    | NodeManager                             |
| Sqoop    | Yes                    |  NodeManager                             |
| Presto   | Yes                    | HiveServer, HiveMetastore and Presto |
| Flink    | Yes                    | None                                           |
| Impala   | No                  | None                                          |
| HBase    | Not recommended                  | None                                           |


## Versions

This example uses software versions as follows:

- CDH 5.16.1
- Hadoop 2.6.0


## Directions

### Configuring the storage environment

1. Log in to Cloudera Manager.
2. On the homepage, select **Configuration** > **Service-Wide**  > **Advanced** as shown below:
   ![](https://main.qcloudimg.com/raw/ee096f8e123efd393e1c8a610dd06ff2.png)
3. Specify your COSN settings in the configuration snippet “Cluster-wide Advanced Configuration Snippet (Safety Valve) for core-site.xml”.

```
<property>
<name>fs.cosn.userinfo.secretId</name>
<value>AK***</value>
</property>
<property>
<name>fs.cosn.userinfo.secretKey</name>
<value></value>
</property>
<property>
<name>fs.cosn.impl</name>
<value>org.apache.hadoop.fs.CosFileSystem</value>
</property>
<property>
<name>fs.AbstractFileSystem.cosn.impl</name>
<value>org.apache.hadoop.fs.CosN</value>
</property>
<property>
<name>fs.cosn.bucket.region</name>
<value>ap-shanghai</value>
</property>
```

The following lists the required COSN settings (added to `core-site.xml`). For other COSN settings, see [Hadoop Tool](https://intl.cloud.tencent.com/document/product/436/6884).

| COSN Parameter                     | Value                                 | Description                                                         |
| ------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| fs.cosn.userinfo.secretId       | AKxxxx                             | API the key information of your Tencent Cloud account                                      |
| fs.cosn.userinfo.secretKey      | Wpxxxx                            | API key information of your Tencent Cloud account                                      |
| fs.cosn.bucket.region           | ap-shanghai                        | The region where your COS bucket resides|
| fs.cosn.impl | org.apache.hadoop.fs.CosFileSystem | COSN implementation class for FileSystem; fixed as `org.apache.hadoop.fs.CosFileSystem` |
| fs.AbstractFileSystem.cosn.impl | org.apache.hadoop.fs.CosN          | COSN implementation class for AbstractFileSystem; fixed as org.apache.hadoop.fs.CosN |

4. Take action on your HDFS service by clicking. Now, the core-site.xml settings above will apply to servers in the cluster.
5. Put the latest JAR file in the COSN SDK under the directory that stores all JAR files for CDH HDFS services. The example below is intended for reference purposes only:

```
cp hadoop-cos-2.7.3-shaded.jar /opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/hadoop-hdfs/
```

>!The SDK JAR file needs to be put in the same location on each server in the cluster.


<span id=1>

### Data migration

Use Hadoop Distcp to migrate your data from CDH HDFS to COSN. For details, see [Migrating Data Between HDFS and COS](https://intl.cloud.tencent.com/document/product/436/34076).

### Using COSN for big data modules

#### 1. MapReduce

**Directions**

(1) Configure HDFS settings as instructed in [Data Migration](#1), and put the JAR file from the COSN SDK in the correct HDFS directory.
(2) On the Cloudera Manager homepage, find YARN and restart the NodeManager service (recommended). You can choose not to restart it for the TeraGen command, but must restart it for the TeraSort command because of the internal business logic.

**Examples**

The example below shows TeraGen and TeraSort in Hadoop standard test:

```
hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar teragen  -Dmapred.job.maps=500  -Dfs.cosn.upload.buffer=mapped_disk -Dfs.cosn.upload.buffer.size=-1 1099 cosn://examplebucket-1250000000/terasortv1/1k-input

hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar terasort -Dmapred.max.split.size=134217728 -Dmapred.min.split.size=134217728 -Dfs.cosn.read.ahead.block.size=4194304 -Dfs.cosn.read.ahead.queue.size=32 cosn://examplebucket-1250000000/terasortv1/1k-input  cosn://examplebucket-1250000000/terasortv1/1k-output
```

>?`cosn:// Replace the content behind `schema` with your own bucket path

#### 2. Hive

##### 2.1 MR engine

**Directions**

(1) Configure HDFS settings as instructed in [Data Migration](#1), and put the JAR file of COSN SDK in the correct HDFS directory.
(2) On the Cloudera Manager homepage, find HIVE and restart the Hiveserver2 and HiverMetastore roles.

**Examples**

To query your actual business data, use the Hive command line to create a location as a partitioned table on CHDFS:

```plaintext
CREATE TABLE `report.report_o2o_pid_credit_detail_grant_daily`(
  `cal_dt` string,
  `change_time` string,
  `merchant_id` bigint,
  `store_id` bigint,
  `store_name` string,
  `wid` string,
  `member_id` bigint,
  `meber_card` string,
  `nickname` string,
  `name` string,
  `gender` string,
  `birthday` string,
  `city` string,
  `mobile` string,
  `credit_grant` bigint,
  `change_reason` string,
  `available_point` bigint,
  `date_time` string,
  `channel_type` bigint,
  `point_flow_id` bigint)
PARTITIONED BY (
  `topicdate` string)
ROW FORMAT SERDE
  'org.apache.hadoop.hive.ql.io.orc.OrcSerde'
STORED AS INPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcInputFormat'
    OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat'
LOCATION
  'cosn://examplebucket-1250000000/user/hive/warehouse/report.db/report_o2o_pid_credit_detail_grant_daily'
TBLPROPERTIES (
  'last_modified_by'='work',
  'last_modified_time'='1589310646',
  'transient_lastDdlTime'='1589310646')
```

Perform SQL query:

```
select count(1) from report.report_o2o_pid_credit_detail_grant_daily;
```

The output is as shown below:
![](https://main.qcloudimg.com/raw/28a566e5f08d7cbbeb4893b851565c01.png)

##### 2.2 Tez engine

You need to import the COSN JAR file as part of a Tez tar.gz file. The following example uses apache-tez.0.8.5:

**Directions**

(1) Locate and decompress the Tez tar.gz file installed in the CDH cluster, e.g., /usr/local/service/tez/tez-0.8.5.tar.gz.
(2) Put the COSN JAR file in the resulting directory, and then compress it into a new tar.gz file.
(3) Upload this new file to the path as specified by tez.lib.uris, or simply replace the existing file with the same name.
(4) On the Cloudera Manager homepage, find HIVE and restart hiveserver and hivemetastore.

#### 3. Spark

**Directions**

(1) Configure HDFS settings as instructed in [Data Migration](#1), and put the JAR file of COSN SDK in the correct HDFS directory.
(2) Restart NodeManager.

**Examples**

The following example runs the word count test on Spark examples using COSN:

```
spark-submit  --class org.apache.spark.examples.JavaWordCount --executor-memory 4g --executor-cores 4  ./spark-examples-1.6.0-cdh5.16.1-hadoop2.6.0-cdh5.16.1.jar cosn://examplebucket-1250000000/wordcount
```

The output is as shown below:
![](https://main.qcloudimg.com/raw/90e847c279f948af89ac670e43cd0b31.png)


#### 4. Sqoop

**Directions**

(1) Configure HDFS settings as instructed in [Data Migration](#1), and put the JAR file of COSN SDK in the correct HDFS directory.

(2) Put the JAR file from the COSN SDK under the sqoop directory, for example, `/opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/sqoop/`.

(3) Restart NodeManager.

**Examples**

For example, to export MYSQL tables to COSN, please refer to [Import/Export of Relational Database and HDFS](https://intl.cloud.tencent.com/document/product/1026/31157).

```
sqoop import --connect "jdbc:mysql://IP:PORT/mysql" --table sqoop_test --username root --password 123**  --target-dir cosn://examplebucket-1250000000/sqoop_test
```

The output is as shown below:
![](https://main.qcloudimg.com/raw/4164c207304ba75eb8be42045f7f1394.png)


#### 5. Presto

**Directions**

(1) Configure HDFS settings as instructed in [Data Migration](#1), and put the JAR file of COSN SDK in the correct HDFS directory.
(2) Put the JAR file from the COSN SDK under the presto directory, for example, `/usr/local/services/cos_presto/plugin/hive-hadoop2`.
(3) Presto does not load the gson-2.*.*.jar JAR file (only used for CHDFS), from Hadoop Common, so you need to manually put it inTO the presto directory, for example, `/usr/local/services/cos_presto/ plugin/hive-hadoop2`.
(4) Restart HiveServer, HiveMetaStore, and Presto.

**Examples**

The example below queries the COSN scheme table as a HIVE-created Location:

```
select * from cosn_test_table where bucket is not null limit 1;
```

>?`cosn_test_table` is a table with location as “cosn scheme”.

The output is as shown below:
![](https://main.qcloudimg.com/raw/b83d2aaf490edebbe3d9cc936c5bcce3.png)
