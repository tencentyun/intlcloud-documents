## Iceberg Overview
Apache Iceberg is an open-source table format for large-scale data analytics and large, slow-moving tabular data storage. It is designed to improve the de facto standard table layout built into Hive, Trino (PrestoSQL), and Spark. Iceberg helps solve issues caused by the differences between data storage formats in lower layers and provides unified APIs for upper layers, so that different engines can access through the APIs.

Apache Iceberg capabilities:
- Schema evolution: supports five actions—Add, Drop, Update, Rename, and Reorder.
- Partition layout evolution: updates the layout of a table as data volume or query patterns change.
- Hidden partitioning: with this capability, queries no longer depend on a table’s physical layout. Through a separation between physical and logical, Iceberg tables can evolve partition schemes over time as data volume changes. Misconfigured tables can be fixed without an expensive migration.
- Time travel: enables reproducible queries that use exactly the same table snapshot, or lets users easily examine changes.
- Version rollback: allows users to quickly correct problems by resetting tables to a good state.

Iceberg boasts high reliability and performance. It can be used in production where a single table contain tens of petabytes of data and these huge tables can be read even without a distributed SQL engine.
- Fast scan planning: a distributed SQL engine isn’t needed to read a table or find files.
- Advanced filtering: data files are pruned with partition and column-level statistics, based on table metadata.

Iceberg is designed to solve correctness problems in eventually-consistent cloud object stores.
- Works with any cloud store and reduces NameNode congestion in HDFS by avoiding listing and renaming.
- Serializable isolation: table changes are atomic and readers never see partial or uncommitted changes.
- Multiple concurrent writers use optimistic concurrency control and will retry to ensure that compatible updates succeed, even when the writes conflict.

Iceberg is designed to manage data in tables in the form of snapshots. A snapshot is the state of a table at some time. Each snapshot is a complete list of files in a table at some time. Data files are stored across multiple manifest files, and the manifest files are listed in a single manifest list file. Manifest files can be shared among different manifest list files, and a manifest list file represents a snapshot.
- A manifest list file is a metadata file that lists the manifest files. Each manifest file takes up a row.
- A manifest file is a metadata file that lists the data files that make up a snapshot. Each row is a detailed description of each data file, including the file status, file path, partition information, column-level statistics (such as the maximum/minimum values and number of empty values in each column), file size, number of rows, etc.
- A data file is where data is stored. Generally, data files are saved in the `data` directory under the table's data storage directory.

## Examples
For more examples, see [here](https://iceberg.apache.org/getting-started).
1. Log in to the master node and switch to the `hadoop` user.
2. Iceberg packages are saved in `/usr/local/service/iceberg/`.
3. Use a compute engine to query data.
 - Spark engine
    - Spark-SQL interactive command line
```
spark-sql --master local[*] --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions--conf spark.sql.catalog.local=org.apache.iceberg.spark.SparkCatalog--conf spark.sql.catalog.local.type=hadoop --conf spark.sql.catalog.local.warehouse=/usr/hive/warehouse --jars /usr/local/service/iceberg/iceberg-spark3-runtime-0.11.0.jar

```
    - Insert and query data.
```
CREATE TABLE local.default.t1 (id int, name string) USING iceberg;
INSERT INTO local.default.t1 values(1, "tom");
SELECT * from local.default.t1;
```
 - Hive engine
    - Use Beeline.
```
beeline -u jdbc:hive2://[hiveserver2_ip:hiveserver2_port] -n hadoop --hiveconf hive.input.format=org.apache.hadoop.hive.ql.io.HiveInputFormat --hiveconf hive.stats.autogather=false
```
    - Query data.
```
ADD JAR /usr/local/service/hive/lib/iceberg-hive-runtime-0.11.0.jar;
CREATE EXTERNAL TABLE t1 STORED BY 'org.apache.iceberg.mr.hive.HiveIcebergStorageHandler' LOCATION '/usr/hive/warehouse/default/t1';
select count(*) from t1;
```
 - Flink engine
    - Launch a Flink standalone cluster and FLink SQL CMD.
```
wget https://repo1.maven.org/maven2/org/apache/flink/flink-sql-connector-hive-3.1.2_2.11/1.12.1/flink-sql-connector-hive-3.1.2_2.11-1.12.1.jar
/usr/local/service/flink/bin/start-cluster.sh
sql-client.sh embedded -j /usr/local/service/iceberg/iceberg-flink-runtime-0.11.0.jar -j flink-sql-connector-hive-3.1.2_2.11-1.12.1.jar shell
```
    - Query data.
```
CREATE CATALOG hive_catalog WITH ('type'='iceberg','catalog-type'='hive','uri'='hivemetastore_ip:hivemetastore_port','clients'='5','property-version'='1','warehouse'='hdfs:///usr/hive/warehouse/');
CREATE DATABASE hive_catalog.iceberg_db;
CREATE TABLE hive_catalog.iceberg_db.t1 (id BIGINT COMMENT 'unique id',data STRING);
INSERT INTO hive_catalog.iceberg_db.t1 values(1, 'tom');
SELECT count(*) from hive_catalog.iceberg_db.t1;
```

