## Issue Description

Messages produced by the client are blocked mainly because they cannot be sent, or message sending is slower than message production.

- If messages cannot be sent, "time out" will be prompted. In this case, you can use the command line for production and consumption first and view the basic performance of the cluster. For more information, see [Running Kafka Client (Optional)](https://intl.cloud.tencent.com/document/product/597/40969).

- There are three reasons why message sending is slower than production:
  - Producer instances are not enough. As the production performance of a single producer is limited, if there are insufficient producers while the traffic is high, message sending may be blocked.
  - The traffic is high, but the topic partitions are not enough, resulting in low write concurrency.
  - Another reason is low service quality. For example, the network quality is low, the broker load is high, or the client load is high (in the case of GC on the client). This will prolong message sending from the client to the server and reduce the production efficiency, causing a heap in the local buffer of the client and eventually blocking messages.

## Possible Causes

1. For Pro Edition instances, you can view advanced monitoring metrics such as the request queue depth and server production and consumption time in the console to check the overall load of the server and whether the server has performance problems. For Standard Edition instances, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to view such metrics.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8a2bf181f50ae2bafa8b87e0f6797024.png)
2. Check the client load such as local server CPU and memory utilization (if the client is in Java, you should pay attention to GC).
3. If blocking occurs occasionally, check whether the local network is stable, especially in a container network environment.
4. Check whether producers are not enough based on the traffic of a single server. If the throughput traffic of a server is high while producers send messages in a single thread, you should pay attention to the number of producers.

## Solutions

Below are some solutions:

1. If messages are produced faster than sent by the `Sender` thread to the broker, the memory configured by `buffer.memory` will be used up, blocking the sending operations by the producer. This parameter sets the maximum blocking time. If a larger `send buffer` is required, you can increase the value of `buffer.memory`, which is 32 MB by default.

```bash
# Maximum blocking time
max.block.ms=60000
# Configure the memory that the producer uses to cache messages to be sent to the broker. Users must adjust this according to the total memory size of the process where the producer resides.
buffer.memory=33554432
```

2. If the topic traffic is high while the producer instances for client message sending are not enough, you can add more producers for production as follows:

```bash
KafkaProducer<byte[],byte[]> producer = new KafkaProducer<>(props);
```

3. Add more partitions to the cluster.
4. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

