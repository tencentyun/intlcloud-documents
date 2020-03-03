## Scenario Description
Data in Kafka can be collected through Flume and stored in Hive.

## Preparations for Development
- As this job requires access to CKafka, you need to create a CKafka instance first. For more information, please see [CKafka](https://intl.cloud.tencent.com/document/product/597).
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, you need to select the Spark component on the software configuration page.

## Using the Kafka Toolkit in the EMR Cluster
First, you need to check the private IP and port number of CKafka. Log in to the CKafka Console, select the CKafka instance you want to use, and view its private IP as `$kafkaIP` in the basic information section, and the port number is generally 9092 by default. Create a topic named `kafka_test` on the topic management page.

## Configuring Flume
1. Create the Flume configuration file `hive_kafka.properties`.
```
vim hive_kafka.properties
agent.sources = kafka_source
agent.channels = mem_channel
agent.sinks = hive_sink
# The following code is used to configure the source
agent.sources.kafka_source.type = org.apache.flume.source.kafka.KafkaSource
agent.sources.kafka_source.channels = mem_channel
agent.sources.kafka_source.batchSize = 5000
agent.sources.kafka_source.kafka.bootstrap.servers = $kafkaIP:9092
agent.sources.kafka_source.kafka.topics = kafka_test
# The following code is used to configure the sink
agent.sinks.hive_sink.channel = mem_channel
agent.sinks.hive_sink.type = hive
agent.sinks.hive_sink.hive.metastore = thrift://172.16.32.51:7004
agent.sinks.hive_sink.hive.database = default
agent.sinks.hive_sink.hive.table = weblogs
agent.sinks.hive_sink.hive.partition = asia,india,%y-%m-%d-%H-%M
agent.sinks.hive_sink.useLocalTimeStamp = true
agent.sinks.hive_sink.round = true
agent.sinks.hive_sink.roundValue = 10
agent.sinks.hive_sink.roundUnit = minute
agent.sinks.hive_sink.serializer = DELIMITED
agent.sinks.hive_sink.serializer.delimiter = ","
agent.sinks.hive_sink.serializer.serdeSeparator = ','
agent.sinks.hive_sink.serializer.fieldnames =id,msg
# The following code is used to configure the channel
agent.channels.mem_channel.type = memory
agent.channels.mem_channel.capacity = 100000
agent.channels.mem_channel.transactionCapacity = 10000
You can confirm Hive Metastore in the following way:
grep "hive.metastore.uris" -C 2 /usr/local/service/hive/conf/hive-site.xml
<property>
<name>hive.metastore.uris</name>
<value>thrift://172.16.32.51:7004</value>
</property>
```
2. Create a Hive table.
```
create table weblogs ( id int , msg string )
partitioned by (continent string, country string, time string)
clustered by (id) into 5 buckets
stored as orc TBLPROPERTIES ('transactional'='true');
```
>All the following conditions must be met: it must be a table with partitions and buckets, the storage format is ORC, and `TBLPROPERTIES ('transactional'='true')` is set.
3. Enable the Hive transaction.
In the console, add the following configuration items to `hive-site.xml`.
```
<property>
<name>hive.support.concurrency</name>
<value>true</value>
</property>
<property>
<name>hive.exec.dynamic.partition.mode</name>
<value>nonstrict</value>
</property>
<property>
<name>hive.txn.manager</name>
<value>nonstrict</value>
</property>
<property>
<name>hive.exec.dynamic.partition.mode</name>
<value>org.apache.hadoop.hive.ql.lockmgr.DbTxnManager</value>
</property>
<property>
<name>hive.compactor.initiator.on</name>
<value>true</value>
</property>
<property>
<name>hive.compactor.worker.threads</name>
<value>1</value>
</property>
<property>
<name>hive.enforce.bucketing</name>
<value>true</value>
</property>
```
>After the configuration is distributed and Hive is restarted, the `hadoop-hive` log will prompt that the Metastore cannot be connected to. Please ignore this error. Because of the startup order of the processes, Metastore will be started before HiveServer2.
4. Copy `hive-hcatalog-streaming-xxx.jar` of Hive to the `lib` directory of Flume.
```
cp -ra /usr/local/service/hive/hcatalog/share/hcatalog/hive-hcatalog-streaming-2.3.3.jar /usr/local/service/flume/lib/
```
5. Run Flume.
```
./bin/flume-ng agent --conf ./conf/ -f hive_kafka.properties -n agent -Dflume.root.logger=INFO,console
```
6. Run the Kafka producer.
```
[hadoop@172 kafka]$ ./bin/kafka-console-producer.sh --broker-list $kafkaIP:9092 --topic kafka_test
1,hello
2,hi
```

## Test
 - Enter information on the client of the Kafka producer and press Enter.
 - Check whether there is corresponding data in the Hive table.

## Reference Documentation
- [Hive Sink Configuration Description](https://flume.apache.org/FlumeUserGuide.html#hive-sink)
- [Hive Log Configuration Description](https://cwiki.apache.org/confluence/display/Hive/Hive+Transactions#HiveTransactions-NewConfigurationParametersforTransactions)
