## Scenario Description
Data in Kafka can be collected through Flume and stored in HDFS or COS.

## Preparations for Development
- As this job requires access to CKafka, you need to create a CKafka instance first. For more information, please see [CKafka](https://intl.cloud.tencent.com/document/product/597).
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, you need to select the Spark component on the software configuration page.

## Using the Kafka Toolkit in the EMR Cluster
First, you need to check the private IP and port number of CKafka. Log in to the CKafka Console, select the CKafka instance you want to use, and view its private IP as `$kafkaIP` in the basic information section, and the port number is generally 9092 by default. Create a topic named `kafka_test` on the topic management page.

## Configuring Flume
1.	Create the Flume configuration file `kafka.properties`.
```
vim kafka.properties
agent.sources = kafka_source
agent.channels = mem_channel
agent.sinks = hdfs_sink
# The following code is used to configure the source
agent.sources.kafka_source.type = org.apache.flume.source.kafka.KafkaSource
agent.sources.kafka_source.channels = mem_channel
agent.sources.kafka_source.batchSize = 5000
agent.sources.kafka_source.kafka.bootstrap.servers = $kafkaIP:9092
agent.sources.kafka_source.kafka.topics = kafka_test
# The following code is used to configure the sink
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
# The following code is used to configure the channel
agent.channels.mem_channel.type = memory
agent.channels.mem_channel.capacity = 100000
agent.channels.mem_channel.transactionCapacity = 10000
```
2. Run Flume.
```
./bin/flume-ng agent --conf ./conf/ -f kafka.properties -n agent -Dflume.root.logger=INFO,console
```
3. Run Kafka. 
```
producer./bin/kafka-console-producer.sh --broker-list $kafkaIP:9092 --topic kafka_test
test
hello
```

## Test
 - Enter information on the client of the Kafka producer and press Enter.
 - Check whether the corresponding directory and file `hadoop fs -ls /data/flume/kafka/` have been generated in HDFS.

## Reference Documentation
[Kafka Source Configuration Description](https://flume.apache.org/FlumeUserGuide.html#kafka-source)
