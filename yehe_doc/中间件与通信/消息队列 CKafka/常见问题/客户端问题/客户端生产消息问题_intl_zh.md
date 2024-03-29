### 客户端生产消息进入到阻塞状态有哪些常见的原因？

生产消息堵塞，核心原因是消息发送不出去，或者发送的速度小于生产的速度。

- 如果是发送不出去，有 time out 的提示，可以先使用命令行进行生产消费，查看集群基本性能。参考 [命令行生产消费](https://intl.cloud.tencent.com/document/product/597/40969)。

- 发送的速度小于生产速度，有三种原因：
  - 生产者的实例太少，即单个生产者的生产性能是有上限的，如果生产者的数量太少，流量太大，可能会导致发送堵塞。
  - 流量太大，Topic 的分区数太少，导致写入并行度不够。
  - 服务的质量有问题，例如网络质量下降，Broker 负载升高，客户端负载升高（例如客户端发生了GC）会导致客户端发送到服务端的整体耗时上升，导致生产速率下降。从而导致客户端本地的 buffer 堆积，出现阻塞。

#### 可能原因

1. 如果是专业版实例，可以在控制台查看高级监控，观察服务端的整体负载情况，如请求队列深度，生产消费的服务端耗时等。来确认服务端是否有性能问题。如果是标准版实例，可以 [提交工单](https://console.cloud.tencent.com/workorder/category) 查看这些指标。
    ![](https://main.qcloudimg.com/raw/1e0c6df4443b1933853616d0a0ecf9bf.png)
2. 排查客户端负载，如本地机器的 CPU，内存情况（如果是 Java 客户端，重点关注 GC 情况）。
3. 如果是偶尔出现阻塞状况，需要排查本地网络是否有波动。特别是容器网络环境下，需要着重关注。
4. 分析生产者的数量是否过少，可以从单机的流量来分析。如果单机吞吐的流量较大，而生产者又是单线程发送，则需要关注。

####  解决办法

可以通过如下手段尝试解决问题：

1. 当生产消息的速度比 Sender 线程发送到 Broker 速度快，导致 buffer.memory 配置的内存用完时会阻塞生产者 send 操作，该参数设置最大的阻塞时间。如果需要更大的send buffer，可以通过调大 buffer.memory，buffer.memory 的默认值是 32MB。
```bash
# 最大阻塞时间
max.block.ms=60000
# 配置生产者用来缓存消息等待发送到 Broker 的内存。用户要根据生产者所在进程的内存总大小调节
buffer.memory=33554432
```
2. 如果 Topic 的流量较大，客户端发送的 Produce 实例较少，可以多起几个 Produce 实例来生产。例如：
```bash
KafkaProducer<byte[],byte[]> producer = new KafkaProducer<>(props);
```
3. 扩容集群的分区数。
4.  [提交工单](https://console.cloud.tencent.com/workorder/category) 申请平台协助处理。



### 客户端生产消息如何保证在同一分区是有序的？

- 如果 Topic 只有一个分区，那么消息会根据服务端收到的数据顺序存储，则数据就是分区有序的。
- 如果 Topic 有多个分区，可以在生产端指定这一类消息的 key，这类消息都用相同的 key 进行消息发送，CKafka 会根据 key 哈希取模选取其中一个分区进行存储，由于一个分区只能由一个消费者进行监听消费，此时消息就具有消息消费的顺序性了。

对于单个生产者来说，对单个分区的生产，是保持有序的。



### 客户端生产消息一般会与 Broker 建立多少个连接？

从单个客户端实例（new 一个 Producer 对象的角度）来看，和所有服务端建立的连接总数公式如下：总连接数 = 1~n（n 是 Broker 的数量）。

每个 Java Producer 端管理 TCP 连接的方式如下：

1. KafkaProducer 实例创建时启动 Sender 线程，从而创建与 bootstrap.servers 中所有 Broker 的 TCP 连接。
2. KafkaProducer 实例首次更新元数据信息之后，还会再次创建与集群中所有 Broker 的 TCP 连接。
3. 如果 Producer 端发送消息到某台 Broker 时发现没有与该 Broke r的 TCP 连接，那么也会立即创建连接。
4. 如果设置 Producer 端 connections.max.idle.ms 参数大于0，则步骤1中创建的 TCP 连接会被自动关闭；默认情况下该参数值是9分钟，即如果在9分钟内没有任何请求“流过”某个 TCP 连接，那么 Kafka 会主动帮您把该 TCP 连接关闭。如果设置该参数=-1，那么步骤1中创建的 TCP 连接将无法被关闭，从而成为“僵尸”连接。



### 使用客户端发送消息后，如何确定是否发送成功？

大部分客户端在发送之后，会返回 Callback 或者 Future，如果回调成功，则说明消息发送成功。

您还可以在控制台通过以下方式确认消息发送是否正常：

- 查看 Topic 的分区状态，可以实时看到各个分区的消息数量。
- 查看 Topic的 流量监控，可以看到生产消息的流量曲线。

可以通过打印 send 方法返回的 partition 和分区信息来确认是否成功：

```java
Future<RecordMetadata> future = producer.send(new ProducerRecord<>(topic, messageKey, messageStr));
RecordMetadata recordMetadata = future.get();
log.info("partition: {}", recordMetadata.partition());
log.info("offset: {}", recordMetadata.offset());
```

如果能够打印出 partition 和 offset，则表示当前发送的消息在服务端已经被正确保存。此时可以通过消息查询的工具去查询相关位点的消息即可。
如果打印不出 partition 和 offset，则表示消息没有被服务端保存，客户端需要重试。

![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)
