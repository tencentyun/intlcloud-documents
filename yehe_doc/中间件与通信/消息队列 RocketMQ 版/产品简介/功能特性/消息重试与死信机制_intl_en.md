This document describes the message retry and dead letter mechanisms and their usages in TDMQ for RocketMQ.

## Feature Overview

When a message is consumed for the first time by a consumer and fails to get a normal response, TDMQ for RocketMQ will automatically retry delivering this message through the message retry mechanism until it is consumed successfully. When the number of retries reaches the specified value but the message is still not consumed successfully, retry will stop, and the message will be delivered to the dead letter queue.

After the message enters the dead letter queue, TDMQ for RocketMQ can no longer process it automatically. At this point, human intervention is generally required. You can write a dedicated client to subscribe to the dead letter queue to process such messages.

>?The broker will automatically retry in the cluster consumption mode but not the broadcast consumption mode.

The following results are considered as consumption failure, and the message will be retried accordingly:

1. The consumer returns `ConsumeConcurrentlyStatus.RECONSUME_LATER`.
2. The consumer returns `null`.
3. The consumer actively/passively throws an exception.

## Number of Retries


When a message needs to be retried in TDMQ for RocketMQ, set the "messageDelayLevel" parameter as follows to configure the number of retries and retry intervals:
```
messageDelayLevel=1s 5s 10s 30s 1m 2m 3m 4m 5m 6m 7m 8m 9m 10m 20m 30m 1h 2h
```

The number of retries and retry intervals have the following relationships:

| Retry Number | Interval Retry | Retry Number | Interval Retry |
| :--------- | :----------------------- | :--------- | :----------------------- |
| 1          | 1 second                      | 10         | 6 minutes                    |
| 2          | 5 seconds                      | 11         | 7 minutes                    |
| 3          | 10 seconds                     | 12         | 8 minutes                    |
| 4          | 30 seconds                     | 13         | 9 minutes                    |
| 5          | 1 minutes                    | 14         | 10 minutes                   |
| 6          | 2 minutes                    | 15         | 20 minutes                   |
| 7          | 3 minutes                    | 16         | 30 minutes                   |
| 8          | 4 minutes                    | 17         | 1 hour                    |
| 9          | 5 minutes                    | 18         | 2 hours                    |

## Usage

If you use `DefaultMQProducer` to send a general message, you can set the maximum number retries allowed if message delivery fails and develop the business retry logic flexibly based on the timeout period. The usage is as follows:
```java
/**Set the maximum number retries after message sending fails*/
public void setRetryTimesWhenSendFailed(int retryTimesWhenSendFailed) {
    this.retryTimesWhenSendFailed = retryTimesWhenSendFailed;
}

/**Send the message synchronously and specify the timeout period*/
public SendResult send(Message msg,
                    long timeout) throws MQClientException, RemotingException, MQBrokerException, InterruptedException {
    return this.defaultMQProducerImpl.send(msg, timeout);
}

```

Below is the sample code of retrying for three times when the producer fails to send a message within 3s:
```java
/**Send the message synchronously and retry three times if the message fails to be sent within 3s*/
DefaultMQProducer producer = new DefaultMQProducer("DefaultProducerGroup");
producer.setRetryTimesWhenSendFailed(3);
producer.send(msg, 3000L);
```

