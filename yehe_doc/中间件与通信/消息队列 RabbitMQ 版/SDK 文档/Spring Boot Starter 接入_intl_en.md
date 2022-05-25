## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Spring Boot Starter as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources.](https://intl.cloud.tencent.com/document/product/1112/43069)
- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-springboot-amqp-demo.zip)


## Directions

### Step 1. Add dependencies

Add dependencies to the `pom.xml` file.
```xml
<!--rabbitmq-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

### Step 2. Prepare configurations

1. Add RabbitMQ configuration information to the configuration file (with the YML configuration as an example).
   ```yaml
   spring:
     rabbitmq:
     	# The host address can be obtained in the console. You can also use the RabbitMQ service address
       host: amqp-xx.rabbitmq.x.tencenttdmq.com
       port: 5672
       # Name of the role to be used, which can be obtained on the **Role Management** page in the console
       username: admin
       # Role key
       password: eyJrZXlJZ....
       # Full name of vhost, which can be obtained on the **Vhost** tab in the console
       virtual-host: amqp-xxx|Vhost
   ```


   | Parameter         | Description                                                         |
   | :----------- | :----------------------------------------------------------- |
   | host              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/8fabb0bfb1bc2a4144b3910b24ad9cb5.png) |
   | port              | Cluster access port, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. |
   | username          | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
   | password          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/81ca86f2f26f57999cc38fde8096ce22.png) |
   | virtual-host      | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/b3f6bd5245f04a73c7054640b6b1d390.png) |

2. Create a configuration file loading program (with the `Fanout exchange` as an example).
>?For the configurations of exchanges in other types, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-springboot-amqp-demo.zip).

```java
   /**
    * Fanout exchange configuration
    */
   @Configuration
   public class FanoutRabbitConfig {
   
       /**
        * Exchange
        */
       @Bean
       public FanoutExchange fanoutExchange() {
           return new FanoutExchange("fanout-logs", true, false);
       }
   
   
       /**
        * Message queue
        */
       @Bean
       public Queue fanoutQueueA() {
           return new Queue("ps_queue", true);
       }
   
       @Bean
       public Queue fanoutQueueB() {
           // You can use this method to bind a dead letter queue
           Map<String, Object> requestParam = new HashMap<>();
           requestParam.put("x-dead-letter-exchange", "my-deadLetter-exchange");
           // Set the message validity period
           requestParam.put("x-message-ttl", 60000);
           return new Queue("ps_queue1", true, false,true, requestParam);
       }
   
       /**
        * Bind the message queue to the exchange
        */
       @Bean
       public Binding bindingFanoutA() {
           return BindingBuilder.bind(fanoutQueueA())
                   .to(fanoutExchange());
       }
   
       @Bean
       public Binding bindingFanoutB() {
           return BindingBuilder.bind(fanoutQueueB())
                   .to(fanoutExchange());
       }
   }
```

| Parameter                     | Description                                                         |
| ---------------------- | ------------------------------------------------------------ |
| fanout-logs            | Name of the bound exchange, which can be obtained from the exchange list in the console.            |
| ps_queue               | Name of the first queue bound to the exchange, which can be obtained from the queue list in the console. |
| my-deadLetter-exchange | Dead letter exchange name, which can be obtained from the exchange list in the console.             |
| ps_queue1              | Name of the second queue bound to the exchange, which can be obtained from the queue list in the console. |

### Step 3. Send messages

Create and compile the message sending program `DemoApplication.java` and use `RabbitTemplate` to send message.

```java
@Autowired
private RabbitTemplate rabbitTemplate;

public String send() {
    String msg = "This is a new message.";
    // Send the message  
    // Parameter description: Parameter 1: Exchange name, which can be obtained from the exchange list in the console. Parameter 2: Routing key. Parameter 3: Message content
    rabbitTemplate.convertAndSend("direct_logs", "", msg);
    return "success";
}
```



### Step 4. Consume messages

Create and compile the message receiving program `FanoutReceiver.java` (with `Fanout exchange` as an example).

   ```java
@Component
public class FanoutReceiver {
	// Register a listener to listen on the specified message queue
    @RabbitHandler
    @RabbitListener(queues = "ps_queue")  // Name of the queue bound to the exchange, which can be obtained from the queue list in the console
    public void listenerPsQueue(String msg) {
        // Business processing...
        System.out.println("(ps_queue) receiver message. [" + msg + "]");
    }
}
   ```

### Step 5. View messages

To check whether messages are sent to TDMQ for RabbitMQ successfully, view the connected consumer status on the **[Cluster](https://console.cloud.tencent.com/tdmq/rabbit-cluster)** > **Queue** page in the console.

![img](https://qcloudimg.tencent-cloud.cn/raw/ca12348ded6a3a1449c1f18fb414f4c3.png)



>? For other samples, see [Spring AMQP](https://docs.spring.io/spring-amqp/reference/html/).
