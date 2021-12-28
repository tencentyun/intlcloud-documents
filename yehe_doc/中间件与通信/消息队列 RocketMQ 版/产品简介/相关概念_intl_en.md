This document lists the common concepts in TDMQ for RocketMQ and their definitions.

### General Message

General message is a basic message type, where a message is delivered to the specified topic by the producer and then consumed by the consumer subscribed to the topic. As general messages are not sequential in a topic, you can use multiple partitions to improve the message production/consumption efficiency, and they deliver the best performance when the throughput is huge.

### Sequential Message

- **Partitionally sequential message**: compared with general messages, partitionally sequential messages are sequential in a particular partition; that is, in the same partition, the consumer consumes messages strictly in the order they are delivered to the partition by the producer. This message type retains the partitioning mechanism to improve the performance while guaranteeing a certain sequence, but it cannot guarantee the sequence across different partitions.

- **Globally sequential message**: the most distinctive characteristic of the globally sequential message type is that messages are consumed strictly in the order they are delivered by the producer. Therefore, it uses a single partition to process messages, and you cannot customize the number of partitions. It has a lower performance than the other two message types.

### Dead Letter Message

A dead letter message is a message that cannot be consumed normally. When you create a subscription in TDMQ (to subscribe a consumer to a topic), a dead letter queue will be automatically created to process messages of this type.

### Retry Letter Queue

A retry letter queue is designed to ensure that messages are consumed normally. If no normal response is received after a message is consumed by the consumer for the first time, it will enter the retry letter queue, and after a specified number of failed retries, it will be delivered to the dead letter queue.

In actual scenarios, messages may not be processed promptly due to temporary issues such as network jitter and service restart, and the retry mechanism of the retry letter queue can be a good solution in this case.

### Dead Letter Queue

A dead letter queue is a special type of message queue used to centrally process messages that cannot be consumed normally. If a message cannot be consumed after a specified number of retries in the retry letter queue, TDMQ will determine that the message cannot be consumed under the current situation and deliver it to the dead letter queue.

In actual scenarios, messages may not be consumed due to service downtime or network disconnection. In this case, they will not be discarded immediately; instead, they will be persisted by the dead letter queue. After fixing the problem, you can create a consumer subscription to the dead letter queue to process such messages.

### Cluster Consumption

Cluster consumption is suitable for scenarios where each message only needs to be processed once.

### Broadcast Consumption

Broadcast consumption is suitable for scenarios where each message needs to be processed by each consumer in the cluster.