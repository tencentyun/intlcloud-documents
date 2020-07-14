## Namespace
Namespace=QCE/CKAFKA

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ------------------------ | ------------------- | ------------------------------------------- | ---- | ----------------------------------------------------- |
| CgroupMaxOffset | Maximum offset of the current partition | Maximum offset in the partition corresponding to the consumer group | Count | consumerGroup, instanceId, topicId, partition, and topicName |
| CtopicMsgOffset | Current consumption offset | Current consumption offset in the partition corresponding to the consumer group | Count | consumerGroup, instanceId, topicId, partition, and topicName |
| CtopicUnconsumeMsgCount | Number of unconsumed messages | Number of unconsumed messages in the partition corresponding to the consumer group | Count | consumerGroup, instanceId, topicId, partition, and topicName |
| CtopicUnconsumeMsgOffset | Offset of the unconsumed messages | Size of the unconsumed messages in the partition corresponding to the consumer group | MB | consumerGroup, instanceId, topicId, partition, and topicName |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------- | ------------- | ------------------------------------------------ |
| Instances.N.Dimensions.0.Name | consumerGroup | Dimension name of the consumer group | Enter a string-type dimension name, such as consumerGroup |
| Instances.N.Dimensions.0.Value | consumerGroup | A specific consumer group | Enter a consumer group to query, such as perf-consumer-8330 |
| Instances.N.Dimensions.1.Name | instanceId | Dimension name of the instance ID | Enter a string-type dimension name, such as instanceId |
| Instances.N.Dimensions.1.Value | instanceId | A specific instance ID | Enter the ID of the instance whose monitoring data is to be queried, such as ckafka-test |
| Instances.N.Dimensions.2.Name | topicId | Dimension name of the topic ID | Enter a string-type dimension name, such as topicId |
| Instances.N.Dimensions.2.Value | topicId | A specific topic ID | Enter the ID of the subscribed topic, such as topic-test |
| Instances.N.Dimensions.3.Name | partition | Dimension name of the partition | Enter a string-type dimension name, such as partition |
| Instances.N.Dimensions.3.Value | partition | A specific partition | Enter a topic partition, such as 0 |
| Instances.N.Dimensions.4.Name | topicName | Dimension name of the topic | Enter a string-type dimension name, such as topicName |
| Instances.N.Dimensions.5.Value | topicName | A specific topic name | Enter the name of the consumption topic, such as test |

## Input Parameters

To query the monitoring data of a CKafka consumer group, use the following input parameters:
&Namespace=QCE/CKAFKA
&Instances.N.Dimensions.0.Name=consumerGroup
&Instances.N.Dimensions.0.Value=<Consumer group name>
&Instances.N.Dimensions.1.Name=instanceId
&Instances.N.Dimensions.1.Value=<Instance ID>
&Instances.N.Dimensions.2.Name=topicId
&Instances.N.Dimensions.2.Value=<Topic ID>
&Instances.N.Dimensions.3.Name=topicName
&Instances.N.Dimensions.3.Value=<Topic name>
&Instances.N.Dimensions.4.Name=partition
&Instances.N.Dimensions.4.Value=<Partition name> 
