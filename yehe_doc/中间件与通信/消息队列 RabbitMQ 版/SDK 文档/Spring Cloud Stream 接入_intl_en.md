## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Spring Cloud Stream as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources.](https://intl.cloud.tencent.com/document/product/1112/43069)
- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo.](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-springcloud-stream-demo.zip)

## Directions

### Step 1. Add dependencies

Add `Stream RabbitMQ` dependencies to `pom.xml`.
```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-stream-rabbit</artifactId>
</dependency>
```

### Step 2. Prepare configurations

1. Configure the configuration file (with the configuration of a `direct` exchange as an example).
```yaml
spring:
  application:
    name: application-name
  cloud:
    stream:
      rabbit:
        bindings:
          # Output channel name
          output:
            # Producer configuration information
            producer:
              # Type of the exchange used by the producer. If the exchange name already exists, this type must be the same as that of the exchange type
              exchangeType: direct
              # It is used to specify a routing key expression
              routing-key-expression: headers["routeTo"] # This field indicates that the `routeTo` field in the header is used as the routing key
              queueNameGroupOnly: true
          # Input channel name
          input:
            # Consumer configuration information
            consumer:
              # Type of the exchange used by the consumer. If the exchange name already exists, this type must be the same as that of the exchange type
              exchangeType: direct
              # Routing keys bound to the consumer message queue
              bindingRoutingKey: info,waring,error
              # If the configuration is modified, the above routing keys will be processed
              bindingRoutingKeyDelimiter: ","  # This configuration item indicates to use commas (,) to separate the configured routing keys
              # Message acknowledgment mode. For more information, see `AcknowledgeMode`
              acknowledge-mode: manual
              queueNameGroupOnly: true
      bindings:
      	# Output channel name
        output: # Channel name
          destination: direct_logs # Name of the exchange to be used
          content-type: application/json
          default-binder: dev-rabbit
        # Input channel name
        input: # Channel name
          destination: direct_logs # Name of the exchange to be used
          content-type: application/json
          default-binder: dev-rabbit
          group: route_queue1 # Name of the message queue to be used
      binders:
        dev-rabbit:
          type: rabbit
          environment:
            spring:
              rabbitmq:
                host: 192.168.xxx.xxx # Cluster access address, which can be obtained in the **Operation** column on the **Cluster** page
                port: 5672
                username: admin # Role name
                password: password # Role key
                virtual-host: vhostnanme # Vhost name
```

| Parameter | Description |
| :---------------- | :----------------------------------------------------------- |
| bindingRoutingKey | Routing key bound to the consumer message queue, which is also the message routing rule and can be obtained in the **Binding Key** column in the binding list in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/554ac6e974817a9c066e7ec7d993c133.png) |
| direct_log        | Exchange name, which can be obtained from the exchange list in the console.                  |
| route_queue1      | Queue name, which can be obtained from the queue list in the console.                         |
| host              | Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/8b09343ada668e380641f03f786d5496.png) |
| port              | Cluster access port, which can be obtained from **Access Address** in the **Operation** column on the **Cluster** page. |
| username          | Role name, which can be copied on the **[Role Management](https://console.intl.cloud.tencent.com/tdmq/role)** page. |
| password          | Role key, which can be copied in the **Key** column on the **[Role Management](https://console.intl.intl.cloud.tencent.com/tdmq/role)** page. ![img](https://qcloudimg.tencent-cloud.cn/raw/b16cbf2b818a5faf318661db1d0468de.png) |
| virtual-host      | Vhost name in the format of **"cluster ID + \| + vhost name"**, which can be copied on the **Vhost** page in the console. ![img](https://qcloudimg.tencent-cloud.cn/raw/632be662b675293f4ffa9531c63ed911.png) |

2. Create a configuration file loading program.
   - OutputMessageBinding.java
```java
     public interface OutputMessageBinding {
         /**
          * Name of the channel to be used (output channel name)
          */
         String OUTPUT = "output";
     
         @Output(OUTPUT)
         MessageChannel output();
     }
```
   - InputMessageBinding.java
```java
     public interface InputMessageBinding {
     
         /**
          * Name of the channel to be used
          */
         String INPUT = "input";
     
         @Input(INPUT)
         SubscribableChannel input();
     }xxxxxxxxxx public interface InputMessageBinding {    /**     * Name of the channel to be used     */    String INPUT = "input";    @Input(INPUT)    SubscribableChannel input();}public interface OutputMessageBinding {    /**     * Name of the channel to be used (output channel name)     */    String OUTPUT = "output";    @Output(OUTPUT)    MessageChannel output();}
```

### Step 3. Send messages

Create and compile the message sending program `IMessageSendProvider.java`.
```java
// Import the configuration class
@EnableBinding(OutputMessageBinding.class)
public class MessageSendProvider {

    @Autowired
    private OutputMessageBinding outputMessageBinding;

    public String sendToDirect() {
        outputMessageBinding.output().send(MessageBuilder.withPayload("[info] This is a new message.[" + System.currentTimeMillis() + "]").setHeader("routeTo", "info").build());
        outputMessageBinding.output().send(MessageBuilder.withPayload("[waring] This is a new waring message.[" + System.currentTimeMillis() + "]").setHeader("routeTo", "waring").build());
        outputMessageBinding.output().send(MessageBuilder.withPayload("[error] This is a new error message.[" + System.currentTimeMillis() + "]").setHeader("routeTo", "error").build());
        return "success";
    }

    public String sendToFanout() {
        for (int i = 0; i < 3; i++) {
            outputMessageBinding.output().send(MessageBuilder.withPayload("This is a new message" + i).build());
        }
        return "success";
    }
}
```

Inject `MessageSendProvider` to the message sending class to send messages.

### Step 4. Consume messages

Create and compile the message consuming program `MessageConsumer.java`. **You can configure multiple channels to listen on different message queues.**
```java
@Service
@EnableBinding(InputMessageBinding.class)
public class MessageConsumer {

    @StreamListener(InputMessageBinding.INPUT)
    public void test(Message<String> message) throws IOException {
        Channel channel = (com.rabbitmq.client.Channel) message.getHeaders().get(AmqpHeaders.CHANNEL);
        Long deliveryTag = (Long) message.getHeaders().get(AmqpHeaders.DELIVERY_TAG);
        channel.basicAck(deliveryTag, false);
        String payload = message.getPayload();
        System.out.println(payload);
    }
}
```

### Step 5. View messages

To check whether messages are sent to TDMQ for RabbitMQ successfully, view the connected consumer status on the **[Cluster](https://console.cloud.tencent.com/tdmq/rabbit-cluster)** > **Queue** page in the console.

![img](https://qcloudimg.tencent-cloud.cn/raw/6ba8a057e8127ca8cd09f30e66d33c5e.png)

>? Above is a sample based on the pub/sub pattern of RabbitMQ, which can be configured as needed. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rabbitmq/tdmq-rabbitmq-springcloud-stream-demo.zip) or [Rabbit Producer Properties](https://github.com/spring-cloud/spring-cloud-stream-binder-rabbit#rabbit-prod-props).

