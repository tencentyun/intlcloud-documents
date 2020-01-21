## Operation Scenarios
Data compression can reduce network I/O transmission traffic and disk usage. This document describes the message formats supported for data compression and how to configure it based on your actual needs.

## Message Format
Currently, Kafka supports two message formats, i.e., v1 and v2 (imported in v0.11.0.0). CKafka supports the open-source versions 0.9 and 0.10.2, and exclusive CKafka clusters support v1.1.1.

**Different configurations apply to different versions**, which are described as below:
- Message format conversion is mainly to make the format compatible with consumer programs on legacy versions. A Kafka cluster usually has message formats on multiple versions (v1 and v2).
- The broker will convert messages on a new version to a format on a legacy version, which involves decompression and recompression of messages.
- Message format conversion greatly affects performance. In addition to extra compression and decompress operations, Kafka will suffer from the loss of its excellent Zero Copy feature due to data compression. Therefore, **you must use the same message format.**
- Zero Copy: this feature can prevent costly data copy in kernel state when data is transmitted in disks or over networks so as to implement fast data transmission.

## Compression Algorithm Comparison
Performance of a compression algorithm is evaluated mainly based on two metrics: compression ratio and compression/decompression throughput.
Versions below Kafka 2.1.0 support three compression algorithms: Gzip, Snappy, and LZ4.
In actual use of Kafka, comparison of **performance metric** between the three algorithms is as shown below:
- Compression ratio: LZ4 > Gzip > Snappy
- Throughput: LZ4 > Snappy > Gzip

Comparison of **physical resource** usage is as shown below:
- Bandwidth: as the compression ratio of Snappy is the lowest, the bandwidth used by Snappy is the lowest.
- CPU: CPU usage of each compression algorithm is similar. Snappy uses more CPU resources during compression, while Gzip uses more CPU resources during decompression.

Since bandwidth resources are more valuable than CPU and disk resources (1-Gigabit network is the standard configuration), the ranking of the three compression algorithms is LZ4 > Gzip > Snappy.

## Configuring Data Compression
A producer can use the following method to configure data compression:
```
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("acks", "all");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

// After the producer is started, all its produced message sets will be compressed, which can greatly reduce the network transmission bandwidth and disk usage of the Kafka broker.

// Please note that different versions have different configurations. Currently, versions 0.9 and below do not support compression, and versions 0.10 and above do not support Gzip compression.

props.put("compression.type", " lz4 ");
Producer<String, String> producer = new KafkaProducer<>(props);

In most cases, after receiving a message from the producer, the broker will retain it as-is without making any modification.
```

## Notes and Precautions
- When data is sent to CKafka, compression for `compression.codec` cannot be set.
- CKafka does not support the Gzip compression format.
Gzip compression has high CPU consumption; therefore, if Gzip is used, all messages will be `InValid`.
- The program cannot run properly when the LZ4 compression method is used. Possible causes include:
The message format is incorrect. The default message version of CKafka is v0.10.2. You need to use the message format v1.
- Setting method for SDK varies by Kafka client. You can query the setting method in the open-source community (e.g., [C/C++ Client Descriptions](https://github.com/edenhill/librdkafka/blob/master/INTRODUCTION.md#compression)) to set the version of the message format.
