This document describes the concept and usage of the `auto.offset.reset` parameter.

## What is `auto.offset.reset`?

The `auto.offset.reset` parameter defines where to start consumption if the offset of the partition to be consumed cannot be obtained. For example, it specifies how the offset will be initialized if no offset is configured for the broker (such as upon initial consumption or when the offset expired for more than 7 days) or reset if the error `OFFSET_OUT_OF_RANGE` occurs.

The `auto.offset.reset` parameter has the following valid values:
- earliest: automatically resets to the minimum offset in the partition.
- latest: automatically resets to the maximum offset in the partition, which is the default value.
- none: throws the `OffsetOutOfRangeException` exception without automatically resetting the offset.

## When will `OFFSET_OUT_OF_RANGE` occur?

This error indicates that the offset committed by the client is out of the offset range allowed by the broker; for example, if ` LogStartOffset` and `LogEndOffset` of partition 1 of `topicA` are 100 and 300 respectively, but the offset committed by the client is less than 100 or greater than 300, then the broker will return this error, and the offset will be reset.

This error may occur in the following cases:
- The offset is set on the client, and there is no consumption in a period of time, but the message retention period is set for the topic, and after it elapses, the offset is deleted on the broker, that is, log scrolling occurs. At this point, if the client commits the deleted offset again, this error will occur.
- Due to problems such as SDK bugs and network packet loss, the client commits an exceptional offset, and this error will occur.
- There are unsynced replicas on the broker, and the leader is switched, triggering the truncation of follower replicas. At this point, if the offset committed by the client is in the truncated range, this error will occur.

## `auto.offset.reset=none` Description

### Background

You don't want the offset to be automatically reset, as your business doesn't allow such large-scale repeated consumption.

>!In this case, the consumer group will report an error as it fails to find the offset in its first consumption. Therefore, you need to manually set the offset in `catch`.


### Use instructions

After `auto.offset.reset` is set to `none`, automatic offset reset can be avoided; however, as the automatic reset mechanism is disabled, when a new partition is added, the client doesn't know where to start consuming the new partition, and an exception will occur. In this case, you need to manually set a consumer group offset and start consuming.

### How to use

During consumption, if you set `auto.offset.reset` to `none` for the consumer, and the exception `NoOffsetForPartitionException` is captured, then you should set the offset in `catch`. You can select one of the following methods based on your actual business needs:

- Specify the offset. You need to maintain the offset, which is convenient for retries.
- Specify to start consuming from the beginning.
- Specify the latest available offset as the offset.
- Get and set the offset based on the timestamp.

**Below is the sample code:**

```java
package com.tencent.tcb.operation.ckafka.plain;

import com.google.common.collect.Lists;
import com.tencent.tcb.operation.ckafka.JavaKafkaConfigurer;
import java.time.Instant;
import java.time.temporal.ChronoUnit;
import java.util.ArrayList;
import java.util.Collection;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Properties;
import org.apache.kafka.clients.CommonClientConfigs;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.clients.consumer.NoOffsetForPartitionException;
import org.apache.kafka.clients.consumer.OffsetAndTimestamp;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.common.PartitionInfo;
import org.apache.kafka.common.TopicPartition;
import org.apache.kafka.common.config.SaslConfigs;

public class KafkaPlainConsumerDemo {

    public static void main(String args[]) {
        // Set the path of the JAAS configuration file
        JavaKafkaConfigurer.configureSaslPlain();

        // Load `kafka.properties`
        Properties kafkaProperties = JavaKafkaConfigurer.getKafkaProperties();

        Properties props = new Properties();
        // Set the access point of the corresponding topic, which can be obtained in the console
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));

        // Set the access protocol
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_PLAINTEXT");
        // Set the PLAIN mechanism
        props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
        // Set the maximum interval between two polls
        // If the consumer does not return a heartbeat message within the interval, the broker determines that the consumer is not alive. The broker removes the consumer from the consumer group and triggers rebalancing. The default value is 30s
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        // Set the maximum number of messages that can be polled at a time
        // Do not set this parameter to an excessively large value. If polled messages are not all consumed before the next poll starts, load balancing is triggered and lagging occurs.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        // Set the method for deserializing messages
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG,
                "org.apache.kafka.common.serialization.StringDeserializer");
        // Set the consumer group of the current consumer instance. Enter the topic you created in the console
        // The instances in the same consumer group consume messages in load balancing mode
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));

        // Position of consumption offset. Note: if `auto.offset.reset` is set to `none`, the consumer group will report an error for failing to find the offset in its first consumption. Therefore, you need to manually set the offset in `catch`
        props.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "none");
        // Construct a consumer object. This generates a consumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(props);
        // Set one or more topics to which the consumer group subscribes
        // We recommend you configure consumer instances with the same `GROUP_ID_CONFIG` value to subscribe to the same topics
        List<String> subscribedTopics = new ArrayList<String>();
        // If you want to subscribe to multiple topics, add the topics here
        // You must create the topics in the console in advance
        String topicStr = kafkaProperties.getProperty("topic");
        String[] topics = topicStr.split(",");
        for (String topic : topics) {
            subscribedTopics.add(topic.trim());
        }
        consumer.subscribe(subscribedTopics);
        // Consume messages in loop
        while (true) {
            try {
                ConsumerRecords<String, String> records = consumer.poll(1000);
                // All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`. We recommend you create an independent thread pool to consume messages and then return the result in async mode
                for (ConsumerRecord<String, String> record : records) {
                    System.out.println(
                            String.format("Consume partition:%d offset:%d", record.partition(), record.offset()));
                }
            } catch (NoOffsetForPartitionException e) {
                System.out.println(e.getMessage());

                // If `auto.offset.reset` is set to `none`, you need to capture exceptions and set the offset on your own. You can select one of the following methods based on your actual business needs:
                // Sample 1. Specify the offset. You need to maintain the offset, which is convenient for retries
                Map<Integer, Long> partitionBeginOffsetMap = getPartitionOffset(consumer, topicStr, true);
                Map<Integer, Long> partitionEndOffsetMap = getPartitionOffset(consumer, topicStr, false);
                consumer.seek(new TopicPartition(topicStr, 0), 0);

                // Sample 2. Specify to start consuming from the beginning
                consumer.seekToBeginning(Lists.newArrayList(new TopicPartition(topicStr, 0)));

                // Sample 3. Specify the latest available offset as the offset
                consumer.seekToEnd(Lists.newArrayList(new TopicPartition(topicStr, 0)));

                // Sample 4. Get and set the offset based on the timestamp; for example, reset the offset to 10 minutes ago
                Map<TopicPartition, Long> timestampsToSearch = new HashMap<>();
                Long value = Instant.now().minus(300, ChronoUnit.SECONDS).toEpochMilli();
                timestampsToSearch.put(new TopicPartition(topicStr, 0), value);
                Map<TopicPartition, OffsetAndTimestamp> topicPartitionOffsetAndTimestampMap = consumer
                        .offsetsForTimes(timestampsToSearch);
                for (Entry<TopicPartition, OffsetAndTimestamp> entry : topicPartitionOffsetAndTimestampMap
                        .entrySet()) {
                    TopicPartition topicPartition = entry.getKey();
                    OffsetAndTimestamp entryValue = entry.getValue();
                    consumer.seek(topicPartition, entryValue.offset()); // Specify the offset. You need to maintain the offset, which is convenient for retries
                }


            }
        }
    }

    /**
     * Get the earliest and latest offsets of the topic
     * @param consumer
     * @param topicStr
     * @param beginOrEnd true begin; false end
     * @return
     */
    private static Map<Integer, Long> getPartitionOffset(KafkaConsumer<String, String> consumer, String topicStr,
            boolean beginOrEnd) {
        Collection<PartitionInfo> partitionInfos = consumer.partitionsFor(topicStr);
        List<TopicPartition> tp = new ArrayList<>();
        Map<Integer, Long> map = new HashMap<>();
        partitionInfos.forEach(str -> tp.add(new TopicPartition(topicStr, str.partition())));
        Map<TopicPartition, Long> topicPartitionLongMap;
        if (beginOrEnd) {
            topicPartitionLongMap = consumer.beginningOffsets(tp);
        } else {
            topicPartitionLongMap = consumer.endOffsets(tp);
        }
        topicPartitionLongMap.forEach((key, beginOffset) -> {
            int partition = key.partition();
            map.put(partition, beginOffset);
        });
        return map;
    }

}
```
