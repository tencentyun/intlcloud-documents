## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Java in a VPC.

## Prerequisites

- [Install JDK 1.8 or above](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Install Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/javakafkademo/VPC)

## Directions

### Step 1. Prepare configurations

1. Upload the `javakafkademo` in the downloaded demo to the Linux server.
2. Log in to the Linux server, enter the `javakafkademo` directory, and configure related parameters.
  2.1 Add the following Java dependency library information to the `pom.xml` file:
      ```xml
      <dependency>
          <groupId>org.apache.kafka</groupId>
          <artifactId>kafka-clients</artifactId>
          <version>0.10.2.2</version>
      </dependency>
      ```
   2.2 Create the CKafka configuration file `kafka.properties`.
      ```bash
      ## Configure the accessed network by copying the information in the **Network** column in the **Access Mode** section on the **Instance Details** page in the console.
      bootstrap.servers=ckafka-xxxxxxxxxxxxxxxxx
      ## Configure the topic by copying the information on the **Topic Management** page in the console.
      topic=XXX
      ## Configure the consumer group as needed
      group.id=XXX
      ```
| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| bootstrap.servers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![](https://main.qcloudimg.com/raw/88b29cffdf22e3a0309916ea715057a1.png) |
| topic             | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |
| group.id          | You can customize it. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |

2.3 Create the configuration file loading program `CKafkaConfigurer.java`. 
      ```
      public class CKafkaConfigurer {
      
          private static Properties properties;
      
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


### Step 2. Send a message

1. Write the message production program `CKafkaProducerDemo.java`.

```java
public class CKafkaProducerDemo {

    public static void main(String args[]) {
        // Load `kafka.properties`
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties properties = new Properties();
        // Set the access point of the corresponding topic, which can be obtained in the console
        properties.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));

        // Set the method for serializing Kafka messages. `StringSerializer` is used in this demo.
        properties.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringSerializer");
        // Set the maximum time to wait for a request
        properties.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
        // Set the number of retries for the client
        properties.put(ProducerConfig.RETRIES_CONFIG, 5);
        // Set the internal retry interval for the client
        properties.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
        // Construct a producer object
        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);

        // Construct a CKafka message
        String topic = kafkaProperties.getProperty("topic"); // Topic of the message. Enter the topic you created in the console
        String value = "this is ckafka msg value"; // Message content

        try {
            // Batch getting future objects can speed up the process. Note that the batch size should not be too large
            List<Future<RecordMetadata>> futureList = new ArrayList<>(128);
            for (int i = 0; i < 10; i++) {
                // Send the message and get a future object
                ProducerRecord<String, String> kafkaMsg = new ProducerRecord<>(topic,
                        value + ": " + i);
                Future<RecordMetadata> metadataFuture = producer.send(kafkaMsg);
                futureList.add(metadataFuture);

            }
            producer.flush();
            for (Future<RecordMetadata> future : futureList) {
                // Sync the future object obtained
                RecordMetadata recordMetadata = future.get();
                System.out.println("produce send ok: " + recordMetadata.toString());
            }
        } catch (Exception e) {
            // If the sending still fails after client internal retries, the system needs to report and handle the error.
            System.out.println("error occurred");
        }
    }
}
```
2. Compile and run `CKafkaProducerDemo.java` to send the message.
3. View the execution result.
```bash
Produce ok:ckafka-topic-demo-0@198
Produce ok:ckafka-topic-demo-0@199
```
4. On the **Topic Management** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic and click **More** > **Message Query** to view the just sent message.
   ![](https://main.qcloudimg.com/raw/ec5fbf218cf50ff3d760be15f6331867.png)


### Step 3. Consume the message

1. Create the subscribed message consumer program `CKafkaConsumerDemo.java`.
```java
public class CKafkaConsumerDemo {

    public static void main(String args[]) {
        // Load `kafka.properties`
        Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

        Properties props = new Properties();
        // Set the access point of the corresponding topic, which can be obtained in the console
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));
        // Set the maximum interval between two polls
        // If the consumer does not return a heartbeat message within the interval, the broker determines that the consumer is not alive. The broker removes the consumer from the consumer group and triggers rebalancing. The default value is 30s
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        // Set the maximum number of messages that can be polled at a time
        // Do not set this parameter to an excessively large value. If polled messages are not all consumed before the next poll starts, load balancing is triggered and lagging occurs.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        // Set the method for deserializing messages
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        // The instances in the same consumer group consume messages in load balancing mode
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));
        // Construct a consumer object. This generates a consumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        // Set one or more topics to which the consumer group subscribes
        // We recommend you configure consumer instances with the same `GROUP_ID_CONFIG` value to subscribe to the same topics
        List<String> subscribedTopics = new ArrayList<>();
        // If you want to subscribe to multiple topics, add the topics here
        // You must create the topics in the console in advance
        String topicStr = kafkaProperties.getProperty("topic");
        String[] topics = topicStr.split(",");
        for (String topic : topics) {
            subscribedTopics.add(topic.trim());
        }
        consumer.subscribe(subscribedTopics);

        // Consume messages in loop
        while (true) {
            try {
                ConsumerRecords<String, String> records = consumer.poll(1000);
                // All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`
                // We recommend you create an independent thread to consume messages and then return the result in async mode
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
2. Compile and run `CKafkaConsumerDemo.java` to consume the message.
3. View the execution result.
```bash
Consume partition:0 offset:298
Consume partition:0 offset:299
```
4. On the **Consumer Group** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name in **Topic Name**, and click **Query Details** to view the consumption details.
   ![](https://main.qcloudimg.com/raw/27775267907600f4ff759e6a197195ee.png)
