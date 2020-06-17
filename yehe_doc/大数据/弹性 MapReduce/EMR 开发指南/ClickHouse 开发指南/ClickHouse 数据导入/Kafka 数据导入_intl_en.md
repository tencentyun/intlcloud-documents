## Overview
This document describes how to import data in Kafka into a ClickHouse cluster.
>To share your thoughts on ClickHouse, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to join the ClickHouse technical exchange group.

Kafka is a widely used open-source messaging middleware program. It is often used to collect data from all services as the data bus, subscribe to or consume data in diverse downstream data services, and generate various reports or data applications. ClickHouse has a built-in Kafka engine, making integration of ClickHouse with Kafka very easy.
 
The standard process for importing data from Kafka to ClickHouse is as follows:
- Create a Kafka engine external table in ClickHouse as an API of the Kafka data source.
- Create a regular table (generally in the `MergeTree` family) in ClickHouse to store the Kafka data.
- Create a materialized view in ClickHouse to listen on Kafka data and write data to the ClickHouse storage table.

After completing the steps above, you can import data in Kafka into the ClickHouse cluster.

## Importing Data from Kafka to ClickHouse
ClickHouse provides the Kafka engine as an API (data stream) for accessing the Kafka cluster, which can be implemented in the following steps:

- **Step 1.** Create a Kafka engine
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
Required parameters:
 - `kafka_broker_list`: broker list of the Kafka service, in which brokers are separated by commas (,).
 - `kafka_topic_list`: Kafka topic. Multiple topics should be separated by commas (,).
 - `kafka_group_name`: consumer group name.
 - `kafka_format`: Kafka data format. For formats supported by ClickHouse, please see [Formats for Input and Output Data](https://clickhouse.tech/docs/en/interfaces/formats/).

 Optional parameters:
 - `kafka_skip_broken_messages`: number of data entries with parsing exceptions that can be ignored, which is a positive integer or 0. If the number of occurring exceptions exceeds the specified value (`N`), the backend thread will stop, and the materialized view will assign a new backend thread to listen on the data.
 - `kafka_num_consumers`: number of consumers for a single Kafka engine. You can increase the consumption data throughput by increasing this parameter value, but it cannot exceed the total number of partitions in the corresponding topic.
 - `kafka_row_delimiter`: message delimiter.
 - `kafka_schema`: schema for `kafka_format`.
 - `kafka_max_block_size`: size of block in the target table to which data from Kafka will be written. If the data size exceeds this value, the data will be flushed.
- **Step 2.** Create the target table for storing the Kafka data as the final storage
In this document, `MergeTree` is used to store Kafka data:
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
- **Step 3.** Create a materialized view to capture data
This document uses the following statements to create a materialized view:
```
CREATE MATERIALIZED VIEW source_mv TO target AS
SELECT 
    ts, 
    tag
FROM source
```
After completing the three steps above, you can query data from Kafka in the `target` table.

In the data import process above, the materialized view acts as an intermediate pipeline, through which a data stream, e.g., Kafka engine is written to the target table. Actually, a data stream can associate with multiple materialized views to import data from Kafka to multiple different target tables. You can use the `DETACH` statement to dissociate the data stream or use the `ATTACH` statement to associate it with a target table again.
