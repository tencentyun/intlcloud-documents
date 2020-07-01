

### Broker

Broker 即代理服务器，是服务的提供者。
在消息队列 CKafka 中，Broker 是一个单独的 CKafka Server，主要用来接收生产者发送的消息、分配 Offset、并将消息保存到磁盘中。同时，Broker 也接收来自消费者和其他 Broker 的请求，根据请求类型进行相应处理并返回响应。



### CKafka

参见 [消息队列 CKafka](#CKafka1)



### 分区

分区（Partition）是用于存储消息的物理概念，是 CKafka 水平扩展性能的基础，您可以通过增加服务器，并在服务器上分配分区的方式，增加 CKafka 的并行处理能力。

- 每个 Topic 可以划分成多个分区，且每个 Topic 至少有一个分区。
- 同一 Topic 下的不同分区包含不同的消息。
- 同一 Topic 的不同分区会分配给不同的 Broker。



### Offset

Offset 是消息在分区（Partition）的唯一序号。



### 副本

副本（Replica）是消息的冗余备份，每个分区可以有多个副本，每个副本包含的消息是一样的（在同一时刻，副本之间并不完全一样，这依赖同步机制）。
在消息队列 CKafka 中每个分区至少有双副本，保障服务的高可用。



### 消费者分组

消费者分组（Consumer Group）是消费者的集合，在 CKafka 中，多个 Consumer 可以组成一个 Consumer Group，且一个 Consumer 只能属于一个 Consumer Group。Consumer Group 保证其订阅 Topic 的每个分区只被分配给该 Consumer Group 中的一个 Consumer 处理。
建议您在消费时指定消费分组 ID，若不指定， CKafka 系统会随机生成一个消费分组，但是容易触发实例创建消费分组的个数上限，具体限制可参考 [CKafka 计费概述](https://intl.cloud.tencent.com/document/product/597/11745)。



<span id="CKafka1"></span>

### 消息队列 CKafka

消息队列 CKafka（Cloud Kafka，CKafka）是一个分布式、高吞吐量、高可扩展性的消息系统，100%兼容开源 Kafka API（0.9、0.10版本）。CKafka 基于发布/订阅模式，通过消息解耦，使生产者和消费者异步交互，无需彼此等待。CKafka 具有数据压缩、同时支持离线和实时数据处理等优点，适用于日志压缩收集、监控数据聚合等场景。



### ZooKeeper

ZooKeeper 是一个为分布式应用提供一致性服务的软件，提供的功能包括：配置维护、域名服务、分布式同步、组服务等。在消息队列 CKafka 中，ZooKeeper 主要用于存储集群的元数据（MetaData）、进行 Leader 选举、故障容错等。