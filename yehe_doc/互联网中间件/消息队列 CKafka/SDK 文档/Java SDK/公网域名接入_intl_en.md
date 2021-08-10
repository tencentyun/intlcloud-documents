## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Java over the public network.

## Prerequisites

- [Install JDK 1.8 or above](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Install Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/javakafkademo/PUBLIC_SASL)

## Directions

### Step 1. Add the Java dependency library

Add the following Java dependency library information to the `pom.xml` file:

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>0.10.2.2</version>
</dependency>
```

### Step 2. Prepare configurations

1. Create the JAAS configuration file `ckafka_client_jaas.conf`.
```bash
KafkaClient {
org.apache.kafka.common.security.plain.PlainLoginModule required
username="yourinstance#yourusername"
password="yourpassword";
};
```
 >?`username` is the combination of the `instance ID` + `#` + `configured username`, and `password` is the configured password.

2. Create the CKafka configuration file `kafka.properties`.
```bash
## Configure the accessed network by copying the information in the **Network** column in the **Access Mode** section on the **Instance Details** page in the console.
bootstrap.servers=xx.xx.xx.xx:xxxx
## Configure the topic by copying the information on the **Topic Management** page in the console.
topic=XXX
## Configure the consumer group as needed
group.id=XXX
## Path of the JAAS configuration file `ckafka_client_jaas.conf`.
java.security.auth.login.config.plain=/xxxx/ckafka_client_jaas.conf
```

| Parameter | Description |
| ------------------------------------- | ------------------------------------------------------------ |
| bootstrap.servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| topic             | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |
| group.id          | You can customize it. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |
| java.security.auth.login.config.plain | Enter the path of the JAAS configuration file `ckafka_client_jaas.conf`.              |

3. Create the configuration file loading program `CKafkaConfigurer.java`.
```
public class CKafkaConfigurer {

    private static Properties properties;

    public static void configureSaslPlain() {
        // If you have used the `-D` parameter or another method to set the path, do not set it again here
        if (null == System.getProperty("java.security.auth.login.config")) {
            // Replace `XXX` with your own path
            System.setProperty("java.security.auth.login.config",
                    getCKafkaProperties().getProperty("java.security.auth.login.config.plain"));
        }
    }

    public synchronized static Properties getCKafkaProperties() {
        if (null != properties) {
            return properties;
        }
        // Get the content of the configuration file `kafka.properties`
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



### Step 3. Send a message

1. Create the message sending program `KafkaSaslProducerDemo.java`.
   ```java
   public class KafkaSaslProducerDemo {
   
       public static void main(String args[]) {
           // Set the path of the JAAS configuration file
           CKafkaConfigurer.configureSaslPlain();
   
           // Load `kafka.properties`
           Properties kafkaProperties =  CKafkaConfigurer.getCKafkaProperties();
   
           Properties props = new Properties();
           // Set the access point of the corresponding topic, which can be obtained in the console
           props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
   
           // Set the access protocol
           props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
           // Set the PLAIN mechanism
           props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
   
           // Set the method for serializing Kafka messages
           props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
           props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
           // Set the maximum time to wait for a request
           props.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
           // Set the number of retries for the client
           props.put(ProducerConfig.RETRIES_CONFIG, 5);
           // Set the internal retry interval for the client
           props.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
           // Construct a producer object. Note: a producer object is thread-safe, and generally one Producer object is sufficient for a process.
           KafkaProducer<String, String> producer = new KafkaProducer<>(props);
   
           // Construct a CKafka message
           String topic = kafkaProperties.getProperty("topic"); // Topic of the message. Enter the topic you created in the console
           String value = "this is ckafka msg value"; // Message content
   
           try {
               // Batch getting future objects can speed up the process. Note that the batch size should not be too large.
               List<Future<RecordMetadata>> futures = new ArrayList<>(128);
               for (int i =0; i < 100; i++) {
                   // Send the message and get a future object
                   ProducerRecord<String, String> kafkaMessage = new ProducerRecord<>(topic, value + ": " + i);
                   Future<RecordMetadata> metadataFuture = producer.send(kafkaMessage);
                   futures.add(metadataFuture);
   
               }
               producer.flush();
               for (Future<RecordMetadata> future: futures) {
                   // Sync the future object obtained
                       RecordMetadata recordMetadata = future.get();
                       System.out.println("Produce ok:" + recordMetadata.toString());
               }
           } catch (Exception e) {
               // If the sending still fails after client internal retries, the system needs to report and handle the error.
               System.out.println("error occurred");
           }
       }
   }
   ```
2. Compile and run `KafkaSaslProducerDemo.java` to send the message.
3. View the execution result (output).
```bash
Produce ok:ckafka-topic-demo-0@198
Produce ok:ckafka-topic-demo-0@199
```
4. On the **Topic Management** page in the CKafka console, select the corresponding topic and click **More** > **Message Query** to view the just sent message.
![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)



### Step 4. Consume the message

1. Create the subscribed message consumer program `KafkaSaslConsumerDemo.java`.

```java
public class KafkaSaslConsumerDemo {
    public static void main(String args[]) {
        // Set the path of the JAAS configuration file
        CKafkaConfigurer.configureSaslPlain();

        // Load `kafka.properties`
        Properties kafkaProperties =  CKafkaConfigurer.getCKafkaProperties();

        Properties props = new Properties();
        // Set the access point of the corresponding topic, which can be obtained in the console
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));

        // Set the access protocol
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
        // Set the PLAIN mechanism
        props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
        // Set the maximum interval between two polls
        // If the consumer does not return a heartbeat message within the interval, the broker determines that the consumer is not alive. The broker removes the consumer from the consumer group and triggers rebalancing. The default value is 30s
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        // Set the maximum number of messages that can be polled at a time
        // Do not set this parameter to an excessively large value. If polled messages are not all consumed before the next poll starts, load balancing is triggered and lagging occurs.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        // Set the method for deserializing messages
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        // Set the consumer group of the current consumer instance. Enter the topic you created in the console
        // The instances in the same consumer group consume messages in load balancing mode
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));
        // Construct a consumer object. This generates a consumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(props);
        // Set one or more topics to which the consumer group subscribes
        // We recommend you configure consumer instances with the same `GROUP_ID_CONFIG` value to subscribe to the same topics
        List<String> subscribedTopics =  new ArrayList<String>();
        // If you want to subscribe to multiple topics, add the topics here
        // You must create the topics in the console in advance
        String topicStr = kafkaProperties.getProperty("topic");
        String[] topics = topicStr.split(",");
        for (String topic: topics) {
            subscribedTopics.add(topic.trim());
        }
        consumer.subscribe(subscribedTopics);

        // Consume messages in loop
        while (true){
            try {
                ConsumerRecords<String, String> records = consumer.poll(1000);
                // All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`
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
2. Compile and run `KafkaSaslConsumerDemo.java` to consume the message.
3. View the execution result.
   ```bash
   Consume partition:0 offset:298
   Consume partition:0 offset:299   
   ```
4. On the **Consumer Group** page in the CKafka console, select the corresponding consumer group, enter the topic name in **Topic Name**, and click **Query Details** to view the consumption details.
   ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
