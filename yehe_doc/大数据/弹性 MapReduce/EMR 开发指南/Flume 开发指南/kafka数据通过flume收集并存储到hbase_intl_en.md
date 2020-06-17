## Scenario Description
Data in Kafka can be collected through Flume and stored in HBase.

## Preparations for Development
- As this job requires access to CKafka, you need to create a CKafka instance first. For more information, please see [CKafka](https://intl.cloud.tencent.com/document/product/597).
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, you need to select the Spark component on the software configuration page.

## Using the Kafka Toolkit in the EMR Cluster
First, you need to check the private IP and port number of CKafka. Log in to the CKafka Console, select the CKafka instance you want to use, and view its private IP as `$kafkaIP` in the basic information section, and the port number is generally 9092 by default. Create a topic named `kafka_test` on the topic management page.

## Configuring Flume
1. Create the Flume configuration file `hbase_kafka.properties`.
```
vim hbase_kafka.properties
agent.sources = kafka_source
agent.channels = mem_channel
agent.sinks = hbase_sink
# The following code is used to configure the source
agent.sources.kafka_source.type = org.apache.flume.source.kafka.KafkaSource
agent.sources.kafka_source.channels = mem_channel
agent.sources.kafka_source.batchSize = 5000
agent.sources.kafka_source.kafka.bootstrap.servers = $kafkaIP:9092
agent.sources.kafka_source.kafka.topics = kafka_test
# The following code is used to configure the sink
agent.sinks.hbase_sink.channel = mem_channel
agent.sinks.hbase_sink.table = foo_table
agent.sinks.hbase_sink.columnFamily = cf
agent.sinks.hbase_sink.serializer = org.apache.flume.sink.hbase.RegexHbaseEventSerializer
# The following code is used to configure the channel
agent.channels.mem_channel.type = memory
agent.channels.mem_channel.capacity = 100000
agent.channels.mem_channel.transactionCapacity = 10000
```
2. Create an HBase table.
```
hbase shell
create 'foo_table','cf'
```
3. Run Flume.
```
./bin/flume-ng agent --conf ./conf/ -f hbase_kafka.properties -n agent -Dflume.root.logger=INFO,console
```
4. Run the Kafka producer.
```
[hadoop@172 kafka]$ ./bin/kafka-console-producer.sh --broker-list $kafkaIP:9092 --topic kafka_test
hello
hbase_test
```

## Test
- Enter information on the client of the Kafka producer and press Enter.
- Check whether there is corresponding data in the HBase table.

## Reference Documentation
[HBaseSink Configuration Description](https://flume.apache.org/FlumeUserGuide.html#hbasesinks)
