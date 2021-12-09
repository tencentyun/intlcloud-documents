## Overview

This document describes how to download the demo, perform a simple test, and run a client after you purchase the TDMQ for Pulsar and CVM services.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have [purchased a CVM instance](https://buy.cloud.tencent.com/cvm).

## Directions

1. Download the demo [here](https://tdmq-1300957330.cos.ap-guangzhou.myqcloud.com/TDMQ-demo/tdmq-pulsar-java-client.zip) and configure relevant parameters.

   **Add Maven dependencies**
   Add Maven dependencies as instructed in [Pulsar Java client](http://pulsar.apache.org/docs/en/client-libraries-java/).
   <dx-codeblock>
   :::  xml

```xml
<!-- in your <properties> block -->
<pulsar.version>2.7.1</pulsar.version>
<!-- in your <dependencies> block -->
<dependency>
	<groupId>org.apache.pulsar</groupId>
	<artifactId>pulsar-client</artifactId>
	<version>${pulsar.version}</version>
</dependency>
```

:::
</dx-codeblock>

   **Create a client**	 
<dx-tabs>
::: Access sample for cluster on v2.7.1 or above
<dx-codeblock>

:::  java

// One Pulsar client corresponds to one client connection
// In principle, one process corresponds to one client. Try to avoid repeated creation, as this may consume resources
// For the best practice of clients and producers/consumers, see [Client Connection and Producer/Consumer](https://cloud.tencent.com/document/product/1179/58090)

PulsarClient client = PulsarClient.builder()
        // Replace it with the cluster access address displayed on the **Cluster Management** page
        .serviceUrl("http://pulsar-..tencenttdmq.com:8080")
        // Replace it with the role token displayed on the **Role Management** page
        .authentication(AuthenticationFactory.token("eyJr"))
        .build(); 

System.out.println(">> pulsar client created.");

:::
</dx-codeblock>

- `serviceUrl` is the access address, which can be viewed and copied on the **[Cluster Management](https://console.cloud.tencent.com/tdmq/cluster)** page in the console.

  ![](https://main.qcloudimg.com/raw/a1bbc4b3857903e04f16fc46d9194c57.png)

- `token` is the role token, which can be copied on the **Role Management** page.

<dx-alert infotype="notice" title="">
Token leakage may lead to data leakage; therefore, you should keep your token confidential.
</dx-alert>

:::
::: Access sample for cluster on v2.6.1

<dx-codeblock>

:::  java

PulsarClient client = PulsarClient.builder()
    .serviceUrl("pulsar://...:6000/")// Access address, which can be copied from the access point list in **Cluster Management**
    .listenerName("custom:pulsar-/vpc-/subnet-")// Replace the value of `custom:` with the route ID in the access point list in **Cluster Management**
    .authentication(AuthenticationFactory.token("eyJr"))// Replace it with the role token displayed on the **Role Management** page
    .build();
System.out.println(">> pulsar client created.");

:::
</dx-codeblock>

- `serviceUrl` is the access address, which can be viewed and copied on the **[Cluster Management](https://console.cloud.tencent.com/tdmq/cluster)** page in the console.
- `listenerName` is the `custom:` plus the route ID (NetModel), which can be viewed and copied on the **[Cluster Management](https://console.cloud.tencent.com/tdmq/cluster)** page in the console.
  ![](https://main.qcloudimg.com/raw/521d7585bb872e8150fc0277da1fe894.png)
- `token` is the role token, which can be copied on the **Role Management** page.



<dx-alert infotype="notice" title="">
Token leakage may lead to data leakage; therefore, you should keep your token confidential.
</dx-alert>
:::
</dx-tabs>

 **Create a consumer process**

```java
Consumer<byte[]> consumer = client.newConsumer()
                // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
                .topic("persistent://pulsar-****/namespace/topicName")
                // You need to create a subscription on the topic details page in the console and enter the subscription name here
                .subscriptionName("subscriptionName")
                // Declare the exclusive mode as the consumption mode
                .subscriptionType(SubscriptionType.Exclusive)
                // Configure consumption starting at the earliest offset; otherwise, historical messages may not be consumed
                .subscriptionInitialPosition(SubscriptionInitialPosition.Earliest)
                .subscribe();
        System.out.println(">> pulsar consumer created.");
```

 <dx-alert infotype="explain" title="">

- You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic Management](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
  ![](https://main.qcloudimg.com/raw/a2e32b311b825df9798b8c98df7c3416.png)
- You need to enter the subscription name in the `subscriptionName` parameter, which can be viewed on the **Consumption Management** page.
  </dx-alert>



   **Create a producer process**

```java
Producer<byte[]> producer = client.newProducer()
                // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
                .topic("persistent://pulsar-****/namespace/topicName")
                .create();
        System.out.println(">> pulsar producer created.");
```

<dx-alert infotype="explain" title="">
You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic Management](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
</dx-alert>



   **Produce a message**

```java
for (int i = 0; i < 5; i++) {
            String value = "my-sync-message-" + i;
            // Send a message
            MessageId msgId = producer.newMessage().value(value.getBytes()).send();
            System.out.println("deliver msg " + msgId + ",value:" + value);
        }
        // Disable the producer
        producer.close();
```

   **Consume a message**

```java
for (int i = 0; i < 5; i++) {
            // Receive a message corresponding to the current offset
            Message<byte[]> msg = consumer.receive();
            MessageId msgId = msg.getMessageId();
            String value = new String(msg.getValue());
            System.out.println("receive msg " + msgId + ",value:" + value);
            // Messages must be acknowledged after being received; otherwise, the offset will be held in the position of the current message, and consumption cannot continue
            consumer.acknowledge(msg);
        }
```

2. Run the `mvn clean package` command in the directory of `pom.xml` or use the features of the IDE to package the entire project and generate an executable JAR file in the `target` directory.
   <img src="https://main.qcloudimg.com/raw/8a4808ea722fe0b19ad1cd91666088c7.png" width="450px"> 

3. After successful execution, upload the JAR file to the CVM instance. For directions, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

4. Log in to the CVM instance and enter the directory of the JAR file just uploaded, where you can see that the file has been uploaded to the CVM instance.
   ![](https://main.qcloudimg.com/raw/677e840a8f28802d217b38acc9745d85.png)
   Run the `java -jar tdmq-demo-1.0.0.jar` command to run the demo and view the execution logs.
   ![](https://main.qcloudimg.com/raw/cd31ccff67fe1f5fa926e383151c5aae.png)

5. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), click **Topic Management** > **Topic Name** to enter the **Consumption Management** page, and click the triangle below a subscription name to view the production and consumption records.

   ![](https://main.qcloudimg.com/raw/da7ce2bc5ac606c91982efecdb3b53bb.png)

6. Enter the **[Message Query](https://console.cloud.tencent.com/tdmq/message)** page to view the message trace after running the demo.
   ![](https://main.qcloudimg.com/raw/d5e09b9c789749b28182b62a501797ca.png)
   The message trace is as follows:
   ![](https://main.qcloudimg.com/raw/eaa0125f6dcd7675e367c4e3e069c915.png)
