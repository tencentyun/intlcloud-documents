## Overview
Data compression can reduce network I/O transmission traffic and disk usage. This document describes the message formats supported for data compression and how to configure it based on your actual needs.

## Message Format
Currently, Kafka supports two versions of message formats: v1 and v2 (imported in Kafka 0.11.0.0). CKafka is compatible with Kafka 0.9, 0.10, 1.1, 2.4, and 2.8.

**Different configurations apply to different versions**, which are described as below:
- Message format conversion is mainly to make the format compatible with consumer programs on legacy versions. A Kafka cluster usually has message formats on multiple versions (v1 and v2).
- The broker will decompress and recompress messages on a new version to convert them to the legacy format.
- Message format conversion greatly affects performance. In addition to extra compression and decompression operations, Kafka will suffer from the loss of its excellent Zero Copy feature due to data compression. Therefore, **you must use the same message format**.
- Zero Copy: This feature can prevent costly data copy in kernel state when data is transferred in disks or over networks to implement fast data transfer.

## Compression Algorithm Comparison
Snappy is the officially recommended compression algorithm. Its analysis process is as follows:

Performance of a compression algorithm is evaluated mainly based on two metrics: compression ratio and compression/decompression throughput.
Versions below Kafka 2.1.0 support three compression algorithms: Gzip, Snappy, and LZ4.
In actual use of Kafka, comparison of **performance metric** between the three algorithms is as shown below:
- Compression ratio: LZ4 > Gzip > Snappy
- Throughput: LZ4 > Snappy > Gzip

Comparison of **physical resource** usage is as shown below:
- Bandwidth: As the compression ratio of Snappy is the lowest, the bandwidth used by Snappy is the lowest.
- CPU: CPU usage of each compression algorithm is similar. Snappy uses more CPU resources during compression, while Gzip uses more CPU resources during decompression.

Therefore, the recommended order of the three compression algorithms under normal circumstances is LZ4 > Gzip > Snappy. 
Long-term testing in the production environment shows that the above model works well in most cases. However, in extreme cases, the LZ4 compression algorithm will increase the CPU load.
As shown by analysis, this is because that the source data content varies by business, resulting in different performance of the compression algorithm. Therefore, we recommend users who are concerned about CPU metrics use the more stable Snappy compression algorithm.

## Configuring Data Compression
A producer can use the following method to configure data compression:
```
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("acks", "all");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

// After the producer is started, all its produced message sets will be compressed, which can greatly reduce the network transmission bandwidth and disk usage of the Kafka broker.

// Note that different versions have different configurations. Currently, v0.9 or earlier does not support compression, and v0.10 or later does not support Gzip compression.

props.put("compression.type", " lz4 ");
Producer<String, String> producer = new KafkaProducer<>(props);

In most cases, after receiving a message from the producer, the broker will retain it as-is without making any modification.
```

## Notes and Precautions
- When data is sent to CKafka, `compression.codec` cannot be set.
- Gzip compression is not supported by default. To use it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
As Gzip compression causes high CPU consumption, if it is used, all messages will become `InValid`.
- The program cannot run properly when the LZ4 compression is used. Possible causes include:
The message format is incorrect. The default message version of CKafka is v0.10.2. You need to use the message format v1.
- Setting method for SDK varies by Kafka client. You can query the setting method in the open-source community (e.g., [C/C++ Client Descriptions](https://github.com/edenhill/librdkafka/blob/master/INTRODUCTION.md#compression)) to set the version of the message format.

