## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Spring Boot Starter as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- You have created the required resources as instructed in [Resource Creation and Preparation](https://intl.cloud.tencent.com/document/product/1112/43069).
- You have installed [JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html).
- You have installed [Maven 2.5 or later](http://maven.apache.org/download.cgi#).
- You have downloaded the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-springboot-demo.zip).

## Directions

### Step 1. Add dependencies

Add dependencies to the `pom.xml` file.
<dx-codeblock>
:::  xml
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-spring-boot-starter</artifactId>
    <version>2.2.1</version>
</dependency>
:::
</dx-codeblock>



### Step 2. Prepare configurations

Add configuration information to the configuration file.
<dx-codeblock>
:::  yaml
server:
     port: 8082

   # RocketMQ configuration information
   rocketmq:
     # Service access address of TDMQ for RocketMQ
     name-server: rocketmq-xxx.rocketmq.ap-bj.public.tencenttdmq.com:9876
     # Producer configurations
     producer:
       # Producer group name
       group: group111
       # Role token
       access-key: eyJrZXlJZC....
       # Name of the authorized role
       secret-key: admin
     # Common configurations for the consumer
     consumer:
       # Role token
       access-key: eyJrZXlJZC....
       # Name of the authorized role
       secret-key: admin

     # Custom configurations
     namespace: rocketmq-xxx|namespace1
     producer1:
       topic: testdev1
     consumer1:
       group: group111
       topic: testdev1
       subExpression: TAG1
     consumer2:
       group: group222
       topic: testdev1
       subExpression: TAG2
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">name-server</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list.</td>
</tr>
<tr>
<td align="left">group</td>
<td align="left">Producer group name, which can be copied under the <strong>Group</strong> tab in the console.</td>
</tr>
<tr>
<td align="left">secret-key</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">access-key</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/51a6ed907fd036c74cbda4500af19380.png" alt="img"></td>
</tr>
<tr>
<td align="left">namespace</td>
<td align="left">Namespace name, which can be copied under the <strong>Namespace</strong> tab in the console.</td>
</tr>
<tr>
<td align="left">topic</td>
<td align="left">Topic name, which can be copied under the <strong>Topic</strong> tab in the console.</td>
</tr>
<tr>
<td align="left">subExpression</td>
<td align="left">A parameter used to set the message tag.</td>
</tr>
</tbody></table>

### Step 3. Send messages

1. Inject **`RcoketMQTemplate`** into the class that needs to send messages.
<dx-codeblock>
:::  java
   @Value("${rocketmq.namespace}%${rocketmq.producer1.topic}")
         private String topic;  // Topic name, which needs to be concatenated.
         
         @Autowired
         private RocketMQTemplate rocketMQTemplate;
:::
</dx-codeblock>
2. Send messages. The message body can be a custom object or a message object and is contained in the package `org.springframework.messaging`.
<dx-codeblock>
:::  java
   SendResult sendResult = rocketMQTemplate.syncSend(destination, message);
	 /*------------------------------------------------------------------------*/
rocketMQTemplate.syncSend(destination, MessageBuilder.withPayload(message).build())
:::
</dx-codeblock>
3. Below is a complete sample.
	<dx-codeblock>
	:::  java
   /**
		* Description: Message producer
		*/
	 @Service
	 public class SendMessage {
		// Use the full name of the topic, which can be either customized or concatenated in the format of "full namespace name%topic name".
			 @Value("${rocketmq.namespace}%${rocketmq.producer1.topic}")
			 private String topic;

			 @Autowired
			 private RocketMQTemplate rocketMQTemplate;


			 /**
				* Sync sending
				*
				* @param message Message content
				* @param tags    Subscription tags
				*/
			 public void syncSend(String message, String tags) {
					 // Spring Boot does not support passing tags by using the header. You must concatenate the topic name and tags with a colon ":" as in `topicName:tags`; otherwise, the topic has no tag for identification.
					 String destination = StringUtils.isBlank(tags) ? topic : topic + ":" + tags;
					 SendResult sendResult = rocketMQTemplate.syncSend(destination,
									 MessageBuilder.withPayload(message)
													 .setHeader(MessageConst.PROPERTY_KEYS, "yourKey")   // Specify the business key
													 .build());
					 System.out.printf("syncSend1 to topic %s sendResult=%s %n", topic, sendResult);
			 }
	 }
:::
</dx-codeblock>

>?Above is a sync sending sample. For more information on async sending and one-way sending, see the [demo](https://tdmq-1300957330.cos.ap-guangzhou.myqcloud.com/TDMQ-demo/tdmq-rocketmq-demo/tdmq-rocketmq-springboot-demo.zip) or [RocketMQ Spring documentation](https://github.com/apache/rocketmq-spring).

### Step 4. Consume messages 
<dx-codeblock>
:::  java
@Service
   @RocketMQMessageListener(
           consumerGroup = "${rocketmq.namespace}%${rocketmq.consumer1.group}",  // Consumer group in the format of "full namespace name%group name"
       	// Use the full name of the topic, which can be either customized or concatenated in the format of "full namespace name%topic name".
           topic = "${rocketmq.namespace}%${rocketmq.consumer1.topic}",
           selectorExpression = "${rocketmq.consumer1.subExpression}" // Subscription expression. If this parameter is not configured, it means subscribing to all messages.
   )
   public class MessageConsumer implements RocketMQListener<String> {

       @Override
       public void onMessage(String message) {
           System.out.println("Tag1Consumer receive message:" + message);
       }
   }
:::
</dx-codeblock>

You can configure multiple consumers as needed, and the consumer configurations depend on your business requirements.

>?For the complete sample, see the [demo](https://tdmq-1300957330.cos.ap-guangzhou.myqcloud.com/TDMQ-demo/tdmq-rocketmq-demo/tdmq-rocketmq-springboot-demo.zip) or [RocketMQ Spring](https://github.com/apache/rocketmq-spring).

### Step 5. View consumption details

Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
![img](https://qcloudimg.tencent-cloud.cn/raw/1357b9a2c411352cf22fb2a502e6d520.png)

