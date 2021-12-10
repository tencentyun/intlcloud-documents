A retry letter topic is designed to ensure that messages are consumed normally. If no normal response is received after a message is consumed by the consumer for the first time, it will enter the retry letter topic, and after a specified number of failed retries, it will be delivered to the dead letter topic.

After the message enters the dead letter topic, TDMQ for Pulsar can no longer process it automatically. At this point, human intervention is generally required. You can write a dedicated client to subscribe to the dead letter topic to process such messages.

## Automatic Retry

### Concepts

**Retry letter topic**: it corresponds to a subscription name (the unique identifier of a subscriber group) and exists in TDMQ for Pulsar in the form of topic. After you create a subscription, a retry letter topic will be automatically created and independently implement the message retry mechanism.

This topic is named as follows:

- For clusters on v2.7.1 or above: [subscription name]-RETRY
- For clusters on v2.6.1: [subscription name]-retry

### How it works

After the consumer you create uses a subscription name to subscribe to a topic in shared mode, if the `enableRetry` attribute is enabled, the retry letter topic corresponding to the subscription name will be automatically subscribed to.

>?Only the shared mode supports the automatic retry and dead letter mechanisms, while exclusive and failover modes don't.

Here, a Java client is used as an example. The `sub1` subscription to `topic1` is created, and the client uses the `sub1` subscription name to subscribe to `topic1` and enables `enableRetry` as shown below:

```java
Consumer consumer = client.newConsumer()
    .topic("persistent://1******30/my-ns/topic1")
    .subscriptionType(SubscriptionType.Shared)// Only the shared consumption mode supports the retry and dead letter mechanisms
    .enableRetry(true)
    .subscriptionName("sub1")
    .subscribe();
```

At this point, the `sub1` subscription to `topic1` forms a delivery model with the retry mechanism, and `sub1` will automatically subscribe to the retry letter topic created automatically during subscription creation (which can be found in the topic list in the console). If no ack is received from the consumer after a message in `topic1` is delivered for the first time, the message will be automatically delivered to the retry letter topic, and as the consumer has subscribed to this topic automatically, the message will subsequently be consumed again according to particular [retry rules](#Retry-rules). If it still fails to be consumed after the specified maximum number of retries, it will be delivered to the dead letter topic and wait for manual processing.

>?If the subscription is automatically created by the client, you can click **[Topic Management](https://console.cloud.tencent.com/tdmq/topic)** > **More** > **View Subscription** in the console to enter the **Subscription Management** page and manually recreate the retry letter and dead letter topics.
>![](https://qcloudimg.tencent-cloud.cn/raw/3392efec6a06176c639fa387a8fc5ba3.png)

### Custom parameter settings

A set of retry and dead letter parameters are configured for TDMQ for Pulsar by default as follows:
<dx-tabs>
::: Clusters\son\sv2.7.1\sor\sabove

- Specify the number of retries as 16 (after 16 failed retries, the message will be delivered to the dead letter topic at the 17th time)
- Specify the retry letter topic as `[subscription name]-RETRY`
- Specify the dead letter topic as `[subscription name]-DLQ`
  :::
  ::: Clusters\son\sv2.6.1
- Specify the number of retries as 16 (after 16 failed retries, the message will be delivered to the dead letter topic at the 17th time)
- Specify the retry letter topic as `[subscription name]-retry`
- Specify the dead letter topic as `[subscription name]-dlq`
  :::
  </dx-tabs>

You can call the `deadLetterPolicy` API to customize these parameters. Below is the sample code:

```java
Consumer<byte[]> consumer = pulsarClient.newConsumer()
    .topic("persistent://pulsar-****")
    .subscriptionName("sub1")
	.subscriptionType(SubscriptionType.Shared)
    .enableRetry(true)// Enable consumption retry
    .deadLetterPolicy(DeadLetterPolicy.builder()
          .maxRedeliverCount(maxRedeliveryCount)// Specify the maximum number of retries
          .retryLetterTopic("persistent://my-property/my-ns/sub1-retry")// Specify the retry letter topic
          .deadLetterTopic("persistent://my-property/my-ns/sub1-dlq")// Specify the dead letter topic
          .build())
    .subscribe();
```


### Retry rules[](id:Retry-rules)

The retry rules are implemented through the `reconsumerLater` API in three modes:

```java
 // Specify any delay time
 consumer.reconsumeLater(msg, 1000L, TimeUnit.MILLISECONDS);
 // Specify the delay level
 consumer.reconsumeLater(msg, 1);
 // Increase with level
 consumer.reconsumeLater(msg);
```

- **Mode 1: specify any delay time**. Enter the delay time in the second parameter and specify the time unit in the third parameter. The delay time is in the same value range as delayed message, which is 1–864,000 seconds.

- **Mode 2: specify any delay level (for existing users of the Tencent Cloud SDK only)**. Its implementation effect is basically the same as that of mode 1, but it allows you to manage the delay time in distributed systems more easily. The delay level is as described below:
  1. The second parameter in `reconsumeLater(msg, 1)` is the message level.
  2. By default, the `MESSAGE_DELAYLEVEL = "1s 5s 10s 30s 1m 2m 3m 4m 5m 6m 7m 8m 9m 10m 20m 30m 1h 2h"` constant determines the respective delay time of each level; for example, level 1 corresponds to 1s and level 3 to 10s. You can customize the default value if it cannot meet your actual business needs.

- **Mode 3: increase with level (for existing users of the Tencent Cloud SDK only)**. Different from the implementation effect of the above two modes, this mode adopts backoff retry; that is, the retry interval is 1s after the first failure, 5s after the second failure, and so on. The more the failures, the longer the interval. The specific retry interval is also determined by the `MESSAGE_DELAYLEVEL` parameter as described in mode 2.
  This retry mechanism often has more practical applications in business scenarios. If consumption fails, the service generally will not be recovered immediately, therefore using such progressive retry mechanism makes more sense.

>!If you use the SDK provided by the Pulsar community, the delay level and increase with level modes are not supported.

### Attributes of retry message

A retry message carries the following attributes:

```json
{
  REAL_TOPIC="persistent://my-property/my-ns/test, 
  ORIGIN_MESSAGE_ID=314:28:-1, 
  RETRY_TOPIC="persistent://my-property/my-ns/my-subscription-retry, 
  RECONSUMETIMES=16
}
```

- `REAL_TOPIC`: original topic
- `ORIGIN_MESSAGE_ID`: ID of the initially produced message
- `RETRY_TOPIC`: retry letter topic
- `RECONSUMETIMES`: number of retries performed for the message



### Flow of retry message ID

The message ID flow process is as shown below, and you can analyze relevant logs based on it.

```
Original consumption: msgid=1:1:0:1
1st retry: msgid=2:1:-1
2nd retry: msgid=2:2:-1
3rd retry: msgid=2:3:-1
.......
16th retry: msgid=2:16:0:1
17th write to the dead letter topic: msgid=3:1:-1
```



### Complete sample code

Below is the sample code for implementing the complete message retry mechanism in TDMQ for Pulsar:

**Subscribing to topic**

```java
Consumer<byte[]> consumer1 = client.newConsumer()
		.topic("persistent://pulsar-****")
		.subscriptionName("my-subscription")
		.subscriptionType(SubscriptionType.Shared)
		.enableRetry(true)// Enable consumption retry
		//.deadLetterPolicy(DeadLetterPolicy.builder()
		//         .maxRedeliverCount(maxRedeliveryCount)
		//         .retryLetterTopic("persistent://my-property/my-ns/my-subscription-retry")// Specify the retry letter topic
		//         .deadLetterTopic("persistent://my-property/my-ns/my-subscription-dlq")// Specify the dead letter topic
		//         .build())
		.subscribe();
```

**Executing consumption**

```java
while (true) {
	  Message msg = consumer.receive();
	  try {
		    // Do something with the message
		    System.out.printf("Message received: %s", new String(msg.getData()));
		    // Acknowledge the message so that it can be deleted by the message broker
		    consumer.acknowledge(msg);
	  } catch (Exception e) {
		    // select reconsume policy
		    consumer.reconsumeLater(msg, 1000L, TimeUnit.MILLISECONDS);
		    //consumer.reconsumeLater(msg, 1);
		    //consumer.reconsumeLater(msg);
	  }
}
```

## Active Retry

If a consumer fails to consume a message at a certain time point and wants to consume the message again, it can send an nack to the TDMQ for Pulsar server, which will send the message to it again. This retry method will not generate new messages, so you cannot customize the retry interval.

Below is the sample code in Java for active retry:

```java
while (true) {
    Message msg = consumer.receive();
    try {
        // Do something with the message
        System.out.printf("Message received: %s", new String(msg.getData()));
        // Acknowledge the message so that it can be deleted by the message broker
        consumer.acknowledge(msg);
    } catch (Exception e) {
        // Message failed to process, redeliver later
        consumer.negativeAcknowledge(msg);
    }
    consumer.negativeAcknowledge(msg);
}
```
