## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for C++ as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed GCC](https://gcc.gnu.org/install/)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-cpp-sdk-demo.zip)

## Directions

1. Prepare the environment.
   1. Install the Pulsar C++ client in the client environment as instructed in [Pulsar C++ client](https://pulsar.apache.org/docs/en/client-libraries-cpp/).
   2. Introduce the files and dynamic libraries that are related to the Pulsar C++ client to the project.
2. Create a client.
<dx-codeblock>
:::  c++
   // Client configuration information
   ClientConfiguration config;
   // Set the role token
   AuthenticationPtr auth = pulsar::AuthToken::createWithToken(AUTHENTICATION);
   config.setAuth(auth);
   // Create a client
   Client client(SERVICE_URL, config);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>SERVICE_URL</td>
        <td style='text-align:left;'>Cluster access address, which can be viewed and copied on the <a
                href='https://console.cloud.tencent.com/tdmq/cluster'><strong>Cluster</strong></a> page in the console.<br><img
                src="https://qcloudimg.tencent-cloud.cn/raw/8612bb79a799375eb97d5e871e239372.png"
                referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>AUTHENTICATION</td>
        <td style='text-align:left;'>Role token, which can be copied in the <strong>Token</strong> column on the <strong><a
                href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.<img
                src="https://qcloudimg.tencent-cloud.cn/raw/65a283caa4b28d9fab366114ea8636b1.png" referrerpolicy="no-referrer"
                alt="img"></td>
    </tr>
    </tbody>
</table>
3. Create a producer.
<dx-codeblock>
:::  c++
// Producer configurations
ProducerConfiguration producerConf;
producerConf.setBlockIfQueueFull(true);
producerConf.setSendTimeout(5000);
// Producer
Producer producer;
// Create a producer
Result result = client.createProducer(
    // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
    "persistent://pulsar-xxx/sdk_cpp/topic1",
    producerConf,
    producer);
if (result != ResultOk) {
    std::cout << "Error creating producer: " << result << std::endl;
    return -1;
}
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
</dx-alert>
4. Send the message.
<dx-codeblock>
:::  c++
   // Message content
   std::string content = "hello cpp client, this is a msg";
   // Create a message object
   Message msg = MessageBuilder().setContent(content)
       .setPartitionKey("mykey")  // Business key
       .setProperty("x", "1")   // Set message parameters
       .build();
   // Send the message
   Result result = producer.send(msg);
   if (result != ResultOk) {
       // The message failed to be sent
       std::cout << "The message " << content << " could not be sent, received code: " << result << std::endl;
   } else {
       // The message was successfully sent
       std::cout << "The message " << content << " sent successfully" << std::endl;
   }
:::
</dx-codeblock>
5. Create a consumer.
<dx-codeblock>
:::  c++
   // Consumer configuration information
   ConsumerConfiguration consumerConfiguration;
   consumerConfiguration.setSubscriptionInitialPosition(pulsar::InitialPositionEarliest);
   // Consumer
   Consumer consumer;
   // Subscribe to a topic
   Result result = client.subscribe(
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
       "persistent://pulsar-xxx/sdk_cpp/topic1",
       // Subscription name
       "sub_topic1",
       consumerConfiguration,
       consumer);
   
   if (result != ResultOk) {
       std::cout << "Failed to subscribe: " << result << std::endl;
       return -1;
   }
:::
</dx-codeblock>
> ?
>
> - You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
>   ![img](https://qcloudimg.tencent-cloud.cn/raw/4bb986f5e871cb9d72d9066ecf7eea66.png)
> - You need to enter the subscription name in the `subscriptionName` parameter, which can be viewed on the **Consumption Management** page.
6. Consume the message.
<dx-codeblock>
:::  c++
   Message msg;
   // Obtain the message
   consumer.receive(msg);
   // Simulate the business processing logic
   std::cout << "Received: " << msg << "  with payload '" << msg.getDataAsString() << "'" << std::endl;
   // Return `ack` as the acknowledgement
   consumer.acknowledge(msg);
   // Return `nack` if the consumption fails, and the message will be delivered again
   // consumer.negativeAcknowledge(msg);
:::
</dx-codeblock>
7. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), click **Topic** > **Topic Name** to enter the **Consumption Management** page, and click the triangle below a subscription name to view the production and consumption records.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/206f52b4a67a3a5eba82309e0d5bc001.png)

>?The above is a brief introduction to the way of publishing and subscribing to messages. For more operations, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-cpp-sdk-demo.zip) or [Pulsar C++ client](https://pulsar.apache.org/docs/en/client-libraries-cpp/).
