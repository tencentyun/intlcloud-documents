## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Go as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed Go](https://golang.org/dl/).
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-go-sdk-demo.zip).

## Directions

1. Import the `pulsar-client-go` library in the client environment.
   1. Run the following command in the client environment to download the dependency package of the Pulsar client.
<dx-codeblock>
:::  shell
      go get -u "github.com/apache/pulsar-client-go/pulsar"
:::
</dx-codeblock>
   2. After the installation is completed, use the following code to import the client into your Go project file.
<dx-codeblock>
:::  go
      import "github.com/apache/pulsar-client-go/pulsar"
:::
</dx-codeblock>
2. Create a Pulsar client.
<dx-codeblock>
:::  go
   // Create a Pulsar client
   client, err := pulsar.NewClient(pulsar.ClientOptions{
       // Service access address
       URL: serviceUrl,
       // Authorize the role token
       Authentication:    pulsar.NewAuthenticationToken(authentication),
       OperationTimeout:  30 * time.Second,
       ConnectionTimeout: 30 * time.Second,
   })
   
   if err != nil {
       log.Fatalf("Could not instantiate Pulsar client: %v", err)
   }
   
   defer client.Close()
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
        <td style='text-align:left;'>serviceUrl</td>
        <td style='text-align:left;'>Cluster access address, which can be viewed and copied on the <a href='https://console.cloud.tencent.com/tdmq/cluster'><strong>Cluster Management</strong></a> page in the console.<br>
                <img
                src="https://qcloudimg.tencent-cloud.cn/raw/8612bb79a799375eb97d5e871e239372.png"
                referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>Authentication</td>
        <td style='text-align:left;'>Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.
                <img
                src="https://qcloudimg.tencent-cloud.cn/raw/65a283caa4b28d9fab366114ea8636b1.png" referrerpolicy="no-referrer"
                alt="img"></td>
    </tr>
    </tbody>
</table>
3. Create a producer.
<dx-codeblock>
:::  go
   // Create a producer with the client
   producer, err := client.CreateProducer(pulsar.ProducerOptions{
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
       Topic: "persistent://pulsar-mmqwr5xx9n7g/sdk_go/topic1",
   })
   
   if err != nil {
       log.Fatal(err)
   }
   defer producer.Close()
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic Management](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
</dx-alert>
4. Send a message.
<dx-codeblock>
:::  go
   // Send a message
   _, err = producer.Send(context.Background(), &pulsar.ProducerMessage{
       // Message content
       Payload: []byte("hello go client, this is a message."),
       // Business key
       Key: "yourKey",
       // Business parameter
       Properties: map[string]string{"key": "value"},
   })
:::
</dx-codeblock>
5. Create a consumer.
<dx-codeblock>
:::  go
   // Create a consumer with the client
   consumer, err := client.Subscribe(pulsar.ConsumerOptions{
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
       Topic:            "persistent://pulsar-mmqwr5xx9n7g/sdk_go/topic1",
       // Subscription name
       SubscriptionName: "topic1_sub",
       // Subscription mode
       Type:             pulsar.Shared,
   })
   if err != nil {
       log.Fatal(err)
   }
   defer consumer.Close()
:::
</dx-codeblock>

> ?
>
> - You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic Management](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
>   ![img](https://qcloudimg.tencent-cloud.cn/raw/4bb986f5e871cb9d72d9066ecf7eea66.png)
> - You need to enter the subscription name in the `subscriptionName` parameter, which can be viewed on the **Consumption Management** page.

6. Consume the message.
<dx-codeblock>
:::  go
   // Obtain the message
   msg, err := consumer.Receive(context.Background())
   if err != nil {
       log.Fatal(err)
   }
   // Simulate business processing
   fmt.Printf("Received message msgId: %#v -- content: '%s'\n",
              msg.ID(), string(msg.Payload()))
   
   // If the consumption is successful, return `ack`; otherwise, return `nack` or `ReconsumeLater` according to your business needs
   consumer.Ack(msg)
:::
</dx-codeblock>
7. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), click **Topic Management** > **Topic Name** to enter the **Consumption Management** page, and click the triangle below a subscription name to view the production and consumption records.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/206f52b4a67a3a5eba82309e0d5bc001.png)

>? The above is a brief introduction to the way of publishing and subscribing to messages. For more operations, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-go-sdk-demo.zip) or [Pulsar Go client](https://pulsar.apache.org/docs/en/client-libraries-go/).
