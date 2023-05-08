## Overview

You can consume a log topic as a Kafka topic over the Kafka protocol. In practice, collected log data can be consumed through the Kafka Consumer or Kafka connectors provided by open-source communities, such as flink-connector-kafka and Kafka-connector-jdbc, to downstream big data components or data warehouses, including Spark, HDFS, Hive, Flink, and Tencent Cloud products like Oceanus and EMR.

This document provides demos for how to consume log topics with Flink and Flume.

## Prerequisites

- You have activated CLS, created a logset and a log topic, and collected log data.   
- Make sure that the current account has the permission to enable **Consumption over Kafka**. For more information, see [Access Policy Templates](https://intl.cloud.tencent.com/document/product/614/45004).


## Use Limits

- Supported Kafka protocol versions: 1.1.1 and earlier.
- Supported compression modes: Snappy and LZ4.
- User authentication mode: SASL_PLAINTEXT.
- You can consume only current but not historical data.
- Data in topics are retained for two hours.




### Consumption over private or public network

- **Consumption over the private network**: A private network domain name is used to consume logs, and the traffic price is 0.032 USD/GB. If your raw log is 100 GB and you choose Snappy for compression, around 50 GB will be billable, and the private network read traffic fees will be 50 GB * 0.032 USD/GB = 1.6 USD. In general, you can consume logs over the private network if your consumer and log topic are in the same VPC or region.
- **Consumption over the public network**: A public network domain name is used to consume logs, and the traffic price is 0.141 USD/GB. If your raw log is 100 GB and you choose Snappy for compression, around 50 GB will be billable, and the public network read traffic fees will be 50 GB * 0.141 USD/GB = 7.05 USD. In general, you need to consume logs over the public network if your consumer and log topic are in different VPCs or regions.

![](https://qcloudimg.tencent-cloud.cn/raw/dc288586793b2229ac2402488213e986.jpg)

[](id:steps)
## Directions


1. Log in to the CLS console and select **[Log Topic](https://console.cloud.tencent.com/cls/topic)** on the left sidebar.
2. On the **Log Topic** page, click the target **Log Topic ID/Name** to enter the log topic management page.
3. On the log topic management page, click the **Consumption over Kafka** tab.
4. Click **Edit** on the right, set **Current Status** to **Enable**, and click **OK**.
5. The console displays the topic and host+port information, which can be copied for constructing the consumer SDK. 



## Consumer Parameter Description

The parameters of the consumer over Kafka are described as follows:

<table>
<thead>
<tr><th style="width: 20%">Parameter</th><th>Description</th></tr>
</thead>
<tbody><tr>
<td>User authentication mode</td>
<td>Currently, only SASL_PLAINTEXT is supported.</td>
</tr>
<tr>
<td>hosts</td>
<td>Consumption over the private network: `kafkaconsumer-${region}.cls.tencentyun.com:9095`.

Consumption over the public network: `kafkaconsumer-${region}.cls.tencentcs.com:9096`. For more information, see <a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a>.</td>
</tr>
<tr>
<td>topic</td>
<td>Topic name provided in the CLS console for consumption over Kafka, which can be copied by clicking the button next to it, such as `XXXXXX-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX`.</td>
</tr>
<tr>
<td>username</td>
<td>Configure it as `${logsetID}`, i.e., logset ID, such as `0f8e4b82-8adb-47b1-XXXX-XXXXXXXXXXXX`. You can copy the logset ID in the log topic list.</td>
</tr>
<tr>
<td>password</td>
<td>Configure it as <code>${SecretId}#${SecretKey}</code>, such as `XXXXXXXXXXXXXX#YYYYYYYY`. Log in to the <a href="https://console.cloud.tencent.com/cam">CAM console</a> and click <b>Access Key</b> on the left sidebar to get the key information. You can use either the API key or project key. We recommend that you use a sub-account key and follow the principle of least privilege when authorizing a sub-account, that is, configure the minimum permission for `action` and `resource` in the access policy of the sub-account.</td>
</tr>
</tbody></table>

>!Be sure not to omit the `;` after the <code>${SecretId}#${SecretKey}</code> of the `jaas.config` in the following sample code; otherwise, an error will be reported.
## SDK for Python

```
import uuid
from kafka import KafkaConsumer,TopicPartition,OffsetAndMetadata
consumer = KafkaConsumer(
#Topic name provided in the CLS console for consumption over Kafka, which can be copied in the console, such as `XXXXXX-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX`.
'Your consumption topic',  
group_id = uuid.uuid4().hex,
auto_offset_reset='earliest',
# Service address + port (9096 for the public network and 9095 for the private network). In this example, consumption is performed over the private network. Enter this field accordingly.
bootstrap_servers = ['kafkaconsumer-${region}.cls.tencentyun.com:9095'],
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',   
# The username is the logset ID, such as `ca5cXXXXdd2e-4ac0af12-92d4b677d2c6`.  
sasl_plain_username = "${logsetID}",
#The password is a string of your `SecretId#SecretKey`, such as `AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac`. Note that `#` is required. We recommend that you use a sub-account key and follow the principle of least privilege when authorizing a sub-account, that is, configure the minimum permission for `action` and `resource` in the access policy of the sub-account.
sasl_plain_password = "${SecretId}#${SecretKey}",
api_version = (1,1,1)
)
print('begin')
for message in consumer:
    print('begins')
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
    print('end')
```

## Consumption of CLS Logs by Oceanus
Create a job in the Oceanus console.


```
CREATE TABLE `nginx_source`
(   # Fields in the log
    `@metadata` STRING,     
    `@timestamp` TIMESTAMP, 
    `agent` STRING,         
    `ecs` STRING,           
    `host` STRING,          
    `input` STRING,         
    `log` STRING,           
    `message` STRING,       
    `partition_id` BIGINT METADATA FROM 'partition' VIRTUAL,    -- Kafka partition
    `ts` TIMESTAMP(3) METADATA FROM 'timestamp'                 
)  WITH (
  'connector' = 'kafka',
  #Topic name provided in the CLS console for consumption over Kafka, which can be copied in the console, such as `XXXXXX-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX`.
  'topic' = 'Your consumption topic',  
  # Service address + port (9096 for the public network and 9095 for the private network). In this example, consumption is performed over the private network. Enter this field accordingly.
  'properties.bootstrap.servers' = 'kafkaconsumer-${region}.cls.tencentyun.com:9095',       
    # Replace it with the name of your consumer group   
  'properties.group.id' = 'The name of your consumer group',  
  'scan.startup.mode' = 'earliest-offset', 
  'format' = 'json',
  'json.fail-on-missing-field' = 'false', 
  'json.ignore-parse-errors' = 'true' ,
  # The username is the logset ID, such as `ca5cXXXXdd2e-4ac0af12-92d4b677d2c6`.
  #The password is a string of your `SecretId#SecretKey`, such as `AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac`. Note that `#` is required. We recommend that you use a sub-account key and follow the principle of least privilege when authorizing a sub-account, that is, configure the minimum permission for `action` and `resource` in the access policy of the sub-account. Be sure not to omit the `;` at the end of the `jaas.config`; otherwise, an error will be reported.
  'properties.sasl.jaas.config' = 'org.apache.kafka.common.security.plain.PlainLoginModule required username="${logsetID}" password="${SecretId}#${SecretKey}";',
  'properties.security.protocol' = 'SASL_PLAINTEXT',
  'properties.sasl.mechanism' = 'PLAIN'
);

```



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

### Registering a Flink table
```sql
CREATE TABLE `nginx_source`
(
    # Fields in the log
    `@metadata` STRING,     
    `@timestamp` TIMESTAMP, 
    `agent` STRING,        
    `ecs` STRING,           
    `host` STRING,          
    `input` STRING,        
    `log` STRING,           
    `message` STRING, 
    # Kafka partition      
    `partition_id` BIGINT METADATA FROM 'partition' VIRTUAL,    
    `ts` TIMESTAMP(3) METADATA FROM 'timestamp'                 
)  WITH (
  'connector' = 'kafka',
  #Topic name provided in the CLS console for consumption over Kafka, which can be copied in the console, such as `XXXXXX-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX`.
  'topic' = 'Your consumption topic',  
  # Service address + port (9096 for the public network and 9095 for the private network). In this example, consumption is performed over the private network. Enter this field accordingly.
  'properties.bootstrap.servers' = 'kafkaconsumer-${region}.cls.tencentyun.com:9095', 
   # Replace it with the name of your consumer group   
  'properties.group.id' = 'The name of your consumer group', 
  'scan.startup.mode' = 'earliest-offset', 
  'format' = 'json',
  'json.fail-on-missing-field' = 'false', 
  'json.ignore-parse-errors' = 'true' ,
  # The username is the logset ID, such as `ca5cXXXXdd2e-4ac0af12-92d4b677d2c6`.
  #The password is a string of your `SecretId#SecretKey`, such as `AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac`. Note that `#` is required. We recommend that you use a sub-account key and follow the principle of least privilege when authorizing a sub-account, that is, configure the minimum permission for `action` and `resource` in the access policy of the sub-account. Be sure not to omit the `;` at the end of the `jaas.config`; otherwise, an error will be reported.
  'properties.sasl.jaas.config' = 'org.apache.kafka.common.security.plain.PlainLoginModule required username="${logsetID}" password="${SecretId}#${SecretKey}";',
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

#Configure the source
a1.sources.source_kafka.type = org.apache.flume.source.kafka.KafkaSource
a1.sources.source_kafka.batchSize = 10
a1.sources.source_kafka.batchDurationMillis = 200000
# Service address + port (9096 for the public network and 9095 for the private network). In this example, consumption is performed over the private network. Enter this field accordingly.
a1.sources.source_kafka.kafka.bootstrap.servers = $kafkaconsumer-${region}.cls.tencentyun.com:9095
#Topic name provided in the CLS console for consumption over Kafka, which can be copied in the console, such as `XXXXXX-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX`.
a1.sources.source_kafka.kafka.topics = Your consumption topic  
#Replace it with the name of your consumer group
a1.sources.source_kafka.kafka.consumer.group.id = The name of your consumer group
a1.sources.source_kafka.kafka.consumer.auto.offset.reset = earliest
a1.sources.source_kafka.kafka.consumer.security.protocol = SASL_PLAINTEXT
a1.sources.source_kafka.kafka.consumer.sasl.mechanism = PLAIN
# The username is the logset ID, such as `ca5cXXXXdd2e-4ac0af12-92d4b677d2c6`.
#The password is a string of your `SecretId#SecretKey`, such as `AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac`. Note that `#` is required. We recommend that you use a sub-account key and follow the principle of least privilege when authorizing a sub-account, that is, configure the minimum permission for `action` and `resource` in the access policy of the sub-account. Be sure not to omit the `;` at the end of the `jaas.config`; otherwise, an error will be reported.
a1.sources.source_kafka.kafka.consumer.sasl.jaas.config = org.apache.kafka.common.security.plain.PlainLoginModule required username="${logsetID}" 
password="${SecretId}#${SecretKey}";



// Configure the sink
a1.sinks.sink_local.type = logger

a1.channels.channel1.type = memory
a1.channels.channel1.capacity = 1000
a1.channels.channel1.transactionCapacity = 100

// Bind the source and sink to the channel
a1.sources.source_kafka.channels = channel1
a1.sinks.sink_local.channel = channel1
```
