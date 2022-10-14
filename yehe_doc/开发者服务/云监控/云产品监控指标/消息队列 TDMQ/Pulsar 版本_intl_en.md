## Namespace

Namespace = QCE/TDMQ

## Monitoring Metrics

> ?Statistical periods (`period`) may vary by metric. You can get the statistical periods for different metrics by calling the [`DescribeBaseMetrics`](https://intl.cloud.tencent.com/document/product/248/33882) API.

### TDMQ for Pulsar

| Parameter | Description | Unit | Dimension | Statistical Period |
| ---------------------------- | ------------------------------------------------------------ | ----- | ------------------------------------------- | ---------------- |
| MsgAverageSize | The average produced message size | B | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| MsgRateIn | The message production rate                                 | Messages/sec | environmentId, tenantId, topicName  | 60s, 300s, 3600s |
| MsgThroughputIn              | The message production traffic                          | B/S | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| InMessagesTotal              | The total number of messages produced in the current topic. This metric will be reset to zero when the server is restarted or switched. | -    | environmentId, tenantId, topicName          | 60s, 300s, 3600s |
| ProducersCount               | The number of producers                                                   | -    | environmentId, tenantId, topicName          | 60s, 300s, 3600s |
| StorageSize | The message heap size | B | environmentId, tenantId, topicName | 60s, 300s, 3600s |
| BacklogSize                  | The number of heaped messages                                                 | -    | environmentId, tenantId, topicName          | 60s, 300s, 3600s |
| SubscriptionsCount           | The number of subscribers                                                   | -    | environmentId, tenantId, topicName          | 60s, 300s, 3600s |
| ConsumersCount               | The number of consumers                                                   | -    | environmentId, tenantId, topicName          | 60s, 300s, 3600s |
| SubMsgBacklog                | The number of messages produced to TDMQ but not consumed in the selected time range. This value should not be too high. If it gets high, expand the consumer service to reduce the heap. | -    | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| SubMsgDelayed                | The number of messages that use TDMQ's delayed message feature in the selected time range. Such messages will not be consumed immediately after production; instead, they will be consumed after the specified delay time elapses. | -    | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| SubUnackedMsg                | The number of messages that were sent to the consumer but haven't received an acknowledgment in the selected time range. If there are a lot of such messages, check whether your consumer service is working properly and whether you are using the official SDK for consumption. | -    | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| SubConsumerCount             | The number of consumers validly connected to this topic in the selected time range.            | -    | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| SubMsgRateRedeliver          | The number of all retransmitted messages in a second under this topic in the selected time range.    | Messages/sec | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| SubMsgRateExpired            | The expired message deletion rate                                             | Messages/sec | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| SubMsgRateOut                | The message consumption rate                                                 | Messages/sec | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| SubMsgThroughputOut          | The message consumption traffic                                                 | B/S   | environmentId, subName, tenantId, topicName | 60s, 300s, 3600s |
| NsStorageSize                | The message heap size in the namespace                                         | B     | namespace, tenant                           | 60s, 300s, 3600s |
| TenantInMessagesTotal        | The total number of inbound messages in the virtual cluster                                           | -    | tenant                                      | 60s, 300s, 3600s |
| TenantMsgAverageSize         | The average message size at the tenant level                                         | B     | tenant                                      | 60s, 300s, 3600s |
| TenantRateIn                 | The message production rate at the tenant level                                        | -    | tenant                                      | 60s, 300s, 3600s |
| TenantRateOut                | The message consumption rate at the tenant level                                         | -    | tenant                                      | 60s, 300s, 3600s |
| TenantStorageSize            | The message heap size at the tenant level                                         | B     | tenant                                      | 60s, 300s, 3600s |
| TenantIn entry Count         | The number of entries that produced messages                                          | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe128       | The number of entries that produced messages less than or equal to 128B                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe1Kb       | The number of entries that produced messages between 512B and 1 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe2Kb       | The number of entries that produced messages between 1 KB and 2 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe4Kb       | The number of entries that produced messages between 2 KB and 4 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe16Kb      | The number of entries that produced messages between 4 KB and 16 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe1Mb       | The number of entries that produced messages between 100 KB and 1 MB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe100Kb     | The number of entries that produced messages between 16 KB and 100 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLeOverflow  | The number of entries that produced messages above 1 MB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantIn entry SizeSum       | The total size of entries that produced messages                                        | -    | tenant                                      | 60s, 300s, 3600s |
| TenantInentrySizeLe512       | The number of entries that produced messages between 128B and 512B                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeCount      | The number of entries that consumed messages                                          | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLe100Kb    | The number of entries that consumed messages between 16 KB and 100 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLe128      | The number of entries that consumed messages less than or equal to 128B                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentry SizeLe1Kb     | The number of entries that consumed messages between 512B and 1 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLe16Kb     | The number of entries that consumed messages between 4 KB and 16 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLe1Mb      | The number of entries that consumed messages between 100 KB and 1 MB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLe2Kb      | The number of entries that consumed messages between 1 KB and 2 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLe4Kb      | The number of entries that consumed messages between 2 KB and 4 KB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLe512      | The number of entries that consumed messages between 128B and 512B                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeLeOverflow | The number of entries that consumed messages above 1 MB                            | -    | tenant                                      | 60s, 300s, 3600s |
| TenantOutentrySizeSum        | The total size of entries that consumed messages                                        | -    | tenant                                      | 60s, 300s, 3600s |

## Dimensions and Parameters

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------- | -------------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name  | environmentId | Dimension name of the `environmentId`         | Enter a string-type dimension name: environmentId  |
| Instances.N.Dimensions.0.Value | environmentId | Specific namespace          | Enter a specific namespace, such as `default`, which can be obtained from the `EnvironmentId` field returned by the [DescribeEnvironments](https://www.tencentcloud.com/document/product/1110/44122) API. |
| Instances.N.Dimensions.0.Name  | tenantId      | Dimension name of the cluster ID | Enter a string-type dimension name: tenantId       |
| Instances.N.Dimensions.0.Value | tenantId      | Specific cluster ID                | Enter a specific cluster ID, such as `pulsar-xxxxxxxxxx`, which can be viewed in [Cluster](https://console.cloud.tencent.com/tdmq/cluster) in the TDMQ for Pulsar console or obtained from the `ClusterId` field returned by the [DescribeClusterDetail](https://www.tencentcloud.com/document/product/1110/44144) API. |
| Instances.N.Dimensions.0.Name  | topicName     | Dimension name of the topic name | Enter a string-type dimension name: topicName |
| Instances.N.Dimensions.0.Value | topicName     | Specific topic name               | Enter a specific topic name, such as `testTopic`, which can be viewed in [Topic](https://console.cloud.tencent.com/tdmq/topic) in the TDMQ for Pulsar console. |
| Instances.N.Dimensions.0.Name  | namespace     | Dimension name of the cluster's namespace | Enter a string-type dimension name: namespace      |
| Instances.N.Dimensions.0.Value | namespace     | Specific namespace               | Enter a specific namespace, such as `test`, which can be obtained from the `NamespaceName` field returned by the [DescribeEnvironments](https://www.tencentcloud.com/document/product/1110/44122) API.               |
| Instances.N.Dimensions.0.Name  | tenant        | Dimension name of the cluster ID | Enter a string-type dimension name: tenant       |
| Instances.N.Dimensions.0.Value | tenant        | Specific cluster ID                | Enter a specific cluster ID, such as `pulsar-xxxxxxxxxx`, which can be obtained from the `ClusterId` field returned by the [DescribeClusterDetail](https://www.tencentcloud.com/document/product/1110/44144) API. |

## Input Parameters

**To query the monitoring data of a message queue, use the following input parameters:**

Metric type 1:
&Namespace = QCE/TDMQ 
&Instances.N.Dimensions.0.Name = environmentId
&Instances.N.Dimensions.0.Value = Specific namespace
&Instances.N.Dimensions.1.Name = tenantId 
&Instances.N.Dimensions.1.Value = Specific cluster ID 
&Instances.N.Dimensions.2.Name = topicName 
&Instances.N.Dimensions.2.Value = Specific topic name


Metric type 2:
&Namespace = QCE/TDMQ 
&Instances.N.Dimensions.0.Name = tenant 
&Instances.N.Dimensions.0.Value = Specific cluster ID
