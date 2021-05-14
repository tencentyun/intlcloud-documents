## Overview

This document describes how to use the Java SDK to connect to CKafka via the default access point and send and receive messages in a VPC environment.

## Prerequisites

- [Install JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Install Maven 2.5 or later](http://maven.apache.org/download.cgi#)

## Directions

### Step 1. Add the Java dependent library

Add the following Java dependent library information to the `pom.xml` file:
```java
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>0.10.2.2</version>
</dependency>
```

### Step 2. Prepare configurations

1. Create a Kafka configuration file named `kafka.properties`.
```
## Configure an access point (access point displayed on the instance details page in the console)
bootstrap.servers=xxxxxxxxxxxxxxxxxxxxx
## Configure a topic, which can be created in the console
topic=ckafka-topic-demo
## Configure a consumer group
group.id=ckafka-consumer-group-demo
```

2. Create a configuration file loading program named `CKafkaConfigurer.java`. 
```java
public class CKafkaConfigurer {

    private static Properties properties;

    public synchronized static Properties getCKafkaProperties() {
        if (null != properties) {
            return properties;
        }
        //Obtain the content of the configuration file `kafka.properties`
        Properties kafkaProperties = new Properties();
        try {
            kafkaProperties.load(CKafkaProducerDemo.class.getClassLoader().getResourceAsStream("kafka.properties"));
        } catch (Exception e) {
            System.out.println("getCKafkaProperties error");
        }
        properties = kafkaProperties;
        return kafkaProperties;
    }
}
```


### Step 3. Send messages

1. Write a message producer named `CKafkaProducerDemo.java`.
```java
public class CKafkaProducerDemo {

    public static void main(String args[]) {
        //Load `kafka.properties`
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties properties = new Properties();
        //Set the access point. Obtain the access point of the corresponding topic via the console
        properties.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
    
        //Set the method for serializing Kafka messages. `StringSerializer` is used in this demo.
        properties.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        //Set the maximum time to wait for a request
        properties.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
        //Set the number of retries for the client
        properties.put(ProducerConfig.RETRIES_CONFIG, 5);
        //Set the interval between retries for the client
        properties.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
        //Construct a producer object
        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);
    
        //Construct a Kafka message
        String topic = kafkaProperties.getProperty("topic"); //Topic of the message. Enter the topic you created in the console
        String value = "this is ckafka msg value"; //Content of the message
    
        try {
            //Batch obtaining future objects can speed up the process. Note that the batch size should not be too large.
            List<Future<RecordMetadata>> futureList = new ArrayList<>(128);
            for (int i = 0; i < 10; i++) {
                //Send the message and obtain a future object
                ProducerRecord<String, String> kafkaMsg = new ProducerRecord<>(topic,
                        value + ": " + i);
                Future<RecordMetadata> metadataFuture = producer.send(kafkaMsg);
                futureList.add(metadataFuture);
    
            }
            producer.flush();
            for (Future<RecordMetadata> future : futureList) {
                //Synchronize the future object obtained
                RecordMetadata recordMetadata = future.get();
                System.out.println("produce send ok: " + recordMetadata.toString());
            }
        } catch (Exception e) {
            //If the sending still fails after client internal retries, the system needs to report and handle the error.
            System.out.println("error occurred");
        }
    }
}
```

2. Compile and run `CKafkaProducerDemo.java` to send messages.
3. View the execution result.
```bash
Produce ok:ckafka-topic-demo-0@198
Produce ok:ckafka-topic-demo-0@199
```

4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the target topic, and click **More** -> **Message Query** to view the message just sent.



### Step 4. Consume messages

1. Create a program named `CKafkaConsumerDemo.java` for a single consumer to subscribe to messages.
```java
public class CKafkaConsumerDemo {

    public static void main(String args[]) {
        //Load `kafka.properties`
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties props = new Properties();
        //Set the access point. Obtain the access point of the corresponding topic via the console
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
        //Set the maximum interval between two polls
        //If the consumer does not return a heartbeat message within the interval, the broker determines that the consumer is not alive. the broker removes the consumer from the consumer group and triggers rebalancing. The default value is 30s.
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        //Set the maximum number of messages that can be polled at a time
        //Do not set this parameter to an excessively large value. If polled messages are not all consumed before the next poll starts, load balancing is triggered and lagging occurs.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        //Set the method for deserializing messages.
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        //The instances in the same consumer group consume messages in load balancing mode
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));
        //Construct a consumer object. This generates a consumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        //Set one or more topics to which the consumer group subscribes
        //You are advised to configure consumer instances with the same `GROUP_ID_CONFIG` value to subscribe to the same topics
        List<String> subscribedTopics = new ArrayList<>();
        //If you want to subscribe to multiple topics, add the topics here
        //You must create the topics in the console in advance
        String topicStr = kafkaProperties.getProperty("topic");
        String[] topics = topicStr.split(",");
        for (String topic : topics) {
            subscribedTopics.add(topic.trim());
        }
        consumer.subscribe(subscribedTopics);
    
        //Consume messages in loop
        while (true) {
            try {
                ConsumerRecords<String, String> records = consumer.poll(1000);
                //All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`
                //You are advised to create an independent thread to consume messages and then return the result in async mode
                for (ConsumerRecord<String, String> record : records) {
                    System.out.println(
                            String.format("Consume partition:%d offset:%d", record.partition(), record.offset()));
                }
            } catch (Exception e) {
                System.out.println("consumer error!");
            }
        }
    }
}
```


2. Compile and run `CKafkaConsumerDemo.java` to consume messages.
3. View the execution result.
```bash
Consume partition:0 offset:298
Consume partition:0 offset:299
```
4. On the **Consumer Group** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group name, enter the topic name, and click **Query Details** to view the consumption details.
![](https://main.qcloudimg.com/raw/f778ac439bde4a94c18c51b966f6877b.png)



