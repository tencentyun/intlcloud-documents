This document describes how to consume data from [Kafka](https://intl.cloud.tencent.com/product/ckafka) to Cloud Data Warehouse in real time.

## Prerequisites
The Kafka data source cluster and the target Cloud Data Warehouse cluster must be in the same VPC.

## Directions
1. Log in to the [Cloud Data Warehouse](https://intl.cloud.tencent.com/document/product/1129/44393) cluster and create a Kafka consumption table.
```
	CREATE TABLE queue (
			timestamp UInt64,
			level String,
			message String
	) ENGINE = Kafka
	SETTINGS
					kafka_broker_list = 'localhost:9092',
					kafka_topic_list = 'topic',
					kafka_group_name = 'group',
					kafka_format = 'JSONEachRow',
					kafka_num_consumers = 1,
					kafka_max_block_size = 65536,
					kafka_skip_broken_messages = 0,
					kafka_auto_offset_reset = 'latest';
```

**The common parameters are described as follows:**

<table>
<thread>
<tr>
<th >Name</th>
<th >Required</th>
<th >Description</th>
</tr>
</thread>
<tbody>
<tr>
<td >kafka_broker_list</td>
<td >Yes</td>
<td >A list of Kafka service brokers separated by commas. We recommend you use `Ip:port` instead of domain name to avoid possible DNS resolution issues.</td>
</tr>
<tr>
<td >kafka_topic_list</td>
<td >Yes</td>
<td >Kafka topics separated by commas</td>
</tr><tr>
<td >kafka_group_name</td>
<td >Yes</td>
<td >Kafka consumption group name</td>
</tr><tr>
<td >kafka_format</td>
<td >Yes</td>
<td >Kafka data format. For information on ClickHouse-supported formats, see the parameters in <a href="https://clickhouse.com/docs/en/interfaces/formats/">Formats for Input and Output Data</a>.</td>
</tr><tr>
<td >kafka_row_delimiter</td>
<td >No</td>
<td >Row delimiter used to split data rows. The default value is `\n`, but you can also set it to another value according to the actual segmentation format during data write.</td>
</tr>
<tr>
<td >kafka_num_consumers</td>
<td >No</td>
<td >Number of consumers for a single Kafka engine. You can increase the consumption data throughput by increasing this parameter value, but it cannot exceed the total number of partitions in the corresponding topic.</td>
</tr>
<tr>
<td >kafka_max_block_size</td>
<td >No</td>
<td >Block size of the target table to which Kafka data is written. It is 65536 bytes by default. If the data size exceeds this value, the data will be flushed.</td>
</tr>
<tr>
<td >kafka_skip_broken_messages</td>
<td >No</td>
<td >Number of data records with parsing exceptions that can be ignored. If the number of exceptions exceeds the specified value (`N`), the backend thread will stop. The default value is 0.</td>
</tr><tr>
<td >kafka_commit_every_batch</td>
<td >No</td>
<td >Frequency of Kafka commit execution.<br>0: commits only after the data of an entire block is written.<br>1: commits after the data of each batch is written.</td>
</tr><tr>
<td >kafka_auto_offset_reset</td>
<td >No</td>
<td >The offset from which to read Kafka data. Its value can be `earliest` or `latest`.</td>
</tr>
</tbody>
</table>

2. Create a ClickHouse local table (target table).

 - If your cluster has one replica:
```
CREATE TABLE daily on cluster default_cluster
(
    day Date,
    level String,
    total UInt64
)
engine = SummingMergeTree()
order by int_id;
```
 - If your cluster has two replicas:
```
create table daily on cluster default_cluster
(
    day Date,
    level String,
    total UInt64
)
engine = ReplicatedSummingMergeTree('/clickhouse/tables/test/test/{shard}', '{replica}')
order by int_id;`
```
 - Create a distributed table:
```
create table daily_dis on cluster default_cluster
AS test.test
engine = Distributed('default_cluster', 'default', 'daily', rand());
```

3. Create a materialized view to sync data consumed by the Kafka consumption table to the ClickHouse target table.
```
CREATE MATERIALIZED VIEW consumer TO daily
AS SELECT toDate(toDateTime(timestamp)) AS day, level, count() as total
FROM queue GROUP BY day, level;
```

4. Query the data.
```
SELECT level, sum(total) FROM daily GROUP BY level;
```

## Notes
If you want to stop receiving topic data or change the conversion logic, perform `detach` and `attach` view operations.
```
  DETACH TABLE consumer;
  ATTACH TABLE consumer;
```
