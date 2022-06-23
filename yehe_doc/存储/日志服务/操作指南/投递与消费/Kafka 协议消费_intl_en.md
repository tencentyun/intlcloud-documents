## Overview
You can consume the data collected by CLS to downstream big data components or data warehouses over the Kafka protocol, such as Kafka, HDFS, Hive, and Flink, as well as Tencent Cloud products such as Oceanus and EMR.   

This document provides demos for how to consume log topics with Flink and Logstash.


### Supported Kafka protocol versions
Kafka v1.1.1 and earlier

### Consumption over private or public network
- Definitions of consumption over the private network and consumption over the private network: For example, if your log topics in Guangzhou region use the Kafka consumption protocol, then consumption to Oceanus in Guangzhou is regarded as over the private network, while consumption to Oceanus in Shanghai is regarded as over the public network.
- Billing differences: The private network traffic is priced at 0.18 CNY/GB, while the public network traffic is priced at 0.8 CNY/GB.
- Consumption service domain name differences: The private and public network service domain names are as listed in the console for your choice as needed.

## Prerequisites
- You have activated CLS, created a logset and a log topic, and collected log data.   
- Make sure that the current account has the permission to enable **Consumption over Kafka**. For more information, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).


## Directions[](id:steps)

1. Log in to the CLS console and select **[Log Topic](https://console.cloud.tencent.com/cls/topic)** on the left sidebar.
3. On the **Log Topic** page, click the target **Log Topic ID/Name** to enter the log topic management page.
4. On the log topic management page, click the **Consumption over Kafka** tab.
5. Click **Edit** on the right, set **Current Status** to **Enable**, and click **OK**.
6. Construct the consumer according to the topic information given by CLS as shown below:



## Consumption of CLS Log by Flink

### Enabling log consumption over Kafka
Enable log consumption over Kafka and get the consumer service domain name and topic as instructed in [Directions](#steps).


### Confirming flink-connector-kafka dependency 
After confirming that `flink-connector-kafka` exists in `flink lib`, directly register a Kafka table in `sql`. The dependency is as follows:
```xml
<dependency>
  <groupId>org.apache.flink</groupId>
  <artifactId>flink-connector-kafka</artifactId>
  <version>1.14.4</version>
</dependency>
```

### Registering Flink table
```sql
CREATE TABLE `nginx_source`
(
    `@metadata` STRING,     -- Field in the log
    `@timestamp` TIMESTAMP, -- Field in the log
    `agent` STRING,         -- Field in the log
    `ecs` STRING,           -- Field in the log
    `host` STRING,          -- Field in the log
    `input` STRING,         -- Field in the log
    `log` STRING,           -- Field in the log
    `message` STRING,       -- Field in the log
    `partition_id` BIGINT METADATA FROM 'partition' VIRTUAL,    -- Kafka partition
    `ts` TIMESTAMP(3) METADATA FROM 'timestamp'                 
)  WITH (
  'connector' = 'kafka',
  'topic' = 'YourTopic',  -- Topic name provided in the CLS console for consumption over Kafka, such as `out-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX` 
  'properties.bootstrap.servers' = 'kafkaconsumer-ap-guangzhou.cls.tencentcs.com:9096',   -- Service address provided in the CLS console for consumption over Kafka. The public network consumer address in Guangzhou region is used as an example. You need to enter the actual information.
  'properties.group.id' = 'kafka_flink', -- Kafka consumer group name
  'scan.startup.mode' = 'earliest-offset', 
  'format' = 'json',
  'json.fail-on-missing-field' = 'false', 
  'json.ignore-parse-errors' = 'true' ,
  'properties.sasl.jaas.config' = 'org.apache.kafka.common.security.plain.PlainLoginModule required username="your username" password="your password";',-- The username is the logset ID of the log topic, such as `ca5cXXXX-dd2e-4ac0-af12-92d4b677d2c6`, and the password is a string of your secretid#secrectkey, such as `AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac`. Do not omit the #.
  'properties.security.protocol' = 'SASL_PLAINTEXT',
  'properties.sasl.mechanism' = 'PLAIN'
);
```

### Querying
After successful execution, you can use the statement for query.
```sql
select count(*) , host from nginx_source group by host;
```

## Consumption of CLS Log by Flume
If you need to have log data consumed by a self-built HDFS or Kafka cluster, you can use the Flume component for forwarding as instructed below.


### Enabling log consumption over Kafka
Enable log consumption over Kafka and get the consumer service domain name and topic as instructed in [Directions](#steps).

### Flume configuration

```
a1.sources = source_kafka
a1.sinks = sink_local
a1.channels = channel1

// Configure the source
a1.sources.source_kafka.type = org.apache.flume.source.kafka.KafkaSource
a1.sources.source_kafka.batchSize = 10
a1.sources.source_kafka.batchDurationMillis = 200000
a1.sources.source_kafka.kafka.bootstrap.servers = kafkaconsumer-ap-guangzhou.cls.tencentcs.com:9096 -- Service address provided in the CLS console for consumption over Kafka. The public network consumer address in Guangzhou region is used as an example. You need to enter the actual information.
a1.sources.source_kafka.kafka.topics = YourClsTopic -- Topic name provided in the CLS console for consumption over Kafka, such as `out-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX` 
a1.sources.source_kafka.kafka.consumer.group.id = cls_flume_kafka
a1.sources.source_kafka.kafka.consumer.auto.offset.reset = earliest
a1.sources.source_kafka.kafka.consumer.security.protocol = SASL_PLAINTEXT
a1.sources.source_kafka.kafka.consumer.sasl.mechanism = PLAIN
a1.sources.source_kafka.kafka.consumer.sasl.jaas.config = org.apache.kafka.common.security.plain.PlainLoginModule required username="YourUsername" 
password="YourPassword";-- The username is the logset ID of the log topic, such as `ca5cXXXX-dd2e-4ac0-af12-92d4b677d2c6`, and the password is a string of your secretid#secrectkey, such as `AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac`. Do not omit the #.



// Configure the sink
a1.sinks.sink_local.type = logger

a1.channels.channel1.type = memory
a1.channels.channel1.capacity = 1000
a1.channels.channel1.transactionCapacity = 100

// Bind the source and sink to the channel
a1.sources.source_kafka.channels = channel1
a1.sinks.sink_local.channel = channel1
```


## SDK for Python
```
import uuid
from kafka import KafkaConsumer,TopicPartition,OffsetAndMetadata
consumer = KafkaConsumer(
// Enter the topic name in the console here for consumption    
'out-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX',  
group_id = uuid.uuid4().hex,
auto_offset_reset='earliest',
// Kafka protocol service address. Enter the service access information in the above figure here. If you consume over the public network, enter
the public network service domain name + port. If over the private network, enter the private network service domain name + port. The example uses the private network service.
bootstrap_servers = ['kafkaconsumer-ap-guangzhou.cls.tencentyun.com:9096'],
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',   
// SASL information. Enter the logset ID of the log topic here.   
sasl_plain_username = "ca5cXXXX-dd2e-4ac0-af12-92d4b677d2c6",
// SASL information. Enter the string of your secretid#secrectkey. Do not omit the #.
sasl_plain_password = "AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac",
api_version = (1,1,1)
)
print('begin')
for message in consumer:
    print('begins')
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
    print('end')
```
