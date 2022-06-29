## Scenarios

This document describes how to use open-source SDK to send and receive messages by using the SDK for Java as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-java-sdk-demo.zip)

## Directions

1. Introduce dependencies in a Java project and add the following dependencies to the `pom.xml` file. This document uses a Maven project as an example.
<dx-codeblock>
:::  xml
 <dependency>
		 <groupId>org.apache.pulsar</groupId>
		 <artifactId>pulsar-client</artifactId>
		 <version>2.7.2</version>
 </dependency>
:::
</dx-codeblock>

>? 
>- SDK 2.7.2 or later is recommended.
>- SDK 2.7.4 or later is recommended if you use the batch message sending and receiving feature (`BatchReceive`) of the client.

2. Create a Pulsar client.
<dx-codeblock>
:::  java
    PulsarClient pulsarClient = PulsarClient.builder()
                   // Service access address
                   .serviceUrl(SERVICE_URL)
                   // Role token
                   .authentication(AuthenticationFactory.token(AUTHENTICATION)).build();
:::
</dx-codeblock>
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>SERVICE_URL</td>
<td>Cluster access address, which can be viewed and copied on the <a href = "https://console.cloud.tencent.com/tdmq/cluster"><b>Cluster</b></a> page in the console.<br><img src = "https://qcloudimg.tencent-cloud.cn/raw/8612bb79a799375eb97d5e871e239372.png"></td>
</tr>
<tr>
<td>AUTHENTICATION</td>
<td>Role token, which can be copied in the **Token** column on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.<br><img src = "https://qcloudimg.tencent-cloud.cn/raw/65a283caa4b28d9fab366114ea8636b1.png"></td>
</tr>
</table>

3. Create a producer.
<dx-codeblock>
:::  java
   // Create a producer of the `byte[]` type
   Producer<byte[]> producer = pulsarClient.newProducer()
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
       .topic("persistent://pulsar-xxx/sdk_java/topic1").create();
:::
</dx-codeblock>

> ?You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.

4. Send the message.
<dx-codeblock>
:::  java
   // Send the message
   MessageId msgId = producer.newMessage()
       // Message content
       .value("this is a new message.".getBytes(StandardCharsets.UTF_8))
       // Business key
       .key("youKey")
       // Business parameter
       .property("mykey", "myvalue").send();
:::
</dx-codeblock>

5. Release the resources.
<dx-codeblock>
:::  java
   // Disable the producer
   producer.close();
   // Disable the client
   pulsarClient.close();
:::
</dx-codeblock>

6. Create a consumer.
<dx-codeblock>
:::  java
   // Create a consumer of the `byte[]` type (default type)
   Consumer<byte[]> consumer = pulsarClient.newConsumer()
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from the **Topic** page.
       .topic("persistent://pulsar-xxx/sdk_java/topic1")
       // You need to create a subscription on the topic details page in the console and enter the subscription name here
       .subscriptionName("sub_topic1")
       // Declare the exclusive mode as the consumption mode
       .subscriptionType(SubscriptionType.Exclusive)
       // Configure consumption starting at the earliest offset; otherwise, historical messages may not be consumed
       .subscriptionInitialPosition(SubscriptionInitialPosition.Earliest)
       // Subscription
       .subscribe();
:::
</dx-codeblock>

> ?
> - You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
> ![](https://qcloudimg.tencent-cloud.cn/raw/4bb986f5e871cb9d72d9066ecf7eea66.png)
> - You need to enter the subscription name in the `subscriptionName` parameter, which can be viewed on the **Consumption Management** page.

7. Consume the message.
<dx-codeblock>
:::  java
   // Receive a message corresponding to the current offset
   Message<byte[]> msg = consumer.receive();
   MessageId msgId = msg.getMessageId();
   String value = new String(msg.getValue());
   System.out.println("receive msg " + msgId + ",value:" + value);
   // Messages must be acknowledged after being received; otherwise, the offset will be held in the position of the current message, causing message heap.
   consumer.acknowledge(msg);
:::
</dx-codeblock>

8. Use the listener for consumption.
<dx-codeblock>
:::  java
   // Message listener
   MessageListener<byte[]> myMessageListener = (consumer, msg) -> {
       try {
           System.out.println("Message received: " + new String(msg.getData()));
           // Return `ack` as the acknowledgement
           consumer.acknowledge(msg);
       } catch (Exception e){
           // Return `nack` if the consumption fails
           consumer.negativeAcknowledge(msg);
       }
   };
   pulsarClient.newConsumer()
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from the **Topic** page.
       .topic("persistent://pulsar-mmqwr5xx9n7g/sdk_java/topic1")
       // You need to create a subscription on the topic details page in the console and enter the subscription name here
       .subscriptionName("sub_topic1")
       // Declare the exclusive mode as the consumption mode
       .subscriptionType(SubscriptionType.Exclusive)
       // Set the listener
       .messageListener(myMessageListener)
       // Configure consumption starting at the earliest offset; otherwise, historical messages may not be consumed
       .subscriptionInitialPosition(SubscriptionInitialPosition.Earliest)
       .subscribe();
:::
</dx-codeblock>

9. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), click **Topic** > **Topic Name** to enter the **Consumption Management** page, and click the triangle below a subscription name to view the production and consumption records.
![img](https://qcloudimg.tencent-cloud.cn/raw/206f52b4a67a3a5eba82309e0d5bc001.png)

>?The above is a brief introduction to the way of publishing and subscribing to messages. For more operations, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-java-sdk-demo.zip) or [Pulsar Java client](https://pulsar.apache.org/docs/en/client-libraries-java/).
