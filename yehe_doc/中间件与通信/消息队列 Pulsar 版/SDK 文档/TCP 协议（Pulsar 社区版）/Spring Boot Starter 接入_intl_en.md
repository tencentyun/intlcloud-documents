## Overview

This document describes how to use Spring Boot Starter to send and receive messages and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later](http://maven.apache.org/download.cgi#)
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
  # Role token
  token-auth-value: eyJrZXlJZC....
  # Cluster name
  tenant: pulsar-xxx
:::
</dx-codeblock>
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>namespace</td>
<td>Namespace name, which can be copied on the <a href = "https://console.cloud.tencent.com/tdmq/env"><b>Namespace</b></a> page in the console.</td>
</tr>
<tr>
<td>service-url</td>
<td>Cluster access address, which can be viewed and copied on the <a href = "https://console.cloud.tencent.com/tdmq/cluster"><b>Cluster</b></a> page in the console.<br><img src = "https://qcloudimg.tencent-cloud.cn/raw/0870f78ee97b38799824fd0ff0d3d4b7.png"></td>
</tr>
<tr>
<td>token-auth-value</td>
<td>Role token, which can be copied in the **Token** column on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.<br><img src = "https://qcloudimg.tencent-cloud.cn/raw/a585d077b08ae9b11fffcebf6cde926e.png"></td>
</tr>
<tr>
<td>tenant</td>
<td>Cluster ID, which can be obtained on the <a href = "https://console.cloud.tencent.com/tdmq/cluster"><b>Cluster</b></a> page in the console.</td>
</tr>
</table>

### Step 3. Produce messages

1. Configure the producer.
<dx-codeblock>
:::  java
@Configuration
public class ProducerConfiguration {

    @Bean
    public ProducerFactory producerFactory() {
        return new ProducerFactory()
                // topic1
                .addProducer("topic1")
                // topic2
                .addProducer("topic2");
    }
}
:::
</dx-codeblock>
2. Inject the producer.
   <dx-codeblock>
   :::  java
   @Autowired
   private PulsarTemplate<byte[]> defaultProducer;
	 :::
   </dx-codeblock>
3. Send messages.
<dx-codeblock>
:::  java
// Send the messages
defaultProducer.send("topic2", ("Hello pulsar client, this is a order message.").getBytes(StandardCharsets.UTF_8));
:::  
</dx-codeblock>
> !
>
> - The topic that sends messages is the one declared in the producer configuration.
> - The type of `PulsarTemplate` must be the same as that of the sent message.
> - When you send a message to the specified topic, the message type must be the same as that bound to the topic in the producer factory configuration.

### Step 4. Consume messages

Configure the consumer.
<dx-codeblock>
:::  java
@PulsarConsumer(topic = "topic1",  // Name of the subscribed topic
                subscriptionName = "sub_topic1", // Subscription name
                serialization = Serialization.JSON, // Serialization method
                subscriptionType = SubscriptionType.Shared, // Subscription mode, which is exclusive mode by default
                consumerName = "firstTopicConsumer", // Consumer name
                maxRedeliverCount = 3, // Maximum number of retries
                deadLetterTopic = "sub_topic1-DLQ" // Dead letter topic name
               )
public void topicConsume(byte[] msg) {
    // TODO process your message
    System.out.println("Received a new message. content: [" + new String(msg) + "]");
    // If the consumption fails, throw an exception, so that the message will enter the retry letter topic and can be consumed again. Once the maximum number of retries is reached, the message will enter the dead letter topic. You need to create retry and dead letter queues for the above process
}
:::
</dx-codeblock>



### Step 5. Query messages

Log in to the console and enter the **[Message Query](https://console.cloud.tencent.com/tdmq/message)** page to view the message trace after running the demo.
![](https://qcloudimg.tencent-cloud.cn/raw/7945598f64d3cfe6ee3fc07feb4b778c.png)
   The message trace is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/9bbfbc3236aec54f1654c520eaa0cba4.png)

>?The above is a simple configuration for using TDMQ for Pulsar through Spring Boot Starter. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-springboot-demo.zip) or [Spring Boot Starter for Apache Pulsar](https://github.com/majusko/pulsar-java-spring-boot-starter).
