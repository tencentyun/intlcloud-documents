## Overview

This document describes how to use Spring Boot Starter to send and receive messages and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-springboot-demo.zip)

## Directions

### Step 1. Add dependencies

Import Pulsar Starter dependencies to the project.
<dx-codeblock>
:::  xml
<dependency>
    <groupId>io.github.majusko</groupId>
    <artifactId>pulsar-java-spring-boot-starter</artifactId>
    <version>1.0.7</version>
</dependency>
<!-- https://mvnrepository.com/artifact/io.projectreactor/reactor-core -->
<dependency>
    <groupId>io.projectreactor</groupId>
    <artifactId>reactor-core</artifactId>
    <version>3.4.11</version>
</dependency>
:::
</dx-codeblock>


### Step 2. Prepare configurations

Add Pulsar configuration information to the configuration file.
<dx-codeblock>
:::  yaml
pulsar:
  # Namespace name
  namespace: namespace_java
  # Service access address
  service-url: http://pulsar-xxx.tdmq.ap-gz.public.tencenttdmq.com:8080
  # Authorized role key
  token-auth-value: eyJrZXlJZC....
  # Cluster ID
  tenant: pulsar-xxx
:::
</dx-codeblock>
<table>
<tr>
<th>Parameter	</th>
<th>Description</th>
</tr>
<tr>
<td>namespace</td>
<td>Namespace name, which can be copied on the <a href = "https://console.intl.cloud.tencent.com/tdmq/env"><b>Namespace</b></a> page in the console.</td>
</tr>
<tr>
<td>service-url</td>
<td>Cluster access address, which can be viewed and copied on the <a href = "https://console.intl.cloud.tencent.com/tdmq/cluster"><b>Cluster</b></a> page in the console.<br><img src = "https://qcloudimg.tencent-cloud.cn/raw/0870f78ee97b38799824fd0ff0d3d4b7.png"></td>
</tr>
<tr>
<td>token-auth-value</td>
<td>Role key, which can be copied in the <b>Key</b> column on the <a href = "https://console.intl.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.<br><img src = "	https://qcloudimg.tencent-cloud.cn/raw/a585d077b08ae9b11fffcebf6cde926e.png"></td>
</tr>
<tr>
<td>tenant</td>
<td>Cluster ID, which can be obtained on the <a href = "https://console.intl.cloud.tencent.com/tdmq/cluster"><b>Cluster</b></a> page in the console.</td>
</tr>
</table>

### Step 3. Produce messages

1. Configure the producer factory.
<dx-codeblock>
:::  java
 @Configuration
 public class ProducerConfiguration {

		 @Bean
		 public ProducerFactory producerFactory() {
				 return new ProducerFactory()
								 // Use a string producer for topic 1
								 .addProducer("topic1", String.class)
								 // Use a byte[] (default type) producer for topic 2
								 .addProducer("topic2")
								 // Use a MyMessage (custom message type) producer for topic 3
								 .addProducer("topic4", MyMessage.class);
		 }
 }
:::
</dx-codeblock>
2. Inject producers.
<dx-codeblock>
:::  java
@Autowired
private PulsarTemplate<byte[]> defaultProducer;  // byte[] producer

@Autowired
private PulsarTemplate<String> stringProducer;   // String producer

@Autowired
private PulsarTemplate<MyMessage> customProducer;  // MyMessage (custom message type) producer
:::
</dx-codeblock>
3. Send messages.
<dx-codeblock>
:::  java
// Send a string message.
stringProducer.send("topic1", "Hello pulsar client.");

// Send a MyMessage message (custom message type)
MyMessage myMessage = new MyMessage();
myMessage.setData("Hello client, this is a custom message.");
myMessage.setSendDate(new Date());
customProducer.send("topic4", myMessage);

// Send a byte[] message
defaultProducer.send("topic2", ("Hello pulsar client, this is a order message" + i + ".").getBytes(StandardCharsets.UTF_8));
:::
</dx-codeblock>

> !
>
> - The topic sending messages is that declared in the producer configuration.
> - The type of `PulsarTemplate` must be the same as that of the sent message.
> - When you send a message to the specified topic, the message type must be the same as that bound to the topic in the producer factory configuration.

### Step 4. Consume messages

Configure the consumer.
<dx-codeblock>
:::  java
@PulsarConsumer(topic = "topic1",  // Subscribed topic name
                subscriptionName = "sub_topic1", // Subscription name
                clazz = String.class, // Message type, which must be the same as that of the producer and cannot be modified after binding
                serialization = Serialization.JSON, // Serialization method
                subscriptionType = SubscriptionType.Shared, // Subscription mode, which is exclusive mode by default
                consumerName = "firstTopicConsumer", // Consumer name
                maxRedeliverCount = 3, // Maximum number of retries
                deadLetterTopic = "sub_topic1-DLQ" // Dead letter topic name
               )
public void topicConsume(String msg) {
    // TODO process your message
    System.out.println("Received a new message. content: [" + msg + "]");
    // If consumption fails, report an exception, so that the message will enter the retry letter queue and can be consumed again. Once the maximum number of retries is reached, the message will enter the dead letter queue. You need to create retry and dead letter queues for the above process
}
:::
</dx-codeblock>



### Step 5. Query messages

1. Log in to the console and enter the **[Message Query](https://console.intl.cloud.tencent.com/tdmq/message)** page to view the message trace after running the demo.
![](https://qcloudimg.tencent-cloud.cn/raw/7945598f64d3cfe6ee3fc07feb4b778c.png)
   The message trace is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/9bbfbc3236aec54f1654c520eaa0cba4.png)

>? Above is a simple configuration for using TDMQ for Pulsar through Spring Boot Starter. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-springboot-demo.zip) or [Spring Boot Starter for Apache Pulsar](https://github.com/majusko/pulsar-java-spring-boot-starter).
