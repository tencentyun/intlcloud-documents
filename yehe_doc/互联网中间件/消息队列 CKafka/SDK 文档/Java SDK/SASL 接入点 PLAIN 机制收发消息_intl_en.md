## Overview

This document describes how to connect the Java SDK to CKafka via an SASL access point and send and receive messages based on the PLAIN mechanism in a public network environment.

## Prerequisites

- [Install JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Install Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)

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

1. Create a JAAS configuration file named `ckafka_client_jaas.conf`.
```
KafkaClient {
org.apache.kafka.common.security.plain.PlainLoginModule required
username="yourinstance#yourusername"
password="yourpassword";
};
```

>?Set `username` to a value in the format of `Instance ID` + `#` + `Configured username`, and `password` to a configured password.

2. Create a Kafka configuration file named `kafka.properties`.
```
##Set the SASL access point, which can be obtained via the console
bootstrap.servers=xxxx
##Set the topic, which can be created via the console
topic=xxxx
##Set the consumer group
group.id=xxxx
##Configure the JAAS configuration file
java.security.auth.login.config.plain=/xxxx/ckafka_client_jaas.conf
```

3. Create a configuration file loading program named `CKafkaConfigurer.java`.
```java
public class CKafkaConfigurer {

    private static Properties properties;

    public static void configureSaslPlain() {
        //If you have used the `-D` parameter or another method to set the path, do not set it again here
        if (null == System.getProperty("java.security.auth.login.config")) {
            //Replace `XXX` to your own path
            System.setProperty("java.security.auth.login.config",
                    getCKafkaProperties().getProperty("java.security.auth.login.config.plain"));
        }
    }

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

1. Create a message sending program named `KafkaSaslProducerDemo.java`.
```java
public class KafkaSaslProducerDemo {
   
       public static void main(String args[]) {
           //Set the path to the JAAS configuration file
           CKafkaConfigurer.configureSaslPlain();
       
           //Load `kafka.properties`
           Properties kafkaProperties =  CKafkaConfigurer.getCKafkaProperties();
       
           Properties props = new Properties();
           //Set the access point. Obtain the access point of the corresponding topic via the console
           props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
       
           //Set the access protocol
           props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
           //Set the PLAIN mechanism
           props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
       
           //Set the method for serializing Kafka messages
           props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
           props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
           //Set the maximum time to wait for a request
           props.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
           //Set the number of retries for the client
           props.put(ProducerConfig.RETRIES_CONFIG, 5);
           //Set the interval between retries for the client
           props.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
           //Construct a producer object. Note: a producer object is thread-safe, and generally one Producer object is sufficient for a process.
           KafkaProducer<String, String> producer = new KafkaProducer<>(props);
       
           //Construct a Kafka message
           String topic = kafkaProperties.getProperty("topic"); //Topic of the message. Enter the topic you created in the console
           String value = "this is ckafka msg value"; //Content of the message
       
           try {
               //Batch obtaining future objects can speed up the process. Note that the batch size should not be too large.
               List<Future<RecordMetadata>> futures = new ArrayList<>(128);
               for (int i =0; i < 100; i++) {
                   //Send the message and obtain a future object
                   ProducerRecord<String, String> kafkaMessage = new ProducerRecord<>(topic, value + ": " + i);
                   Future<RecordMetadata> metadataFuture = producer.send(kafkaMessage);
                   futures.add(metadataFuture);
       
               }
               producer.flush();
               for (Future<RecordMetadata> future: futures) {
                   //Synchronize the future object obtained
                       RecordMetadata recordMetadata = future.get();
                       System.out.println("Produce ok:" + recordMetadata.toString());
               }
           } catch (Exception e) {
               //If the sending still fails after client internal retries, the system needs to report and handle the error.
               System.out.println("error occurred");
           }
       }
   }
```


2. Compile and run `KafkaSaslProducerDemo.java` to send messages.
3. View the running result (output).
```bash
Produce ok:ckafka-topic-demo-0@198
Produce ok:ckafka-topic-demo-0@199
```
4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the target topic, and click **More** -> **Message Query** to view the message just sent.


### Step 4. Consume messages

1. Single consumer subscribing to messages: create a program named `KafkaSaslConsumerDemo.java` for a single consumer to subscribe to messages.
```java
public class KafkaSaslConsumerDemo {
    public static void main(String args[]) {
        //Set the path to the JAAS configuration file
        CKafkaConfigurer.configureSaslPlain();

        //Load `kafka.properties`
        Properties kafkaProperties =  CKafkaConfigurer.getCKafkaProperties();
        
        Properties props = new Properties();
        //Set the access point. Obtain the access point of the corresponding topic via the console
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
        
        //Set the access protocol
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
        //Set the PLAIN mechanism
        props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
        //Set the maximum interval between two polls
        //If the consumer does not return a heartbeat message within the interval, the broker determines that the consumer is not alive. the broker removes the consumer from the consumer group and triggers rebalancing. The default value is 30s.
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        //Set the maximum number of messages that can be polled at a time
        //Do not set this parameter to an excessively large value. If polled messages are not all consumed before the next poll starts, load balancing is triggered and lagging occurs.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        //Set the method for deserializing messages.
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        //Set the consumer group of the current consumer instance. Enter the topic you created in the console
        //The instances in the same consumer group consume messages in load balancing mode
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));
        //Construct a consumer object. This generates a consumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(props);
        //Set one or more topics to which the consumer group subscribes
        //You are advised to configure consumer instances with the same `GROUP_ID_CONFIG` value to subscribe to the same topics
        List<String> subscribedTopics =  new ArrayList<String>();
        //If you want to subscribe to multiple topics, add the topics here
        //You must create the topics in the console in advance
        String topicStr = kafkaProperties.getProperty("topic");
        String[] topics = topicStr.split(",");
        for (String topic: topics) {
            subscribedTopics.add(topic.trim());
        }
        consumer.subscribe(subscribedTopics);
        
        //Consume messages in loop
        while (true){
            try {
                ConsumerRecords<String, String> records = consumer.poll(1000);
                //All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`
                for (ConsumerRecord<String, String> record : records) {
                    System.out.println(String.format("Consume partition:%d offset:%d", record.partition(), record.offset()));
                }
            } catch (Exception e) {
                System.out.println("consumer error!");
            }
        }
    }
}
```


2. Compile and run `KafkaSaslConsumerDemo.java` to consume messages.

3. View the execution result.
   ```bash
   Consume partition:0 offset:298
   Consume partition:0 offset:299
   
   ```

4. On the **Consumer Group** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name, and click **Query Details** to view the consumption details.
![](https://main.qcloudimg.com/raw/ac08523c05f4f363024ca1eb2965410f.png)


