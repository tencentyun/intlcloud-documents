

To meet the needs in different scenarios, TDMQ for Pulsar provides multiple subscription modes, which can be combined flexibly to create more possibilities:
- If you want to implement the traditional "publish-subscribe" pattern, you can let each consumer have a unique subscription name (exclusive mode).
- If you want to implement the traditional "message queue" pattern, you can make multiple consumers use the same subscription name (shared or failover mode).
- If you want to implement both of the above at the same time, you can make some consumers use the exclusive mode and other consumers use other modes.

![](https://main.qcloudimg.com/raw/ab3396672d1e49642485686f2df3f479.png)

## Exclusive Mode
In this mode, if two or more consumers attempt to subscribe to a topic in the same way, they will receive an error. This mode is suitable for globally sequential consumption scenarios.
```java
 Consumer<byte[]> consumer1 = client.newConsumer()
                .subscriptionType(SubscriptionType.Exclusive)
                .topic(topic)
                .subscriptionName(groupName)
                .subscribe();
// Consumer 1 was started successfully
 Consumer<byte[]> consumer2 = client.newConsumer()
                .subscriptionType(SubscriptionType.Exclusive)
                .topic(topic)
                .subscriptionName(groupName)
                .subscribe();
// Consumer 2 failed to be started
```

## Failover Mode
In this mode, consumers are sorted lexicographically, and the first consumer is initialized to be the only one who can receive messages. 
```java
 Consumer<byte[]> consumer1 = client.newConsumer()
                .subscriptionType(SubscriptionType.Failover)
                .topic(topic)
                .subscriptionName(groupName)
                .subscribe();
// Consumer 1 was started successfully
 Consumer<byte[]> consumer2 = client.newConsumer()
                .subscriptionType(SubscriptionType.Failover)
                .topic(topic)
                .subscriptionName(groupName)
                .subscribe();
// Consumer 2 was started successfully
```
When the master consumer is disconnected, all messages (unacknowledged and subsequent) will be distributed to the next consumer in the queue.

## Shared Mode
Messages are distributed to different consumers through a customizable round robin mechanism, with each message going to only one consumer. When a consumer is disconnected, any messages delivered to it but not acknowledged are redistributed to other active consumers.
```java
 Consumer<byte[]> consumer = client.newConsumer()
                .subscriptionType(SubscriptionType.Shared)
                .topic(topic)
                .subscriptionName(groupName)
                .subscribe();
```
