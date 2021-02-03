## Namespace
Namespace=QCE/CKAFKA

## Monitoring Metrics

### Consumer group - partition

| Parameter | Metric | Unit | Dimension |
| ------------------------ | ------------------------ | ------- | ----------------------------------------------------- |
| CpartitionConsumerSpeed  | Partition consumption speed             | Times/min | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| CgroupMaxOffset          | Maximum consumer group offset       | -      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| CtopicMsgOffset          | Topic-level consumer group offset   | -      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| CtopicUnconsumeMsgCount  | Number of topic-level unconsumed messages   | -      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| CtopicUnconsumeMsgOffset | Topic-level unconsumed message size | MB      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |

### Consumer group - topic

| Parameter | Metric | Unit | Dimension |
| ------------------- | ------------------------------- | ------- | ----------------------------------------------------- |
| CtopicConsumerSpeed | Topic consumption speed                    | Times/min | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| MaxOffsetTopic      | Maximum topic offset corresponding to consumer group | -      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| OffsetTopic         | Current consumption offset in consumer group          | -      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| UnconsumeSizeTopic  | Unconsumed message size in consumer group          | MB      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |
| UnconsumeTopic      | Number of unconsumed messages in consumer group            | -      | ConsumerGroup, InstanceId, TopicId, Partition, TopicName |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------- | ------------- | ------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | consumerGroup | Consumer group dimension name | Enter a String-type dimension name: consumerGroup       |
| Instances.N.Dimensions.0.Value | consumerGroup | Specific consumer group information | Enter the information of the consumer group to be viewed, such as `perf-consumer-8330` |
| Instances.N.Dimensions.1.Name  | instanceId    | Instance ID dimension name   | Enter a String-type dimension name: instanceId       |
| Instances.N.Dimensions.1.Value | instanceId   | Specific instance ID | Enter the ID of the instance for which to view monitoring data, such as `ckafka-test` |
| Instances.N.Dimensions.2.Name  | topicId   | Topic ID dimension name | Enter a String-type dimension name: topicId                    |
| Instances.N.Dimensions.2.Value | topicId   | Specific topic ID | Enter the ID of the topic subscribed to, such as `topic-test` |
| Instances.N.Dimensions.3.Name  | partition   | Partition dimension name   | Enter a String-type dimension name: partition                     |
| Instances.N.Dimensions.3.Value | partition   | Specific partition information |  Enter the partition information of the topic, such as `0` |
| Instances.N.Dimensions.4.Name  | topicName   | Topic dimension name | Enter a String-type dimension name: topicName                  |
| Instances.N.Dimensions.5.Value | topicName   | Specific topic name | Enter the name of the consumed topic, such as `test` |

## Input Parameter Description

To query the monitoring data of a CKafka consumer group, set the following input parameters:
&Namespace=QCE/CKAFKA
&Instances.N.Dimensions.0.Name=consumerGroup
&Instances.N.Dimensions.0.Value=consumer group
&Instances.N.Dimensions.1.Name=instanceId
&Instances.N.Dimensions.1.Value=instance ID
&Instances.N.Dimensions.2.Name=topicId
&Instances.N.Dimensions.2.Value=topic ID
&Instances.N.Dimensions.3.Name=topicName
&Instances.N.Dimensions.3.Value=topic name
&Instances.N.Dimensions.4.Name=partition
&Instances.N.Dimensions.4.Value=partition 
