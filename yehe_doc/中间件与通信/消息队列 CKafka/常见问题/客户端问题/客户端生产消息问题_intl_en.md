### What are the common reasons why messages produced by a client are blocked?

Produced messages are blocked mainly because the messages cannot be sent, or message sending is slower than message production.

- If messages cannot be sent, "time out" will be prompted. In this case, you can use the command line for production and consumption first and view the basic performance of the cluster. For more information, please see [Running Kafka Client (Optional)](https://intl.cloud.tencent.com/document/product/597/40969).

- There are three reasons why message sending is slower than production:
  - Producer instances are not enough. As the production performance of a single producer is limited, if there are too few producers, but the traffic is high, message sending may be blocked.
  - The traffic is high, but the topic partitions are not enough, resulting in low write concurrency.
  - The service quality is exceptional; for example, the network quality is low, the broker load is high, or the client load is high (in case of GC on the client). This will prolong message sending from the client to the server and reduce the production efficiency, causing a heap in the local buffer of the client and eventually blocking messages.

#### Possible causes

1. For Pro Edition instances, you can view advanced monitoring metrics such as the request queue depth and server production and consumption time in the console to check the overall load of the server and whether the server has performance problems. For Standard Edition instances, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to view such metrics.
   ![](https://main.qcloudimg.com/raw/af8dcc058b765c4f116cba7a89850904.png)
2. Check the client load such as local server CPU and memory utilization (if the client is in Java, you should pay attention to GC).
3. If blocking occurs occasionally, you should check whether the local network is stable, especially in a container network environment.
4. Check whether producers are not enough based on the traffic of a single server. If the throughput traffic of a server is high, but producers send messages in a single thread, you should pay attention to the number of producers.

#### Solutions

You can fix the problem in the following ways:

1. If messages are produced faster than sent by the `Sender` thread to the broker, the memory configured by `buffer.memory` will be used up, blocking the sending operations by the producer. This parameter sets the maximum period of blocking. If a larger `send buffer` is required, you can increase the value of `buffer.memory`, which is 32 MB by default.
```bash
# Maximum blocking time
max.block.ms=60000
# Configure the memory that the producer uses to cache messages waiting to be sent to the broker. You should adjust this value based on the total memory size of the process where the producer resides
buffer.memory=33554432
```
2. If the topic traffic is high, but the producer instances for client message sending are not enough, you can add more producers for production as follows:
```bash
KafkaProducer<byte[],byte[]> producer = new KafkaProducer<>(props);
```
3. Add more partitions to the cluster.
4. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.



### How is it ensured that messages produced by the client are orderly in the same partition?

- If the topic has only one partition, messages will be stored in the order in which they are received by the server, and the data will be orderly in the partition.
- If the topic has multiple partitions, you can specify keys for messages on the producer. If such messages are sent with the same key, CKafka will select a partition for their storage based on the hash of the key. As a partition can be listened on and consumed by only one consumer, messages will be consumed in the sending order.

Message consumption in a single partition for a single producer is orderly.



### How many connections does a client generally establish to brokers for message production?

For a single client instance (a producer object generated in the `new` method), the total connections established between it and all servers is 1–number of brokers.

Each Java producer manages TCP connections as follows:

1. The `Sender` thread will be initiated when a `KafkaProducer` instance is created to establish TCP connections to all brokers in `bootstrap.servers`.
2. After the metadata on the `KafkaProducer` instance is updated, TCP connections to all brokers in the cluster will be established again.
3. If no TCP connections are found when a producer sends a message to a broker, a connection will be established immediately.
4. If you set the `connections.max.idle.ms` parameter on the producer to a value above 0, TCP connections established in step 1 will be closed automatically. The parameter value is 9 minutes by default; that is, if no requests are sent through a TCP connection in 9 minutes, Kafka will automatically close the connection. If you set the parameter to -1, TCP connections established in step 1 cannot be closed and will become "zombie" connections.



### How do I know whether a message is successfully sent from a client?

After sending a message, most clients will return a `Callback` or `Future`. If the callback is success, the message is successfully sent.

You can also use the following methods to check whether a message is successfully sent in the console:

- View the topic partition status to see the real-time number of messages in each partition.
- View the topic traffic monitoring data to see the traffic curve of the produced messages.

You can print the partition information returned by the `send` method to check whether the message is successfully sent:

```java
Future<RecordMetadata> future = producer.send(new ProducerRecord<>(topic, messageKey, messageStr));
RecordMetadata recordMetadata = future.get();
log.info("partition: {}", recordMetadata.partition());
log.info("offset: {}", recordMetadata.offset());
```

If the partition and offset can be printed out, the currently sent message has been correctly saved on the server. At this time, you can use the message query tool to query the information of the relevant offset.
If the partition and offset cannot be printed out, the message has not been saved on the server, and the client needs to retry.

![](https://main.qcloudimg.com/raw/cca4f62e86898eec49d8a9cde7ae9fa8.png)
