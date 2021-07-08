## Scenario Description
Collecting and saving the data in Kafka to HDFS or COS via Flume

## Development Preparations
- This task requires access to CKafka, so you need to create a CKafka instance first. For more information, see [Message Queue CKafka](https://intl.cloud.tencent.com/document/product/597).
- Create an EMR cluster. When creating the EMR cluster, you need to select the Spark component on the software configuration page and enable access to COS on the basic configuration page.

## Using the Kafka Toolkit in the EMR Cluster
First, you need to check the private IP and port number of CKafka. Log in to the CKafka console, select the CKafka instance you want to use, and find the private IP (`$kafkaIP`) and port number (generally `9092`) in the basic information section. Create a topic named `kafka_test` on the topic management page.

## Configuring Flume
1. Create a Flume configuration file `kafka.properties`.
```
vim kafka.properties
agent.sources = kafka_source
agent.channels = mem_channel
agent.sinks = hdfs_sink
# The following is for source configuration.
agent.sources.kafka_source.type = org.apache.flume.source.kafka.KafkaSource
agent.sources.kafka_source.channels = mem_channel
agent.sources.kafka_source.batchSize = 5000
agent.sources.kafka_source.kafka.bootstrap.servers = $kafkaIP:9092
agent.sources.kafka_source.kafka.topics = kafka_test
# The following is for sink configuration.
agent.sinks.hdfs_sink.type = hdfs
agent.sinks.hdfs_sink.channel = mem_channel
agent.sinks.hdfs_sink.hdfs.path = /data/flume/kafka/%Y%m%d (or cosn://bucket/xxx)
agent.sinks.hdfs_sink.hdfs.rollSize = 0  
agent.sinks.hdfs_sink.hdfs.rollCount = 0  
agent.sinks.hdfs_sink.hdfs.rollInterval = 3600  
agent.sinks.hdfs_sink.hdfs.threadsPoolSize = 30
agent.sinks.hdfs_sink.hdfs.fileType=DataStream    
agent.sinks.hdfs_sink.hdfs.useLocalTimeStamp=true
agent.sinks.hdfs_sink.hdfs.writeFormat=Text
# The following is for channel configuration.
agent.channels.mem_channel.type = memory
agent.channels.mem_channel.capacity = 100000
agent.channels.mem_channel.transactionCapacity = 10000
```
2. Run Flume.
```
./bin/flume-ng agent --conf ./conf/ -f kafka.properties -n agent -Dflume.root.logger=INFO,console
```
3. Run Kafka producer.
```
[hadoop@172 kafka]$ ./bin/kafka-console-producer.sh --broker-list $kafkaIP:9092 --topic kafka_test
test
hello
```

## Testing
- Enter information on the Kafka producer client and press Enter.
- Check whether the corresponding directory and file `hadoop fs -ls /data/flume/kafka/` have been generated in HDFS.

## References
[Kafka Source Configuration Description](https://flume.apache.org/FlumeUserGuide.html#kafka-source)