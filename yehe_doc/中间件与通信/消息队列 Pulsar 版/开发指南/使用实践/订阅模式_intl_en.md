In order to meet the needs of different use cases, TDMQ for Pulsar supports four subscription modes: exclusive, shared, failover, and key_shared.

![](https://qcloudimg.tencent-cloud.cn/raw/fbfd9ecad9703182e4a01412fe536d9f.png)

## Exclusive Mode

**Exclusive mode (default)**: A subscription can be associated with only one consumer. Only this consumer can receive all messages in the topic, and if it fails, consumption will stop.

In the exclusive subscription mode, only one consumer in a subscription can consume messages in the topic. If multiple consumers subscribe, an error will be reported. This mode is suitable for globally sequential consumption scenarios.

![](https://qcloudimg.tencent-cloud.cn/raw/eb8883954cc273035acaf72b75869955.png)
<dx-codeblock>
:::  java
// Construct a consumer
Consumer<byte[]> consumer = pulsarClient.newConsumer()
    // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
    .topic("persistent://pulsar-xxx/sdk_java/topic1")
    // You need to create a subscription on the topic details page in the console and enter the subscription name here
    .subscriptionName("sub_topic1")
    // Declare the exclusive mode as the consumption mode
    .subscriptionType(SubscriptionType.Exclusive)
    .subscribe();
:::
</dx-codeblock>

If multiple consumers are started, an error will be reported.
![](https://qcloudimg.tencent-cloud.cn/raw/a5643f95aa4fbbaa14f6fbdba2317066.png)

## Shared Mode

Messages are distributed to different consumers through a customizable round robin mechanism, with each message going to only one consumer. When a consumer is disconnected, any messages delivered to it but not acknowledged are redistributed to other active consumers.

![](https://qcloudimg.tencent-cloud.cn/raw/81bc25f19440fff8229a1fe716879f1e.png)
<dx-codeblock>
:::  java
// Construct a consumer
Consumer<byte[]> consumer = pulsarClient.newConsumer()
    // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
    .topic("persistent://pulsar-xxx/sdk_java/topic1")
    // You need to create a subscription on the topic details page in the console and enter the subscription name here
    .subscriptionName("sub_topic1")
    // Declare the shared mode as the consumption mode
    .subscriptionType(SubscriptionType.Shared)
    .subscribe();
:::
</dx-codeblock>

There can multiple consumers in the shared mode.
![](https://qcloudimg.tencent-cloud.cn/raw/b4d26ed3eb60d8828d281a48a7ddc771.png)

## Failover Mode

If there are multiple consumers, they will be sorted lexicographically, and the first consumer will be initialized to be the only one who can receive messages. When the first consumer is disconnected, all messages (unacknowledged and subsequent) will be distributed to the next consumer in the queue.

![](https://qcloudimg.tencent-cloud.cn/raw/7a2be3e1e0a9a60cca6a2f9facccf5a8.png)
<dx-codeblock>
:::  java
// Construct a consumer
Consumer<byte[]> consumer = pulsarClient.newConsumer()
    // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
    .topic("persistent://pulsar-xxx/sdk_java/topic1")
    // You need to create a subscription on the topic details page in the console and enter the subscription name here
    .subscriptionName("sub_topic1")
    // Declare the failover mode as the consumption mode
    .subscriptionType(SubscriptionType.Failover)
    .subscribe();
:::
</dx-codeblock>

There can be multiple consumers in the failover mode.
![](https://qcloudimg.tencent-cloud.cn/raw/78d1859db165635424337c1b31cfb87d.png)

## Key_Shared Mode

If there are multiple consumers, messages will be distributed by key, and messages with the same key will only be distributed to the same consumer.

![](https://qcloudimg.tencent-cloud.cn/raw/7a7a764e6769ca6b120c9708c3c31741.png)

<dx-codeblock>
:::  java
// Set the key when sending messages
MessageId msgId = producer.newMessage()
    // Message content
    .value(value.getBytes(StandardCharsets.UTF_8))
    // Set the key here. Messages with the same key will only be distributed to the same consumer.
    .key("youKey1")
    .send();
:::
</dx-codeblock>
    
<dx-codeblock>
:::  java
// Construct a consumer
Consumer<byte[]> consumer = pulsarClient.newConsumer()
    // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
    .topic("persistent://pulsar-xxx/sdk_java/topic1")
    // You need to create a subscription on the topic details page in the console and enter the subscription name here
    .subscriptionName("sub_topic1")
    // Declare the key_shared mode as the consumption mode
    .subscriptionType(SubscriptionType.Key_Shared)
    .subscribe();
:::
</dx-codeblock>

There can be multiple consumers in the key_shared mode.
![](https://qcloudimg.tencent-cloud.cn/raw/d74fc90e27c1b01c2132980bb8ec3088.png)
