
In TDMQ, messages can be divided into the following types according to their characteristics and use cases:

| Message Type | Consumption Sequence | Performance | Use Cases | 
| ----- | ----- | ----- | ----- |
| General message | No sequence | Highest | Huge-Throughput use cases with no requirements for production and consumption sequence | 
| Partitionally sequential message | All messages in the same partition follow the First In, First Out (FIFO) rule | High | High-Throughput use cases that require message sequence in the same partition but not across different partitions |
| Globally sequential message | All messages in the same topic follow the First In, First Out (FIFO) rule | Average | Average-Throughput use cases that require global message sequence with only one partition |
| Dead letter message | -  | - | Messages that cannot be consumed normally | 

### General Message

General message is a basic message type, where a message is delivered to the specified topic by the producer and then consumed by the consumer subscribed to the topic. As general messages are not sequential in a topic, you can use multiple partitions to improve the message production/consumption efficiency, and they deliver the best performance when the throughput is huge.

### Partitionally Sequential Message

Compared with general messages, partitionally sequential messages are sequential in a particular partition; that is, in the same partition, the consumer consumes messages strictly in the order they are delivered to the partition by the producer. This message type retains the partitioning mechanism to improve the performance while guaranteeing a certain sequence, but it cannot guarantee the sequence across different partitions.

### Globally Sequential Message

The most distinctive characteristic of the globally sequential message type is that messages are consumed strictly in the order they are delivered by the producer. Therefore, it uses a single partition to process messages, and you cannot customize the number of partitions. It has a lower performance than the other two message types.

### Dead Letter Message

A dead letter message is a message that cannot be consumed normally. When you create a subscription in TDMQ for Pulsar (to subscribe a consumer to a topic), a dead letter topic will be automatically created to process messages of this type.


