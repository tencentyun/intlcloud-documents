Apache Hudi provides streaming primitives over HDFS datasets for upsert and incremental pull.

In most cases, we store a large amount of data in HDFS. As new data is incrementally written to the storage, old data is rarely changed, especially if the data is cleansed and stored in, for example, a Hive warehouse. Limited support is provided for updates and the computing costs are high. Further, tools like Hive, Presto, and HBase cannot natively analyze the new data written in a specific period of time. Instead, the data is filtered based on the timestamp before the analysis.

Hudi is a solution to those issues because it supports record-level updates and incremental queries. You can use Apache Hive, Presto, and Spark to directly query the data managed by Hudi.

As a general-purpose big data storage system, Hudi provides the following key features:
- Ingests snapshots from query engines, such as Hive, Presto, and Spark.
- Supports rollback and savepoint for dataset recovery.
- Automatically manages file sizes and layouts to optimize query performance and provide near-real-time data for queries.
- Asynchronously compresses real-time data and column data.

## Timeline
At its core, Hudi maintains a **timeline** of all actions performed on the dataset at different **instants** of time. Therefore, Hudi provides views of the dataset at different points in time.

A Hudi instant consists of the following components:
- Instant action: The type of action performed on the dataset.
- Instant time: Instant time is a timestamp, such as 20190117010349, which monotonically increases in the order of the start time of actions.
- State: The state of the instant.

## File Layout
Hudi organizes a dataset on DFS into a directory structure under a `base path`. The dataset is divided into partitions, which are folders containing data files for that partition. This is much like a Hive table.

Each partition is identified by a specific `partition path`, which is relative to the base path. In each partition, files are organized into file groups, which are uniquely identified by file IDs. Each file group contains multiple file slices. Each file slice contains a base file `*.parquet`, which is a columnar file generated at a certain commit or compaction instant time, and a set of `*.log*` files that contain upserts to the base file since it was generated.

Hudi works on the Multi-Version Concurrency Control (MVCC) mechanism. Logs and base files are compacted to produce new file slices, and unused and older file slices are cleared to reclaim space on DFS. Hudi provides efficient upserts by mapping a given hoodie key (record key + partition path) to a file group through an indexing mechanism.

Once the first version of a record is written to a file, the mapping between the record key and the file group or file ID never changes. In other words, a mapped file group contains all versions of a group of records.

## Storage Types
Hudi supports the following storage types:
- Copy on Write: Data is stored only in a columnar file format, such as Parquet. The version is updated and the file rewritten by performing a synchronous merge during the data write.
- Merge on Read: Data is stored in both columnar (such as Parquet) and row-based (such as Avro) file formats. Updates are recorded in incremental files, which are synchronously or asynchronously compacted to produce new versions of columnar files.

The following table summarizes the trade-offs between these two storage types:

| **Trade-Off**        | **Copy on Write**                | **Merge on Read**           |
| --------------- | --------------------------- | ---------------------- |
| Data latency        | Higher                        | Lower                   |
| Update cost (I/O) | Higher (rewrite the entire Parquet file) | Lower (append to incremental logs) |
| Parquet file size | Smaller (high update (I/O)) | Larger (low update cost)     |
| Write amplification          | Higher                        | Lower (depending on compaction strategies) |

## EMR Underlying Storage Supported by Hudi
- HDFS
- COS

## Installing Hudi
Go to the [EMR purchase page](https://buy.cloud.tencent.com/emr), select **EMR-V2.2.0** for **Product Version**, and select the **hudi 0.5.1** optional component. By default, Hudi is installed on the master and router nodes.
>! Hudi relies on Hive and Spark. If you install Hudi, EMR automatically installs Hive and Spark.

## Examples
The following examples are applicable to Hudi 0.11.0 and later. For more information about examples applicable to other versions, see the [Docker Demo](http://hudi.apache.org/docs/docker_demo.html) on Hudi’s official website.
1. Log in to the master node and switch to the `hadoop` user.
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
3. Modify the Kafka data source.
```
/usr/local/service/hudi/demo/config/kafka-source.properties
bootstrap.servers=kafka_ip:kafka_port
```
Upload the first batch of data:
```
cat demo/data/batch_1.json | kafkacat -b [kafka_ip] -t stock_ticks -P
```
4. Ingest the first batch of data.
```
spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar   --table-type COPY_ON_WRITE --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path /usr/hive/warehouse/stock_ticks_cow --target-table stock_ticks_cow --props /hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider
spark-submit --class org.apache.hudi.utilities.deltastreamer.HoodieDeltaStreamer  --master yarn ./hudi-utilities-bundle_2.11-0.5.1-incubating.jar  --table-type MERGE_ON_READ --source-class org.apache.hudi.utilities.sources.JsonKafkaSource --source-ordering-field ts  --target-base-path /usr/hive/warehouse/stock_ticks_mor --target-table stock_ticks_mor --props /hudi/config/kafka-source.properties --schemaprovider-class org.apache.hudi.utilities.schema.FilebasedSchemaProvider --disable-compaction
```
5. View the HDFS data.
```
 hdfs dfs -ls /usr/hive/warehouse/
```
6. Synchronize the Hive metadata.
```
bin/run_sync_tool.sh  --jdbc-url jdbc:hive2://[hiveserver2_ip:hiveserver2_port]  --user hadoop --pass [password] --partitioned-by dt --base-path /usr/hive/warehouse/stock_ticks_cow --database default --table stock_ticks_cow
bin/run_sync_tool.sh  --jdbc-url jdbc:hive2://[hiveserver2_ip:hiveserver2_port]   --user hadoop --pass [password]--partitioned-by dt --base-path /usr/hive/warehouse/stock_ticks_mor --database default --table stock_ticks_mor --skip-ro-suffix
```
7. Use a compute engine to query data.
 - Hive engine
```
beeline -u jdbc:hive2://[hiveserver2_ip:hiveserver2_port] -n hadoop --hiveconf hive.input.format=org.apache.hadoop.hive.ql.io.HiveInputFormat --hiveconf hive.stats.autogather=false
```
Or Spark engine
```
spark-sql --master yarn --conf spark.sql.hive.convertMetastoreParquet=false
```
Execute the following SQL statements in the Hive or Spark engine:
```
select symbol, max(ts) from stock_ticks_cow group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_cow where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_mor where  symbol = 'GOOG';
select symbol, max(ts) from stock_ticks_mor_rt group by symbol HAVING symbol = 'GOOG';
select `_hoodie_commit_time`, symbol, ts, volume, open, close  from stock_ticks_mor_rt where  symbol = 'GOOG';
```
 - Presto engine
```
/usr/local/service/presto-client/presto --server localhost:9000 --catalog hive --schema default --user Hadoop
```
**To query a field with underscores (_) in the Presto engine, you must enclose the field with double quotation marks(" ")**. Example: `"_hoodie_commit_time"`. Execute the following SQL statements:
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
10. Query the incremental data. The query method is the same as step 7.
11. Use the hudi-cli tool.
```
 cli/bin/hudi-cli.sh
connect --path /usr/hive/warehouse/stock_ticks_mor
compactions show all
compaction schedule
Compact execution plans.
 compaction run --compactionInstant [requestID] --parallelism 2 --sparkMemory 1G  --schemaFilePath /hudi/config/schema.avsc --retry 1
```
12. Specify Tez or Spark as the query engine.
```
beeline -u jdbc:hive2://[hiveserver2_ip:hiveserver2_port] -n hadoop --hiveconf hive.input.format=org.apache.hadoop.hive.ql.io.HiveInputFormat --hiveconf hive.stats.autogather=false
set hive.execution.engine=tez;
set hive.execution.engine=spark;
```
Execute the SQL query. For more information about the query method, see step 7.

## Using Hudi with COS
Like HDFS, when using Hudi with COS, you must add `cosn://[bucket]` before the storage path. Example:
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


