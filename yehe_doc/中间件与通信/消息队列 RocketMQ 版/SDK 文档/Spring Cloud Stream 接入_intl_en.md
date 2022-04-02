## Overview

This document describes how to use Spring Cloud Stream to send and receive messages and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1112/43069).
- [You have installed JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-springcloud-stream-demo.zip)

## Directions
### Step 1. Import dependencies
Import dependencies related to `stream-rocketmq` to the `pom.xml` file.
```xml
<dependency>
		<groupId>org.apache.rocketmq</groupId>
		<artifactId>rocketmq-client</artifactId>
		<version>4.7.1</version>
</dependency>
<dependency>
	 <groupId>org.apache.rocketmq</groupId>
	 <artifactId>rocketmq-acl</artifactId>
	 <version>4.7.1</version>
</dependency>

<!-- The RocketMQ version in spring-cloud-starter-stream-rocketmq is old. Exclude it and import a new version.-->
<dependency>
	 <groupId>com.alibaba.cloud</groupId>
	 <artifactId>spring-cloud-starter-stream-rocketmq</artifactId>
	 <version>2.2.5-RocketMQ-RC1</version>
	 <exclusions>
			 <exclusion>
					 <groupId>org.apache.rocketmq</groupId>
					 <artifactId>rocketmq-client</artifactId>
			 </exclusion>
			 <exclusion>
					 <groupId>org.apache.rocketmq</groupId>
					 <artifactId>rocketmq-acl</artifactId>
			 </exclusion>
	 </exclusions>
</dependency>
```

### Step 2. Add configurations
Add RocketMQ-related configurations to the configuration file.
```yaml
spring:
 cloud:
	 stream:
		 rocketmq:
			 bindings:
				 # Channel name, which is the same as the channel name in spring.cloud.stream.bindings.
				 Topic-test1:
					 consumer:
						 # Tag type of the subscription, which is configured based on consumers’ actual needs. All messages are subscribed to by default.
						 subscription: TAG1
				 # Channel name
				 Topic-test2:
					 consumer:
						 subscription: TAG2
			 binder:
				 # Full service address
				 name-server: rocketmq-xxx.rocketmq.ap-bj.public.tencenttdmq.com:9876
				 # Role name
				 secret-key: admin
				 # Role token
				 access-key: eyJrZXlJZ...
				 # Full namespace name
				 namespace: rocketmq-xxx|namespace1
				 # Producer group name
				 group: group1
		 bindings:
			 # Channel name
			 Topic-send:
				 # Specify a topic, which refers to the one you created
				 destination: topic1
				 content-type: application/json
				 # The group name to be used
				 group: group1
			 # Channel name
			 Topic-test1:
				 destination: topic1
				 content-type: application/json
				 group: group1
			 # Channel name
			 Topic-test2:
				 destination: topic1
				 content-type: application/json
				 group: group2
```
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">name-server</td>
<td align="left">Cluster access address, which can be obtained from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster Management</strong> page in the console.</td>
</tr>
<tr>
<td align="left">secret-key</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">access-key</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/14e42cb135540bf6f79a6b04e5e76bb9.png" alt=""></td>
</tr>
<tr>
<td align="left">namespace</td>
<td align="left">Namespace name, which can be copied under the <strong>Namespace</strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">group</td>
<td align="left">Producer group name, which can be copied under the <strong>Group</strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">destination</td>
<td>Topic name, which can be copied under the <strong>Topic</strong> tab on the cluster details page in the console.</td>
</tr>
<tr>
<td align="left">subExpression</td>
<td align="left">A parameter used to set the message tag.</td>
</tr>
</tbody></table>

### Step 3. Configure channels
You can separately configure input and output channels as needed.
```java
import org.springframework.cloud.stream.annotation.Input;
import org.springframework.cloud.stream.annotation.Output;
import org.springframework.messaging.MessageChannel;

/**
* Custom channel binder
*/
public interface CustomChannelBinder {

	 /**
		* (Message producers) send messages
		* Bind the channel name in the configurations
		*/
	 @Output("Topic-send")
	 MessageChannel sendChannel();


	 /**
		* (Consumer 1) receives message 1
		* Bind the channel name in the configurations
		*/
	 @Input("Topic-test1")
	 MessageChannel testInputChannel1();

	 /**
		* (Consumer 2) receives message 2
		* Bind the channel name in the configurations
		*/
	 @Input("Topic-test2")
	 MessageChannel testInputChannel2();
}
```

### Step 4. Add annotations
Add annotations to the configuration class or startup class. If multiple binders are configured, specify them in the annotations.
```java
@EnableBinding({CustomChannelBinder.class})
```

### Step 5. Send messages

1. Inject `CustomChannelBinder` into the class that needs to send messages.
	```java
	@Autowired
	private CustomChannelBinder channelBinder;
	```
2. Use the corresponding output stream channel to send messages.
	```java
	Message<String> message = MessageBuilder.withPayload("This is a new message.").build();
	channelBinder.sendChannel().send(message);
	```

### Step 6. Consume messages
 ```java
 @Service
 public class TestStreamConsumer {
		 private final Logger logger = LoggerFactory.getLogger(DemoApplication.class);

		 /**
			* Listen on the channel in the binder configurations
			*
			* @param messageBody message content
			*/
		 @StreamListener("Topic-test1")
		 public void receive(String messageBody) {
				 logger.info("Receive1: Messages are received through the stream. messageBody = {}", messageBody);
		 }

		 /**
			* Listen on the channel in the binder configurations
			*
			* @param messageBody message content
			*/
		 @StreamListener("Topic-test2")
		 public void receive2(String messageBody) {
				 logger.info("Receive2: Messages are received through the stream. messageBody = {}", messageBody);
		 }
 }
 ```

For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-springcloud-stream-demo.zip) or [Spring Cloud Stream](https://github.com/alibaba/spring-cloud-alibaba/wiki/RocketMQ-en).

