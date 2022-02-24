This document describes how to import data from [COS](https://intl.cloud.tencent.com/product/cos) to Cloud Data Warehouse.

## Prerequisites
1. The COS data source and the Cloud Data Warehouse cluster must be in the same VPC.
2. The `access-key-id` and `access-key-secret` entered in the table function must have permission to read the corresponding `oss-file-path`.
3. The `oss-file-path` parameter needs to meet the OSS path format specification, which is `oss://<bucket-name/<path-to-file>` typically.

## Directions
In the following example, data is imported from the S3 system (with COS as an example in this document) to Cloud Data Warehouse.
1. Log in to Cloud Data Warehouse and create an S3 table.
```
CREATE TABLE cos_engine_table
(
    `int_id` UInt32
)
ENGINE = S3('http://clickhouse-xxx.myqcloud.com/clickhouse-xxx/cos/data.csv.gz', 'CSV', 'gzip')
```
 - Sample S3 engine parameters:
The S3 table engine provides integration with the Amazon S3 ecosystem. Its parameter follows the format of `S3(path, [aws_access_key_id, aws_secret_access_key,] format, [compression])`.
	- path: bucket URL with file path. In read-only mode, it supports *, ?, {abc,def}, and {N..M} wildcards, where N and M are digits and 'abc' and 'def' are strings.
	- format: file format.
	- `aws_access_key_id` and `aws_secret_access_key`: permanent credentials of COS account. You can use them to authenticate your request. These parameters are optional. If no credentials are specified, credentials will be read from the configuration file. For more information, see Using S3 to Store Data.
	- compression: compression type. Supported values are `none`, `gzip/gz`, `brotli/br`, `xz/LZMA`, and `zstd/zst`. This parameter is optional. The compression type is automatically detected based on the file extension by default.

2. Create a target table.

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
create table test.test_dis on cluster default_cluster
AS test.test
engine = Distributed('default_cluster', 'test', 'test', rand());
```

3. Write data to the target table.
```
INSERT INTO test.test SELECT * FROM cos_engine_table;
```

4. Query the data.
```
select * from test.test
```
