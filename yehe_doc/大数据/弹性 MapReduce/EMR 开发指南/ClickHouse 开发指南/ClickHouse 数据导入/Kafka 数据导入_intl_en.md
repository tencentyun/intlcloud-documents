## Overview
This article describes how to import data from Kafka into a ClickHouse cluster.
>?For more technical exchanges on ClickHouse, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to us, and we will add you into the ClickHouse technical exchange group.

Kafka is a widely used open source messaging middleware. A common use case of Kafka is to collect data from services as a data bus, including service, subscription, and spending data, and then generate reports or data applications. ClickHouse has a built-in Kafka engine, making it easy to integrate ClickHouse and Kafka.
 
Standard process for importing data from Kafka into ClickHouse:
- Create an external Kafka engine table in ClickHouse as a connector to access the Kafka data source.
- Create a common table in ClickHouse (usually MergeTree family) to store the data from Kafka.
- Create a materialized view in ClickHouse to listen to the data in Kafka and write the data from Kafka to a ClickHouse table.

After completing the above three steps, you can import the data from Kafka to the ClickHouse cluster.

## Importing data from Kafka to ClickHouse
ClickHouse provides a Kafka engine that serves as a connector (or a data stream) to access Kafka clusters. The detailed steps are as shown below:

- **Step 1:** Create an external Kafka engine table
```
CREATE TABLE source
(
    `ts` DateTime, 
    `tag` String, 
    `message` String
)
ENGINE = Kafka()
SETTINGS kafka_broker_list = '172.19.0.47:9092', 
         kafka_topic_list = 'tag',
         kafka_group_name = 'clickhouse', 
         kafka_format = 'JSONEachRow',
         kafka_skip_broken_messages = 1,
         kafka_num_consumers = 2
```
<table>
<tr>
<th>Parameter</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>kafka_broker_list</td>
<td>Yes</td>
<td>Enter Kafka brokers and separate each one with a comma</td>
</tr>
<tr>
<td>kafka_topic_list</td>
<td>Yes</td>
<td>Enter Kafka topics and separate each one with a comma</td>
</tr>
<tr>
<td>kafka_group_name</td>
<td>Yes</td>
<td>Enter the consumer group name</td>
</tr>
<tr>
<td>kafka_format</td>
<td>Yes</td>
<td>Kafka data format. For formats supported by ClickHouse, see <a href="https://clickhouse.tech/docs/en/interfaces/formats/">Formats for Input and Output Data</td>
</tr>
<tr>
<td>kafka_skip_broken_messages</td>
<td>No</td>
<td>Enter an integer greater than or equal to 0, which indicates the number of errors to tolerate when parsing messages. Where N errors occur, background threads end. The materialized view will rearrange background threads to listen to data</td>
</tr>
<tr>
<td>kafka_num_consumers</td>
<td>No</td>
<td>Number of consumers of a single external Kafka engine table. By giving a higher value for this parameter, you can increase the throughput of consumed data, but the number of consumers should not be greater than the number of partitions in the topic</td>
</tr>
<tr>
<td>kafka_row_delimiter</td>
<td>No</td>
<td>Message delimiter</td>
</tr>
<tr>
<td>kafka_schema</td>
<td>No</td>
<td>If kafka_format requires a schema definition, this parameter determines the schema</td>
</tr>
<tr>
<td>kafka_max_block_size</td>
<td>No</td>
<td>This parameter determines the maximum block size allowed for writing Kafka data into the target table. The data will be flushed to the disk if the block size exceeds this value</td>
</tr>
</table>
- **Step 2:** Create a target table to store Kafka data. This table is the destination where the Kafka data will be stored
This article uses MergeTree to store Kafka data:
```
CREATE TABLE target
(
    `ts` DateTime, 
    `tag` String
)
ENGINE = MergeTree()
PARTITION BY toYYYYMM(ts)
ORDER BY tag
```
- **Step 3:** Create a materialized view to capture data
This article uses the following statements to create the materialized view:
```
CREATE MATERIALIZED VIEW source_mv TO target AS
SELECT 
    ts, 
    tag
FROM source
```
After completing the above three steps, you can query the data from Kafka in the target table.

In the above process, the materialized view acts as an intermediate pipeline to write the data streams represented by Kafka engine to the target table. In fact, a data stream can be attached to multiple materialized views to import the data from Kafka to multiple target tables simultaneously. You can also detach a data stream from a table or attach it to a target table.
