## Namespace

Namespace = QCE/TDMQ

## Monitoring Metrics

> ?Statistical periods (`period`) may vary by metric. You can get the statistical periods for different metrics by calling the [`DescribeBaseMetrics`](https://intl.cloud.tencent.com/document/product/248/33882) API.


### TDMQ for RocketMQ

| Parameter | Description | Unit | Dimension | Statistical Period |
| ----------------------- | ------------------------------------------------------------ | ----- | ----------------------------------- | ---------------- |
| CmqQueueMsgBacklog | The number of heaped messages in the queue                       | -  | environmentId, tenantId, topicName  | 60s, 300s, 3600s |
| CmqTopicMsgBacklog | The number of heaped messages in the topic                                           | - | environmentId, tenantId, topicName  | 60s, 300s, 3600s |
| InactiveMsgNum | The number of invisible messages                                 | -    | appId, resourceId, resourceName | 60s, 300s, 3600s |
| CmqInactiveMsgPercentage | The percentage of invisible messages in CMQ | %     | environmentId, tenantId, topicName  | 60s, 300s, 3600s |
| MsgRateIn | The message production rate                                 | Messages/sec | environmentId, tenantId, topicName  | 60s, 300s, 3600s |
| MsgRateOut | The number of messages consumed by all consumers under the topic per second in the selected time range | Messages/sec | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| MsgThroughputIn | The data size of messages consumed by all consumers under the topic per second in the selected time range | B/S | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| SubMsgThroughputOut | The message consumption traffic                          | B/S | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| StorageSize | The message heap size | B | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| MsgAverageSize | The average produced message size | B | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| StorageBacklogPercentage | The percentage of the used message heap quota | % | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| CmqRequestCount | This metric is used to calculate the fees of API calls rather than the actual number of calls. | - | appId, resourceId, resourceName | 60s, 300s, 3600s |

## Dimensions and Parameters

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------- | -------------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name  | environmentId | Dimension name of the `environmentId`         | Enter a string-type dimension name: environmentId  |
| Instances.N.Dimensions.0.Value | environmentId | Specific namespace          | Enter a specific namespace, such as `CMQ_QUEUE-test99`, which can be obtained from the `NamespaceName` field returned by the [DescribeCmqQueues](https://www.tencentcloud.com/document/product/1110/44162) API. |
| Instances.N.Dimensions.0.Name  | tenantId      | Dimension name of the cluster ID | Enter a string-type dimension name: tenantId       |
| Instances.N.Dimensions.0.Value | tenantId      | Specific cluster ID          | Enter a specific cluster ID, such as `cmq-xxxxxxxx`, which can be obtained from the `TenantId` field returned by the [DescribeCmqQueues](https://www.tencentcloud.com/document/product/1110/44162) API. |
| Instances.N.Dimensions.0.Name  | topicName     | Dimension name of the topic name | Enter a string-type dimension name: topicName |
| Instances.N.Dimensions.0.Value | topicName     | Specific topic name          | Enter a specific topic name, such as `cmq-xxxxxxxx`, which can be obtained from the `QueueName` field returned by the [DescribeCmqQueues](https://www.tencentcloud.com/document/product/1110/44162) API. |
| Instances.N.Dimensions.0.Name | appId | Dimension name of the root account APPID | Enter a string-type dimension name: appid |
| Instances.N.Dimensions.0.Value | appId | Specific root account APPID      | Enter a root account APPID, such as `1250000000`                 |
| Instances.N.Dimensions.0.Name | resourceId | Dimension name of the cluster ID | Enter a string-type dimension name: resourceId |
| Instances.N.Dimensions.0.Value | resourceId | Specific cluster ID          | Enter a specific cluster ID, such as `cmq-xxxxxxxx`, which can be obtained from the `TenantId` field returned by the [DescribeCmqQueues](https://www.tencentcloud.com/document/product/1110/44162) API. |
| Instances.N.Dimensions.0.Name | resourceName | Dimension name of the topic name | Enter a string-type dimension name: resourceName |
| Instances.N.Dimensions.0.Value | resourceName | Specific topic name          | Enter a specific topic name, such as `cmq-xxxxxxxx`, which can be obtained from the `QueueName` field returned by the [DescribeCmqQueues](https://www.tencentcloud.com/document/product/1110/44162) API. |


## Input Parameters

**To query the monitoring data of a message queue, use the following input parameters:**

Metric 1:

&Namespace = QCE/TDMQ 
&Instances.N.Dimensions.0.Name = environmentId
&Instances.N.Dimensions.0.Value = Specific namespace
&Instances.N.Dimensions.1.Name = tenantId 
&Instances.N.Dimensions.1.Value = Specific cluster ID 
&Instances.N.Dimensions.2.Name = topicName 
&Instances.N.Dimensions.2.Value = Specific topic name

Metric 2:

&Namespace = QCE/TDMQ 
&Instances.N.Dimensions.0.Name = appId
&Instances.N.Dimensions.0.Value = Root account APPID
&Instances.N.Dimensions.1.Name = resourceId
&Instances.N.Dimensions.1.Value = Specific cluster ID 
&Instances.N.Dimensions.2.Name = resourceName
&Instances.N.Dimensions.2.Value = Specific topic name
