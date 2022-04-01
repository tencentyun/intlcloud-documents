## Overview

This document describes how to use Spring Boot Starter to send and receive messages and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1112/43069).
- [You have installed JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-springboot-demo.zip)

## Directions

### Step 1. Add dependencies

Add dependencies to the `pom.xml` file.

```xml
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-spring-boot-starter</artifactId>
    <version>2.2.1</version>
</dependency>
```

### Step 2. Prepare configurations

Add configuration information to the configuration file.

```yaml
server:
  port: 8082

RocketMQ configuration information
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

  # User’s custom configurations
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
```

| Parameter          | Description                                                         |
| :------------ | :----------------------------------------------------------- |
| name-server   | Cluster access address, which can be obtained in the console by clicking **Access Address** in the **Operation** column of the cluster list on the **Cluster** page. |
| group         | Producer group name, which can be copied under the **Group** tab on the cluster details page.           |
| secret-key    | Role name, which can be copied on the **[Role Management]](https://console.cloud.tencent.com/tdmq/role)** page. |
| access-key    | Role token, which can be copied in the **Token** column on the**[Role Management](https://console.cloud.tencent.com/tdmq/role)** page. ![img](https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png) |
| namespace     | Namespace name, which can be copied under the **Namespace** tab on the cluster details page in the console.               |
| topic         | Topic name, which can be copied under the **Topic** tab on the cluster details page in the console.                  |
| subExpression | A parameter used to set the message tag.                                         |

### Step 3. Send messages

1. Inject **`RcoketMQTemplate`** into the class that needs to send messages.

   ```java
   @Value("${rocketmq.namespace}%${rocketmq.producer1.topic}")
   private String topic;  // Topic name, which is concatenated in the format of “full namespace name%topic name”.
   
   @Autowired
   private RocketMQTemplate rocketMQTemplate;
   ```

2. Send messages. The message body can be a custom object or a message object and is contained in the package `org.springframework.messaging`.

   ```java
   SendResult sendResult = rocketMQTemplate.syncSend(destination, message)
   ```

   ```java
   rocketMQTemplate.syncSend(destination, MessageBuilder.withPayload(message).build())
   ```

3. Below is a complete sample.

   ```java
   /**
    * Description: Message producer
    */
   @Service
   public class SendMessage {
   	// Use the full name of the topic, which can be either customized or concatenated in the format of “full namespace name%topic name”.
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
           // Spring Boot does not support passing tags by using the header. You must concatenate the topic name and tags with a colon “:” as in `topicName:tags`; otherwise, the topic has no tag for identification.
           String destination = StringUtils.isBlank(tags) ? topic : topic + ":" + tags;
           SendResult sendResult = rocketMQTemplate.syncSend(destination,
                   MessageBuilder.withPayload(message)
                           .setHeader(MessageConst.PROPERTY_KEYS, "yourKey")   // Specify the business key
                           .build());
           System.out.printf("syncSend1 to topic %s sendResult=%s %n", topic, sendResult);
       }
   }
   ```

>?Above is a sync sending sample. For more information on async sending and one-way sending, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-springboot-demo.zip) or [RocketMQ Spring](https://github.com/apache/rocketmq-spring).

### Step 4. Consume messages 

```java
@Service
@RocketMQMessageListener(
        consumerGroup = "${rocketmq.namespace}%${rocketmq.consumer1.group}",  // Consumer group in the format of “full namespace name%group name”
    	// Use the full name of the topic, which can be either customized or concatenated in the format of “full namespace name%topic name”.
        topic = "${rocketmq.namespace}%${rocketmq.consumer1.topic}",
        selectorExpression = "${rocketmq.consumer1.subExpression}" // Subscription expression. If this parameter is not configured, it means subscribing to all messages.
)
public class MessageConsumer implements RocketMQListener<String> {

    @Override
    public void onMessage(String message) {
        System.out.println("Tag1Consumer receive message:" + message);
    }
}
```

You can configure multiple consumers as needed, and the consumer configurations depend on your business requirements.

>?For the complete sample, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-springboot-demo.zip) or [RocketMQ Spring](https://github.com/apache/rocketmq-spring).

### Step 5. View consumption details

Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
![img](https://main.qcloudimg.com/raw/7187da67219534d767206553e2a383ab.png)

