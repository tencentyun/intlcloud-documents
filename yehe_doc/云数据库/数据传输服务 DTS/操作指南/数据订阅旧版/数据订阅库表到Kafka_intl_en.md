This document provides a simple example that walks you through how to pull a table from data subscription to Kafka as well as a simple [Kafka Demo](https://main.qcloudimg.com/raw/cf803ad5ddbb3f20534d98a5a0a23334/KafkaDemo.zip).

## Configuring Environment
- OS: CentOS
- Download relevant resources
 - [Data subscription SDK](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/binlogsdk-2.8.2-jar-with-dependencies.jar?_ga=1.22270587.1971922487.1581299091)
 - [SLF4J component](https://main.qcloudimg.com/raw/f8a577788af1d57cd269410fbe436a35/SLF4J.zip)
 - [Kafka-clients](https://main.qcloudimg.com/raw/a60f793a4eafe5f77e63615c5ce920e8/kafka-clients-1.1.0.jar)
- Java environment configuration 
```
yum install java-1.8.0-openjdk-devel 
```

## Installing Kafka 
1. Please install Kafka as instructed in [Kafka Quick Start](http://kafka.apache.org/quickstart).
2. After Kafka is launched, create a `testtop` topic.
```
[root@VM_71_10_centos kafka_2.11-1.1.0]# bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic testtop
Created topic "testtop".
```

## Getting Key
Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) to get a key.

## Selecting Data Subscription
1. Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page) and select **Data Subscription** on the left sidebar to enter the data subscription page.
2. In the subscription list, click a subscription name to enter the subscription details page and view the corresponding channel ID, service IP, and service port.
3. Enter them together with the obtained key into the corresponding `KafkaDemo.java`.
```
  // Enter the key obtained from the CAM Console here      
 final String TOPIC = "testtop"; Subscribed topic
        Properties props = new Properties();
	props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092"); Enter the `ip:port` corresponding to Kafka
        props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        final Producer<String, String> producer = new KafkaProducer<String, String>(props);
               context.setSecretId("AKIDfdsfdsfsdt1331431sdfds"); Enter the obtained `secretID`
        context.setSecretKey("test111usdfsdfsddsfRkeT"); Enter the obtained `secretKey`
	// Enter the IP and port obtained from the subscription details page here
        context.setServiceIp("10.66.112.181"); Enter the obtained IP
        context.setServicePort(7507); Enter the obtained port
        final DefaultSubscribeClient client = new DefaultSubscribeClient(context);
	// Enter the names of both the database and table to be synced and modify the name of the file where they will be stored
        final String targetDatabase = "test"; Enter the name of the database to subscribe to
                 client.addClusterListener(listener);
	// Enter the `dts-channel` configuration information obtained from the subscription details page here
	client.askForGUID("dts-channel-e4FQxtYV3It4test"); Enter the obtained channel ID
        client.start();
```


## Compiling and Testing
1. Compile the client program `KafkaDemo.java`.
```
javac -classpath binlogsdk-2.6.0-release.jar:slf4j-api-1.7.25.jar:slf4j-log4j12-1.7.2.jar:kafka-clients-1.1.0.jar -encoding UTF-8 KafkaDemo.java 
```
2. Launch the program. If no errors are reported, the program works properly.
```
java -XX:-UseGCOverheadLimit -Xms2g -Xmx2g  -classpath .:binlogsdk-2.6.0-release.jar:kafka-clients-1.1.0.jar:slf4j-api-1.7.25.jar:slf4j-log4j12-1.7.2.jar  KafkaDemo
```
3. Insert a data entry into the `alantest` table, and you will find that the data has been stored in the `testtop` subscribed to by Kafka.

```
MySQL [test]> insert into alantest values(123456,'alan');
Query OK, 1 row affected (0.02 sec)

[root@VM_71_10_centos kafka_2.11-1.1.0]#  bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic testtop --from-beginning 
checkpoint:144251@3@1275254@1153089
record_id:00000100000000001198410000000000000001
record_encoding:utf8
fields_enc:latin1,utf8
gtid:4f21864b-3bed-11e8-a44c-5cb901896188:5552
source_category:full_recorded
source_type:mysql
table_name:alantest
record_type:INSERT
db:test
timestamp:1524649133
primary:id

Field name: id
Field type: 3
Field length: 6
Field value: 123456
Field name: name
Field type: 253
Field length: 4
Field value: alan
```

