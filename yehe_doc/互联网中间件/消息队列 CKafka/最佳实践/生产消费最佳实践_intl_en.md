This document describes the best practices of message production and consumption in CKafka to help you reduce errors in message consumption.

## Message Production

### Recommendations for topic use

- Configuration requirements: 3 replicas and in-sync replication are recommended. The minimum number of in-sync replicas should be 2, and the number of in-sync replicas cannot be equal to the number of topic replicas; otherwise, the failure of 1 replica will lead to the inability to produce messages.
- Creation method: you can choose whether to enable **Auto-Create Topic** in CKafka. After it is enabled, a topic with 3 partitions and 3 replicas will be automatically created when a topic that has not been created is produced or consumed in.
- The recommended maximum number of partitions for a topic is 100.
- A topic can have 3 replicas (due to the limits on the current version, this value cannot be changed).

### Retry upon failure

In a distributed environment, due to network or other issues, messages may occasionally fail to be sent. This is probably because the message actually has been sent successfully but the ACK mechanism failed, or because the message indeed has not been sent successfully.

You can set the following retry parameters based on your business needs:

|  Parameter  |  Description |
| ------ | ------ | 
| `retries` | Number of retries, which is `3` by default. You can consider setting it to `Integer.MAX_VALUE` (valid and maximum) for applications that have zero tolerance for data loss. |
| `retry.backoff.ms` | Retry interval. We recommend you set it to `1000`. |

By doing so, you will be able to deal with the issue where the broker's leader partition can't respond to producer requests immediately.

### Async sending

The sending API is async. If you want to receive the result of sending, you can call `metadataFuture.get(timeout, TimeUnit.MILLISECONDS)`.

### One producer corresponding to one app

A producer is thread-safe and can send messages to any topics. Generally, we recommend that one application correspond to one producer.

### Acks

Kafka's ACK mechanism refers to the producer's mechanism for acknowledgment of message sending. It is set to `Acks` in Kafka 0.10.x or `request.required.acks` on version 0.8.x. The setting of `Acks` will directly affect the throughput of the Kafka cluster and the reliability of messages.

The `Acks` parameter is described as follows:

|  Parameter  |  Description |
| ------ | ------ | 
| `acks=0` | No response from the server is required. In this case, the performance is high, but the risk of data loss is great. |
| `acks=1` | A response will be returned after the primary server node writes successfully. In this case, the performance is moderate, and the risk of data loss is also moderate. A failure of the primary node may cause data loss. |
| `acks=all` | A response will be returned only after the primary server node writes successfully and the secondary node syncs successfully. The performance is poor, but the risk of data loss is small. Only a failure of both the primary and secondary nodes will cause data loss. |

We recommend you select `acks=1` generally and select `acks=all` for important services.


### Batch

A CKafka topic generally has multiple partitions. Before the producer client sends a message to the server, it needs to determine the topic and the partition to which the message should be sent. When sending multiple messages to the same partition, the producer client will package the messages into a batch and then send the batch to the server. Additional overheads will be incurred when the batch is processed. In general, a small batch will cause the producer client to generate a large number of requests, which will cause the messages to queue up on the client and the server, lead to an increase in the corresponding device's CPU utilization, and thus increase the delays in message sending and consumption. A suitable batch size can reduce the number of requests sent to the server by the client during message sending, thereby improving the throughput and reducing the delay in message sending.

The batch parameters are described as follows:

|  Parameter  |  Description |
| ------ | ------ | 
| `batch.size` | Size of cached messages sent to each partition (which is the sum of bytes of the messages rather than the number of messages). Once the set value is reached, a network request will be triggered, and the producer client will send the messages to the server in batch. |
| `linger.ms` | Maximum amount of time each message is cached. After this time elapses, the producer client will ignore the limit of the `batch.size` and immediately send the messages to the server. |
| `buffer.memory` | After the total size of all cached messages exceeds this value, the messages will be sent to the server immediately, and the limits of `batch.size` and `linger.ms` will be ignored. The default value of `buffer.memory` is 32 MB, which can ensure sufficient performance for a single producer. |

  >? If you start multiple producers in the same JVM, it is likely that each producer will use 32 MB of cache space. In this case, OOM errors may occur, and you need to consider the value of `buffer.memory` in order to avoid OOM errors.

You can adjust the values of the parameters based on your actual business needs.

### Key and value

Each message in CKafka has two fields: key (message identifier) and value (message content).

For ease of tracking, please set a unique key for each message, which allows you to track a message and print its sending and consumption logs to learn about its production and consumption conditions.

If you want to send a large number of messages, we recommend you use the sticky partitioning policy instead of setting keys.

### Sticky partitioning

Only messages sent to the same partition will be placed in the same batch, so one factor that determines how a batch will be formed is the partitioning policy set by the Kafka producer. The Kafka producer allows you to choose a partition that suits your business by setting the partitioner implementation class. If a key is specified for a message, the default policy of the Kafka producer is to hash the message key and then select a partition based on the result of hashing to ensure that messages with the same key are sent to the same partition.

If no key is specified for a message, the default policy of Kafka below v2.4 is to use all partitions in the topic in loops and send the message to each partition in a round robin manner. However, this default policy has a poor batch performance and may produce a large number of small batches, which increases actual delays. As it was inefficient in partitioning messages without a key, Kafka 2.4 introduced the sticky partitioning policy.

The sticky partitioning policy mainly addresses the problem of small batches caused by the distribution of messages without a key into different partitions. The main practice is to randomly select another partition and use it as much as possible for subsequent messages after the batch is completed for a partition. With this policy, messages will be sent to the same partition in the short run, but from the perspective of the entire execution, messages will be evenly sent to different partitions, which helps avoid skewed partitions while reducing delays and improving the overall service performance.

If you use a Kafka producer client on v2.4 or later, the default partitioning policy is sticky partitioning. If you use an older producer client, you can implement a partitioning policy on your own based on how the sticky partitioning policy works and then make it take effect through the `partitioner.class` parameter.

For more information on how to implement the sticky partitioning policy, please see the following implementation of Java code. The code is implemented by switching from one partition to another at certain time intervals.

```
public class MyStickyPartitioner implements Partitioner {

    // Record the time of the last partition switch.
    private long lastPartitionChangeTimeMillis = 0L;
    // Record the current partition.
    private int currentPartition = -1;
    // Partition switch time interval, which can be selected based on your business needs.
    private long partitionChangeTimeGap = 100L;
    
    public void configure(Map<String, ?> configs) {}

    /**
     * Compute the partition for the given record.
     *
     * @param topic The topic name
     * @param key The key to partition on (or null if no key)
     * @param keyBytes serialized key to partition on (or null if no key)
     * @param value The value to partition on or null
     * @param valueBytes serialized value to partition on or null
     * @param cluster The current cluster metadata
     */
    public int partition(String topic, Object key, byte[] keyBytes, Object value, byte[] valueBytes, Cluster cluster) {

        // Get the information of all partitions.
        List<PartitionInfo> partitions = cluster.partitionsForTopic(topic);
        int numPartitions = partitions.size();

        if (keyBytes == null) {
            List<PartitionInfo> availablePartitions = cluster.availablePartitionsForTopic(topic);
            int availablePartitionSize = availablePartitions.size();

            // Determine the current available partitions.
            if (availablePartitionSize > 0) {
                handlePartitionChange(availablePartitionSize);
                return availablePartitions.get(currentPartition).partition();
            } else {
                handlePartitionChange(numPartitions);
                return currentPartition;
            }
        } else {
            // For messages with a key, a partition will be selected based on the hash value of the key.
            return Utils.toPositive(Utils.murmur2(keyBytes)) % numPartitions;
        }
    }

    private void handlePartitionChange(int partitionNum) {
        long currentTimeMillis = System.currentTimeMillis();

        // After the partition switch time interval elapses, the next partition will be switched to; otherwise, the original partition will still be used.
        if (currentTimeMillis - lastPartitionChangeTimeMillis >= partitionChangeTimeGap
            || currentPartition < 0 || currentPartition >= partitionNum) {
            lastPartitionChangeTimeMillis = currentTimeMillis;
            currentPartition = Utils.toPositive(ThreadLocalRandom.current().nextInt()) % partitionNum;
        }
    }

    public void close() {}

}
```

### Order in partition

Within a single partition, messages are stored in the order in which they are sent. Each topic is divided into a number of partitions. If messages are distributed to different partitions, the cross-partition message order cannot be ensured.

If you want messages to be consumed in the sending order, you can specify keys for such messages on the producer. If such messages are sent with the same key, CKafka will select a partition for their storage based on the hash of the key. As a partition can be listened on and consumed by only one consumer, messages will be consumed in the sending order.

## Message Consumption

### Basic message consumption process

1. Poll the data.
2. Execute the consumption logic.
3. Poll the data again.

### Load balancing

Each consumer group can contain multiple consumers with the same `group.id` value. In this way, consumers in the same consumer group consume the subscribed topic through load balancing.

For example, if consumer group A subscribes to topic A and enables three consumer instances C1, C2, and C3, then each message sent to topic A will be eventually delivered to only one of the three instances. By default, CKafka will evenly distribute messages to the consumer instances to achieve consumption load balancing.

Load balancing within CKafka works by allocating the partitions of the subscribed topic evenly to all consumers. Therefore, the number of consumers should not be greater than the number of partitions; otherwise, there will be consumer instances with no partitions. Except for the first start, load balancing will be triggered every time consumer instances are restarted, added, or removed.

### Subscription relationship

We recommend that all consumer instances in the same consumer group subscribe to the same topic so as to facilitate troubleshooting.

- **A consumer group subscribes to multiple topics.**

  A consumer group can subscribe to multiple topics, and the messages in such topics will be consumed evenly by the consumers in the consumer group. For example, if consumer group A subscribes to topics A, B, and C, then messages in the three topics will be consumed evenly by the consumers in consumer group A. 

  Below is the sample code to make a consumer group subscribe to multiple topics:
  ```
  String topicStr = kafkaProperties.getProperty("topic");
  String[] topics = topicStr.split(",");
  for (String topic: topics) {
  subscribedTopics.add(topic.trim());
  }
  consumer.subscribe(subscribedTopics);
  ```

- **A topic is subscribed to by multiple consumer groups.**

  A topic can be subscribed to by multiple consumer groups, and the consumers in such consumer groups independently consume all messages in the topic. For example, if both consumer groups A and B subscribe to topic A, each message sent to topic A will be delivered to both the consumer instances in consumer group A and the consumer instances in consumer group B, and the two processes are independent of each other.

### One consumer group corresponding to one application

We recommend that one consumer group correspond to one application. In other words, different applications correspond to different code snippets. If you need to write different code snippets in the same application, you should prepare different copies of `kafka.properties`, such as `kafka1.properties` and `kafka2.properties`.

### Consumer offset

Each topic has multiple partitions, and each partition counts the total number of current messages, which is called `MaxOffset`.

CKafka consumers consume messages in partitions in sequence and record the number of consumed messages, which is called `ConsumerOffset`.

Number of remaining messages (aka the "number of retained messages") = MaxOffset - ConsumerOffset.

**Offset commit**

There are two parameters related to CKafka consumers:
- enable.auto.commit: the default value is `true`.
- auto.commit.interval.ms: the default value is 1000, i.e., 1s.

As a result of the combination of the two parameters, before the client polls the data, it will always check the time of the last committed offset first, and if the time defined by the `auto.commit.interval.ms` parameter has elapsed, the client will start an offset commit.

Therefore, if `enable.auto.commit` is set to `true`, it is always necessary to ensure that the data polled last time has been consumed before data polling; otherwise, the offset may be skipped.

If you want to control offset commits by yourself, please set `enable.auto.commit` to `false` and call the `commit(offsets)` function.

**Offset reset**

The `ConsumerOffset` will be reset under the following two circumstances:
- The server has no committed offsets (for example, when the client is started for the first time).
- A message is pulled from an invalid offset (for example, the `MaxOffset` in a partition is 10, but the client pulls a message from offset 11).

For a Java client, you can configure a resetting policy by using `auto.offset.reset`. There are three policies: 
- latest: consumption will start from the maximum offset.
- earliest: consumption will start from the minimum offset.
- none: resetting will not be performed.

>?
>- We recommend you set the resetting policy to `latest` instead of `earliest` so as to avoid starting consumption from the beginning when the offset is invalid, as that may cause a lot of repetitions.
>- If you manage the offset by yourself, you can set the policy to `none`.

### Message pull

In the consumption process, the client pulls messages from the server. When the client pulls large messages, you should control the pulling speed and pay attention to the following parameters:
- max.poll.records: set it to 1 if a single message exceeds 1 MB in size.
- max.partition.fetch.bytes: set it to a value slightly greater than the size of a single message.
- fetch.max.bytes: set it to a value slightly greater than the size of a single message.

When messages are consumed over the public network, a disconnection may often occur due to the bandwidth limit of the public network. In this case, you should control the pulling speed and pay attention to the following parameters:
- fetch.max.bytes: we recommend you set it to half of the public network bandwidth (note that the unit of this parameter is bytes, while the unit of the public network bandwidth is bits).

- max.partition.fetch.bytes: we recommend you set it to one third or one fourth of `fetch.max.bytes`.

### Duplicate messages and consumption idempotency

CKafka consumption uses the at-least-once semantics, that is, a message is delivered at least once, which guarantees that messages will never be lost. However, messages may be delivered more than once. Network issues and client restarts may cause a few duplicate messages. If the application consumer is sensitive to duplicate messages (such as orders and transactions), idempotency should be implemented for the messages.

Taking a database application as an example, the common practice is as follows:
- When sending a message, pass in the key as the unique ID.
- When consuming a message, determine whether the key has already been consumed; if so, ignore it; otherwise, consume it once.

Of course, if the application itself is not sensitive to a small number of duplicate messages, idempotency is not necessary.

### Consumption failures

In CKafka, messages are consumed from partitions one by one in sequence. If the consumer fails to execute the consumption logic after getting a message, for example, when dirty data is stored on the application server, the message will fail to be processed, and human intervention will be required. There are two methods for dealing with this situation:

- The consumer will keep trying to execute the consumption logic upon failure. This method may cause the consumer thread to be jammed by the current message and lead to message heap.
- As CKafka is not designed to process failed messages, in practice, it will typically print failed messages or store them in a service (such as a dedicated topic created for storing failed messages), so that you can regularly check failed messages, analyze the causes of failures, and process accordingly.

### Consumption delays

In the consumption process, the client pulls messages from the server. In general, if the client can consume messages timely, there will be no significant delays. If a high delay is detected, you should first check whether messages heap up and speed up consumption accordingly.

### Consumption heap

The common causes of message heap include the following:
- Consumption is slower than production. In this case, you should speed up consumption.
- Consumption is jammed.

After getting a message, a consumer will execute the consumption logic and generally make some remote calls. If it waits for the results at the same time, the consumption process may be jammed.

It should be ensured as much as possible that the consumer will not jam the consumption threads. If it needs to wait for the call results, we recommend you set a wait timeout period, so that the consumer will be treated as a failure after the timeout period elapses.

### Speeding up consumption

- Increase the number of consumer instances.
  You can either increase the number of consumer instances directly in the process (you need to ensure that each instance corresponds to one thread) or deploy multiple consumer instance processes.
  >?After the number of instances exceeds the number of partitions, you can't add more instances; otherwise, there will be idle consumer instances.

- Increase the number of consumer threads. 
  1. Define a thread pool.
  2. Poll the data.
  3. Commit the data into the thread pool for concurrent processing.
  4. Poll the data again after a successful concurrent processing result is returned.

### Socket buffers

The default value of the `receive.buffer.bytes` parameter in Kafka 0.10.x is 64 KB, but the default value of the `socket.receive.buffer.bytes` parameter in Kafka 0.8.x is 100 KB.

Both the default values are too small for high-throughput environments, especially when the bandwidth-delay product of the network between the broker and the consumer is greater than that of the local area network (LAN).

For networks with a delay of 1 ms or more and a high bandwidth (such as 10 Gbps or higher), we recommend you set the socket buffer size to 8 or 16 MB.

Even if you don't have enough memory, you should consider setting this parameter to at least 1 MB. You can also set it to -1, so that the underlying operating system will adjust the buffer size based on the actual network conditions.

However, for consumers that need to start "hot" partitions, automatic adjustment may not be that fast.



