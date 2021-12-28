### How do I choose an appropriate number of CKafka replicas?

We recommend you select two or three replicas for data storage when creating a topic to ensure data reliability. A created topic has two replicas by default. If your business requires higher availability, you can select three replicas. If you need more replicas, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. When creating a topic, you can select the number of replicas as shown below:

![topic](https://main.qcloudimg.com/raw/08bf05cf16f28acecf0534c1d96a0391.png)

To improve data security, CKafka has banned the creation of single-replica topics currently. If you have a single-replica topic in your account, please migrate it as follows:
1. Create a topic, select the same partition parameter, and select "dual-replica".
2. Produce messages in the new topic while the existing single-replica topic continues to be consumed.
3. Modify the consumer configuration after consumption is completed to subscribe to the new topic for consumption.

### Why can messages still be queried after the message retention period set for the topic elapsed?

1. A timestamp field and timestamp types are added to messages. Currently, two timestamp types are supported: `CreateTime` and `LogAppendTime`. The former indicates the time when the message is created by the producer, and the latter indicates the time when the broker receives the message. If the timestamp data of the time when a client produces a message is invalid, data deletion on the broker server will be affected.
2. If there are too many partitions in the topic and too little message data, and only one log segment file exists in the partition, messages will not be deleted.
3. The log deletion task checks whether the current log size exceeds the set threshold, i.e., 1 GB per segment. If the maximum timestamp data in the log segment is still within the retention period, messages will not be deleted.

### Why is the number of topics (total number of partitions) limited?

A high number of topics (total number of partitions) in Kafka will compromise the cluster performance and stability.

As the number of partitions that a server can sustain is limited, if you want more partitions, you need to add more nodes, which incur more fees. Kafka's storage and coordination mechanisms work by partition. If there are too many partitions, storage fragmentation will be severe, random writes on individual servers will increase, the efficiency of leader switch in the cluster will decrease, controller node failover will slow down, and other problems may occur, which lower the overall cluster performance and stability.

### What is the relationship between the number of topics and the number of partitions?

CKafka uses partition as an allocation unit.

Total number of partitions = topic A * number of replicas + topic B * number of replicas + ... + topic N * number of replicas.

Replicas are also counted into the total number of partitions. For example, if you create 1 topic with 6 partitions and 2 replicas for each partition, then you have a total of 12 partitions (1 * 6 * 2).

- Partition count: it is a concept in physical partition, where one topic can contain one or more partitions.
- Replica count: the number of partition replicas is used to ensure the high availability of the partition. To ensure data reliability, creating a single-replica topic is not supported. Two replicas are enabled by default.

