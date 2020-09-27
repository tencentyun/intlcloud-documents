Apache Hudi provides the following streaming primitives over datasets on HDFS: upsert and incremental pull.

In general, we will store large amounts of data in HDFS and incrementally write new data but seldom change old data, particularly in scenarios where data is cleansed and placed in a data warehouse. In data warehouses such as Hive, the support for updates is very limited, and computing is expensive. In addition, in scenarios where only data that is added over a certain period of time needs to be analyzed, as Hive, Presto, and HBase do not provide native methods, it is necessary to filter and analyze it based on timestamp.

In view of this, Hudi enables you to update records and only query incremental data. In addition, it supports Hive, Presto, and Spark, so that you can directly use these components to query data managed by Hudi.

Hudi is a universal big data storage system that enables:
- Snapshot isolation between ingestion and query engines, including Apache Hive, Presto, and Apache Spark.
- Support for rollbacks and savepoints to recover datasets.
- Auto-management of file sizes and layout to optimize query performance and near real-time ingestion to feed queries with fresh data.
- Async compaction of both real-time and columnar data.

## Timeline

At its core, Hudi maintains a **timeline** of all actions performed on the dataset at different **instants of time** that helps provide instantaneous views of the dataset.

A Hudi instant consists of the following components:
- Action type: type of action performed on the dataset.
- Instant time: typically a timestamp (such as 20190117010349), which monotonically increases in the order of action start time.
- State: current state of the instant.

## File Organization

Hudi organizes datasets on DFS into a directory structure under a `basepath`. A dataset is broken down into partitions, which are folders containing data files for the corresponding partitions, very similar to Hive tables.

Each partition is uniquely identified by its `partitionpath`, which is relative to the `basepath`.

Within each partition, files are organized into `file groups` uniquely identified by `file ID`.

Each file group contains several `file slices`, where each slice contains a base columnar file (`*.parquet`) produced at a certain commit/compaction instant time, along with a set of log files (`*.log*`) that contain inserts/updates to the base file since the base file was produced.

 Hudi adopts an MVCC design, where compaction action merges logs and base files to produce new file slices and cleaning action gets rid of unused/older file slices to reclaim space on DFS.

Hudi provides efficient upserts by mapping a given hoodie key (record key + partition path) to a file group through an indexing mechanism.

This mapping between record key and `file group`/`file id` never changes once the first version of a record has been written to a file. In short, the mapped file group contains all versions of a group of records.

## Storage Types

Hudi supports the following storage types:
- Copy on write: it stores data only in columnar file formats (e.g., parquet), updates version, and rewrites the files by performing a sync merge during write.
- Merge on read: it stores data by using a combination of columnar (e.g., parquet) and row-based (e.g., avro) file formats. Updates are logged to incremental files and later compacted to produce new versions of columnar files synchronously or asynchronously.

The following table summarizes the trade-offs between these two storage types:

| **Trade-Off** | **Copy on Write** | **Merge on Read** |
| --------------- | --------------------------- | ---------------------- |
| Data latency | Higher | Lower |
| Update cost (I/O) | Higher (rewriting entire parquet) | Lower (appending to incremental log) |
| Parquet file size | Smaller (high update cost (I/O)) | Larger (low update cost) |
| Write amplification | Higher | Lower (depending on compaction policy) |


## Hudi Support for EMR Underlying Storage

- HDFS
- COS

## Installing Hudi
Enter the [EMR purchase page](https://buy.cloud.tencent.com/emapreduce?regionId=1#/) and select EMR v2.2.0 as the **Product Version** and **Hudi 0.5.1** as the **Optional Component**. Hudi is installed on the master and router nodes by default.
> Hudi relies on Hive and Spark components. If you choose to install Hudi, EMR will automatically install Hive and Spark.

## Use Cases
For more information, please see [Hudi official demo](http://hudi.apache.org/docs/docker_demo.html):
1. Log in to a master node and switch to the `hadoop` user.
2. Load the Spark configuration.
```
cd /usr/local/service/hudi
ln -s /usr/local/service/spark/conf/spark-defaults.conf /usr/local/service/hudi/demo/config/spark-defaults.conf 
```
Upload the configuration to HDFS:
```
hdfs dfs -mkdir -p /hudi/config
hdfs dfs -copyFromLocal demo/config/* /hudi/config/
```
3.	Modify the Kafka data source.
```
/usr/local/service/hudi/demo/config/kafka-source.properties
bootstrap.servers=kafka_ip:kafka_port
```
Upload the first batch of data:
```
cat demo/data/batch_1.json | kafkacat -b [kafka_ip] -t stock_ticks -P
```
4.	Ingest the first batch of data.
```
spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar   --table-type COPY_ON_WRITE --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path /usr/hive/warehouse/stock_ticks_cow --target-table stock_ticks_cow --props /hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider
spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer  --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar  --table-type MERGE_ON_READ --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path /usr/hive/warehouse/stock_ticks_mor --target-table stock_ticks_mor --props /hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider --disable-compaction
```
5.	View HDFS data.
```
 hdfs dfs -ls /usr/hive/warehouse/
```
6.	Sync Hive metadata.
```
bin/run_sync_tool.sh  --jdbc-url jdbc:hive2://[hiveserver2_ip:hiveserver2_port]  --user hadoop --pass [password] --partitioned-by dt --base-path /usr/hive/warehouse/stock_ticks_cow --database default --table stock_ticks_cow
bin/run_sync_tool.sh  --jdbc-url jdbc:hive2://[hiveserver2_ip:hiveserver2_port]   --user hadoop --pass [password]--partitioned-by dt --base-path /usr/hive/warehouse/stock_ticks_mor --database default --table stock_ticks_mor --skip-ro-suffix
```
7.	Query data with a computing engine.
 - Hive engine
```
beeline -u jdbc:hive2://[hiveserver2_ip:hiveserver2_port] -n hadoop --hiveconf hive.input.format=org.apache.hadoop.hive.ql.io.HiveInputFormat --hiveconf hive.stats.autogather=false
```
Or Spark engine
```
spark-sql --master yarn --conf spark.sql.hive.convertMetastoreParquet=false
```
In the Hive/Spark engine, execute the following SQL statement:
```
select symbol, max(ts) from stock_ticks_cow group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_cow where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_mor where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor_rt group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_mor_rt where  symbol = 'GOOG';
```
 - Enter the Presto engine
```
/usr/local/service/presto-client/presto --server localhost:9000 --catalog hive --schema default --user Hadoop
```
**You need to enclose a field with underlines in double quotation marks to query it with Presto**, such as `"_hoodie_commit_time"`. Execute the following SQL statement:
```
select symbol, max(ts) from stock_ticks_cow group by symbol HAVING symbol = 'GOOG';
select "_hoodie_commit_time", symbol, ts, volume, open, close  from stock_ticks_cow where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor group by symbol HAVING symbol = 'GOOG';
select "_hoodie_commit_time", symbol, ts, volume, open, close  from stock_ticks_mor where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor_rt group by symbol HAVING symbol = 'GOOG';
```
8. Upload the second batch of data.
```
cat demo/data/batch_2.json | kafkacat -b 10.0.1.70 -t stock_ticks -P
```
9. Ingest the second batch of incremental data.
```
spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar   --table-type COPY_ON_WRITE --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path /usr/hive/warehouse/stock_ticks_cow --target-table stock_ticks_cow --props /hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider
spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer  --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar  --table-type MERGE_ON_READ --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path /usr/hive/warehouse/stock_ticks_mor --target-table stock_ticks_mor --props /hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider --disable-compaction
```
10.	Query incremental data by following step 7.
11.	Use the hudi-cli tool.
```
 cli/bin/hudi-cli.sh
connect --path /usr/hive/warehouse/stock_ticks_mor
compactions show all
compaction schedule
Combine the execution plans
 compaction run --compactionInstant [requestID] --parallelism 2 --sparkMemory 1G  --schemaFilePath /hudi/config/schema.avsc --retry 1
```
12.	Query data with the Spark/Tez engine.
```
beeline -u jdbc:hive2://[hiveserver2_ip:hiveserver2_port] -n hadoop --hiveconf hive.input.format=org.apache.hadoop.hive.ql.io.HiveInputFormat --hiveconf hive.stats.autogather=false
set hive.execution.engine=tez;
set hive.execution.engine=spark;
```
Then, execute an SQL query by following step 7.


## Working with COS

Like HDFS, you need to add `cosn://[bucket]` before the storage path. Please see the following steps:
```
bin/kafka-server-start.sh config/server.properties &
cat     demo/data/batch_1.json | kafkacat -b kafkaip -t stock_ticks -P
cat     demo/data/batch_2.json | kafkacat -b kafkaip -t stock_ticks -P
kafkacat -b kafkaip  -L
hdfs dfs -mkdir -p cosn://[bucket]/hudi/config
hdfs dfs -copyFromLocal demo/config/*  cosn://[bucket]/hudi/config/


spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar   --table-type COPY_ON_WRITE --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path cosn://[bucket]/usr/hive/warehouse/stock_ticks_cow --target-table stock_ticks_cow --props cosn://[bucket]/hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider


spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer  --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar  --table-type MERGE_ON_READ --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path cosn://[bucket]/usr/hive/warehouse/stock_ticks_mor --target-table stock_ticks_mor --props cosn://[bucket]/hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider --disable-compaction


bin/run_sync_tool.sh  --jdbc-url jdbc:hive2://[hiveserver2_ip:hiveserver2_port] --user hadoop --pass isd@cloud --partitioned-by dt --base-path cosn://[bucket]/usr/hive/warehouse/stock_ticks_cow --database default --table stock_ticks_cow

bin/run_sync_tool.sh  --jdbc-url jdbc:hive2://[hiveserver2_ip:hiveserver2_port] --user hadoop --pass hive --partitioned-by dt --base-path cosn://[bucket]/usr/hive/warehouse/stock_ticks_mor --database default --table stock_ticks_mor --skip-ro-suffix


beeline -u jdbc:hive2://[hiveserver2_ip:hiveserver2_port] -n hadoop --hiveconf hive.input.format=org.apache.hadoop.hive.ql.io.HiveInputFormat --hiveconf hive.stats.autogather=false

spark-sql --master yarn --conf spark.sql.hive.convertMetastoreParquet=false


hivesqls:
select symbol, max(ts) from stock_ticks_cow group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_cow where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_mor where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor_rt group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_mor_rt where  symbol = 'GOOG';

prestosqls:
/usr/local/service/presto-client/presto --server localhost:9000 --catalog hive --schema default --user Hadoop
select symbol, max(ts) from stock_ticks_cow group by symbol HAVING symbol = 'GOOG';
select "_hoodie_commit_time", symbol, ts, volume, open, close  from stock_ticks_cow where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor group by symbol HAVING symbol = 'GOOG';
select "_hoodie_commit_time", symbol, ts, volume, open, close  from stock_ticks_mor where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor_rt group by symbol HAVING symbol = 'GOOG';
select "_hoodie_commit_time", symbol, ts, volume, open, close  from stock_ticks_mor_rt where  symbol = 'GOOG';


cli/bin/hudi-cli.sh
connect --path cosn://[bucket]/usr/hive/warehouse/stock_ticks_mor
compactions show all
compaction schedule
compaction run --compactionInstant [requestid]  --parallelism 2 --sparkMemory 1G  --schemaFilePath cosn://[bucket]/hudi/config/schema.avsc --retry 1
```


