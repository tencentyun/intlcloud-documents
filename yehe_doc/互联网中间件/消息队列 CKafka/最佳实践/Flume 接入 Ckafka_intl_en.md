## Apache Flume Overview
Apache Flume is a distributed, reliable, and highly available log collection system that supports a wide variety of data sources such as HTTP, log file, JMS, and listening port. It can efficiently collect, aggregate, move, and store massive amounts of log data to a specified storage system like Kafka, distributed file system, and Solr search server.

The structure of Flume is as follows:
![](https://mc.qcloudimg.com/static/img/291cf61049ab4820c10c05c6f0900850/00.png)

Flume uses agents as the smallest independent unit of operation. An agent is a JVM composed of three main components: source, sink, and channel.
![](https://mc.qcloudimg.com/static/img/17244b0d3460b838f7b6764db5497c98/11.png)

## Flume and Kafka 
When you store data in a downstream storage module or a computing module such as HDFS or HBase, a lot of complex factors need to be taken into account, such as the number of concurrent writes, system load, and network delay. As a flexible distributed system, Flume has various APIs and provides customizable pipelines.
In the production process, Kafka can act as a cache when the production and consumption are at different paces. It has a partition structure and uses `append` to append data, which makes it have an excellent throughput. In addition, it has a replication structure, which makes it highly fault-tolerant.
Therefore, Flume and Kafka together can satisfy most requirements in production environments.

## How to Connect to Open-Source Kafka
### Preparations
-	 Download [Apache Flume](http://flume.apache.org/download.html) (v1.6.0 or higher is compatible with Kafka).
-	Download [Kafka](https://kafka.apache.org/downloads) (v0.9.x or higher is required as v0.8 is no longer supported).
- Confirm that Kafka's source and sink components are already in Flume.	

### Connection method
Kafka can be used as source or sink to import or export messages.

**Kafka source**
Configure Kafka as the message source, i.e., pulling data from Kafka into a specified sink as a consumer. The main configuration items are as follows:

| Configuration Item | Description |
| :-------- | :--------|
| channels | Configured channel |
| type	| This must be `org.apache.flume.source.kafka.KafkaSource` |
| kafka.bootstrap.servers	| Kafka broker server |
|kafka.consumer.group.id	| ID of the group as Kafka consumer |
|kafka.topics	| Kafka topic as data source |
|batchSize	| Size of each write into channel |
|batchDurationMillis	 | Maximum time interval between writes |

Sample:
```
tier1.sources.source1.type = org.apache.flume.source.kafka.KafkaSource 
tier1.sources.source1.channels = channel1
tier1.sources.source1.batchSize = 5000
tier1.sources.source1.batchDurationMillis = 2000
tier1.sources.source1.kafka.bootstrap.servers = localhost:9092
tier1.sources.source1.kafka.topics = test1, test2
tier1.sources.source1.kafka.consumer.group.id = custom.g.id
```

**Kafka sink**
Configure Kafka as the message receiver, i.e., pushing data into the Kafka server as a producer for subsequent operations. The main configuration items are as follows:

| Configuration Item | Description |
| :-------- | :--------|
| channel | Configured channel |
| type	| This must be `org.apache.flume.sink.kafka.KafkaSink` |
| kafka.bootstrap.servers	| Kafka broker server |
|kafka.topics	| Kafka topic as data source |
|kafka.flumeBatchSize	| Size of each written batch |
|kafka.producer.acks	 | 	Production policy of Kafka producer |

Sample:
```
a1.sinks.k1.channel = c1
a1.sinks.k1.type = org.apache.flume.sink.kafka.KafkaSink
a1.sinks.k1.kafka.topic = mytopic
a1.sinks.k1.kafka.bootstrap.servers = localhost:9092
a1.sinks.k1.kafka.flumeBatchSize = 20
a1.sinks.k1.kafka.producer.acks = 1
```
For more information, please visit [Apache Flume's official website](https://flume.apache.org/FlumeUserGuide.html).


## Flume Connection to CKafka
### Preparations
- In the CKafka Console, [create an instance](https://intl.cloud.tencent.com/document/product/597/39718).
- Download [Apache Flume](http://flume.apache.org/download.html). Flume 1.7.0 is used in this document. 

### CKafka configuration
1. In the **[CKafka Console](https://console.cloud.tencent.com/ckafka?rid=1)**, click the instance name to view the specific information assigned to the instance.
>The private IP and port in the figure serve as the subsequent server IP.
2. Click **Topic Management** > **Create** to create a topic named `flume_test`.

### Flume configuration
#### 1. Decompress the downloaded Apache Flume package
#### 2. Configure Flume options
 **Use CKafka as a sink**
 1. Write a configuration file.
The combination of Flume and CKafka as a sink is focused on here, while the source and channel use the default configuration. Below is a simple demo (configured in the `conf` folder in the extracted directory). If there is no special requirement, simply replace your own instance IP and topic in the configuration file. The source used in this example is `tail -F flume-test`, which represents the information newly added in the file.
 2. Start Flume.
```
./bin/flume-ng agent -n agentckafka -c conf -f conf/flume-kafka-sink.properties
```
 3. Write messages to the `flume-test` file. At this time, the messages will be written by Flume to CKafka.
![](https://mc.qcloudimg.com/static/img/c9dc1f539e00f21fca1ead546f4e007e/66.png)
 4. Start the CKafka client for consumption.
```
./kafka-console-consumer.sh --bootstrap-server 172.16.16.12:9092 --topic flume_test --from-beginning --new-consumer
```
You can see that the messages have been consumed.
 ![](https://mc.qcloudimg.com/static/img/ee394af9d8280bfef988d71ccc30f805/77.png)

**Use CKafka as a source**
1. Write a configuration file.
The combination of Flume and CKafka as a source is focused on here, while the sink and channel use the default configuration. Below is a simple demo (configured in the `conf` folder in the extracted directory). If there is no special requirement, simply replace your own instance IP and topic in the configuration file. The sink used in this example is `logger`.
2.	Start Flume.
```
./bin/flume-ng agent -n agentckafka -c conf -f conf/flume-kafka-source.properties
```
3. View the logger output (the default path is `logs/flume.log`).
![](https://mc.qcloudimg.com/static/img/d6b51f8de1a063e51171b2996764f40d/99.png)


