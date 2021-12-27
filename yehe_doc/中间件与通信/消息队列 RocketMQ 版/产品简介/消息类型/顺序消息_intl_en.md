This document describes the concept and usage of sequential message in TDMQ for RocketMQ.

## Concepts

Sequential messages include globally sequential messages and partitionally sequential messages:

- **Globally sequential message**: the most distinctive characteristic of the globally sequential message type is that messages are consumed strictly in the order they are delivered by the producer. Therefore, it uses a single partition to process messages, and you cannot customize the number of partitions. It has a lower performance.

- **Partitionally sequential message**: compared with general messages, partitionally sequential messages are sequential in a particular partition; that is, in the same partition, the consumer consumes messages strictly in the order they are delivered to the partition by the producer. This message type retains the partitioning mechanism to improve the performance while guaranteeing a certain sequence, but it cannot guarantee the sequence across different partitions.

The comparison between sequential message and general message is as follows:

| Message Type | Consumption Sequence | Performance | Use Cases |
| :----------- | :-------------------------------------------- | :--- | :----------------------------------------------------------- |
| General message | No sequence | Highest | Huge-Throughput use cases with no requirements for production and consumption sequence |
| Partitionally sequential message<br> | All messages in the same partition follow the First In, First Out (FIFO) rule | High | High-Throughput use cases that require publishing and consuming messages in the same partition in strict accordance with the FIFO rule |
| Globally sequential message<br> | All messages in the same topic follow the First In, First Out (FIFO) rule | Average | Average-Throughput use cases that require publishing and consuming all messages in strict accordance with the FIFO rule |


