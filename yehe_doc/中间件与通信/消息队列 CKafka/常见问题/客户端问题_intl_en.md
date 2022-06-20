### What should I do if no messages are displayed in the Kafka console when I test the client?

- If the "latest" option is used, the consumer can only get the last messages, and production needs to be ongoing so that the messages can be seen.
- Change to the "earliest" option for data consumption.

### What should I do if a production/consumption error occurs after a new client is connected to the service?

- Check whether telnet works. It might be a network issue. Check if Kafka and the producer are in the same network.
- Check whether the accessed “vip - port” is correctly configured.
- Check whether the topic allowlist is enabled. If yes, you need to configure the correct IP for access.




### How can I ensure that messages produced by the client are sequential in the same partition?

- If the topic has only one partition, messages will be stored in the order in which they are received by the server. This makes messages sequential in the partition.
- If a topic has multiple partitions, you can specify keys for messages of the same type on the producer. If such messages are sent with the same key, CKafka will select a partition to store them using the hash algorithm according to the key. As a partition can be listened on and consumed by only one consumer, messages will be consumed in the sending order.

A single producer produces messages to a single partition sequentially.



### How many connections does a client generally establish to brokers for message production?

For a single client instance (a producer object created with the `new` command), the total number of connections established between it and all servers ranges from one to n (n refers to the number of brokers).

Each Java producer manages TCP connections as follows:

1. The `Sender` thread will be initiated when a `KafkaProducer` instance is created to establish TCP connections to all brokers in `bootstrap.servers`.
2. After the metadata on the `KafkaProducer` instance is updated, TCP connections to all brokers in the cluster will be established again.
3. If no TCP connections are found when a producer sends a message to a broker, a connection will be established immediately.
4. If you set the `connections.max.idle.ms` parameter on the producer to a value above 0, TCP connections established in step 1 will be closed automatically. The parameter value is 9 minutes by default; that is, if no requests are sent through a TCP connection in 9 minutes, Kafka will automatically close the connection. If you set the parameter to -1, TCP connections established in step 1 cannot be closed and will become "zombie" connections.



### How do I know whether a message is successfully sent from a client?

After sending a message, most clients will return a `Callback` or `Future`. A successful callback indicates that the message is successfully sent.

You can also check whether a message is successfully sent in the console by the following methods:

- View the topic partition status to see the number of messages in each partition in real time.
- View the topic traffic monitoring data to see the traffic curve of the produced messages.

You can print the partition information returned by the `send` method to check whether the message is successfully sent:

```java
Future<RecordMetadata> future = producer.send(new ProducerRecord<>(topic, messageKey, messageStr));
RecordMetadata recordMetadata = future.get();
log.info("partition: {}", recordMetadata.partition());
log.info("offset: {}", recordMetadata.offset());
```

If the partition and offset information can be printed out, the currently sent message has been correctly saved on the server. At this time, you can use the message query tool to query the information of the relevant offset.
If the partition and offset information cannot be printed out, the message has not been saved on the server, and the client needs to retry.

![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)

[](id:leader_change)
### What is leader switch?
When a topic is created, the Kafka broker cluster specifies a leader for each partition, and the topic partitions are evenly distributed to each broker.
As time elapses, the partitions may become unevenly distributed across brokers, 
and the client may throw exceptions such as `BrokerNotAvailableError` and `NotLeaderForPartitionError` during the production or consumption process.
Generally, such issues occur because the partition leader has been switched as described in the following scenarios:

- When the broker where a partition leader resides cannot communicate with the broker controller due to some exceptions such as network disconnections, program crashes, and hardware failures, 
**leader switch** will occur, that is, the current topic partition leader will be replaced by a new leader elected from among the follower partitions.
- When the Kafka cluster sets `auto.leader.rebalance.enable = true` to automatically trigger rebalancing or when rebalancing is manually triggered by the increase/decrease of the number of brokers, 
**leader switch** will also occur due to partition rebalancing.

When the leader is switched due to the broker’s accidental disconnection:
- If the client has set `ack = all` and `min.insync.replicas > 1`, messages won’t get lost as they have been acknowledged by both the leader and follower partitions.
- If the client has set `ack = 1`, **some messages may get lost** as they may fail to be synced to the follower partitions within the specified `replica.lag.time.max.ms`.

Messages won’t get lost if the broker works normally and the leader is switched due to the rebalancing manually/automatically triggered by instance upgrade, the single- to multi-AZ deployment mode switchover, or instance migration. This is because:
- If the client has set `ack = all` and `min.insync.replicas > 1`, messages won’t get lost as they have been acknowledged by both the leader and follower partitions.
- If the client has set `ack = 1`, messages won’t get lost as the partition offset will be automatically synced when the leader is switched.

