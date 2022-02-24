This document describes how to import data from [HDFS](https://intl.cloud.tencent.com/product/chdfs) to Cloud Data Warehouse.

## Prerequisites
1. Read permissions of HDFS are required for HDFS data access. See Access Control Overview for how to set permissions.
2. The HDFS instance and Cloud Data Warehouse cluster must be in the same VPC.

## Directions
1. Log in to Cloud Data Warehouse and create an HDFS table.
```
CREATE TABLE hdfs_engine_table
(
    `int_id` UInt32
)
ENGINE = ENGINE=HDFS('hdfs://hdfs1:9000/other_storage', 'TSV')
```
<dx-alert infotype="explain" title="Reference">
ENGINE = HDFS(URI, format)
`URI` is the URI of the entire file in HDFS, and `format` specifies an available file format. For more formats, see [Formats for Input and Output Data](https://clickhouse.com/docs/zh/interfaces/formats/#formats). A path URI may contain glob wildcards. In this case, the table will be read-only.
</dx-alert>



2. Create a ClickHouse target table.
	- If your cluster has one replica:
```
CREATE TABLE test.test on cluster default_cluster
(
    `int_id` UInt32
)
engine = MergeTree()
order by int_id;
```
	- If your cluster has two replicas:
```
create table test.test on cluster default_cluster
(
    `int_id` UInt32
)
engine = ReplicatedMergeTree('/clickhouse/tables/test/test/{shard}', '{replica}')
order by int_id;
```
	- Create a distributed table:
```
create table test.test_dis on cluster default
AS test.test
engine = Distributed('default_cluster', 'test', 'test', rand());
```
3. Write data to the target table.
```
INSERT INTO test.test SELECT * FROM hdfs_engine_table;
```
4. Query the data.
```
select * from test.test
```

