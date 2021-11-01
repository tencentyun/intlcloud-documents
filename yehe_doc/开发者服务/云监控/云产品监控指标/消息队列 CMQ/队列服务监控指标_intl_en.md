## Namespace
Namespace=QCE/CMQ

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| -------------------- | ---------- | ---- | ----------------- | ----------------- |
| InvisibleMsgNum | Invisible messages in the queue | Number of invisible messages in the queue | Count | queueId and queueName |
| VisibleMsgNum | Visible messages in the queue | Number of visible messages in the queue | Count | queueId and queueName |
| SendMsgReqCount | Requests for sending messages | Number of requests for sending messages that a producer sends to the queue | Count | queueId and queueName |
| SendMsgNum | Sent messages | Number of messages that a producer sends to the queue | Count | queueId and queueName |
| RecvMsgReqCount | Requests for receiving messages | Number of requests for pulling messages that a consumer sends to the queue | Count | queueId and queueName |
| RecvMsgNum | Received messages | Number of messages that a consumer pulls from the queue | Count | queueId and queueName |
| RecvNullMsgNum | Received empty messages | Number of empty messages that a consumer pulls from the queue | Count | queueId and queueName |
| BatchRecvNullMsgNum | Empty messages received in batches | Number of empty messages that a consumer pulls from the queue in batches | Count | queueId and queueName |
| DelMsgReqCount | Requests for deleting messages | Number of requests for deleting messages that a consumer sends to the queue | Count | queueId and queueName |
| DelMsgNum | Deleted messages | Number of deleted messages | Count | queueId and queueName |
| SendMsgSize | Size of the messages sent | Size of the messages that a producer sends to the queue | MB | queueId and queueName |
| BatchSendMsgSize | Size of the messages sent in batches | Total size of the messages that a producer sends to the queue in batches | MB | queueId and queueName |
| BatchSendMsgReqCount | Requests for sending messages in batches | Number of requests for sending messages in batches that a producer sends to the queue | Count | queueId and queueName |
| BatchRecvMsgReqCount | Requests for receiving messages in batches | Number of requests for pulling messages in batches that a consumer sends to the queue | Count | queueId and queueName |
| BatchDelMsgReqCount | Requests for deleting messages in batches | Number of requests for deleting messages in batches | Count | queueId and queueName |
| MsgHeapNum | Heaped messages | Number of messages stored in the queue | Count | queueId and queueName |
| LanOuttraffic | Outbound traffic of private network requests | Outbound traffic of private network requests | MB | queueId and queueName |
| WanOuttraffic | Outbound traffic of public network requests | Outbound traffic of public network requests | MB | queueId and queueName |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.



## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | queueId | Dimension name of the CMQ queue ID | Enter a string-type dimension name, such as queueId |
| Instances.N.Dimensions.0.Value | queueId | A specific CMQ queue ID | Enter a specific CMQ queue ID, such as queue-3abkyggi |
| Instances.N.Dimensions.1.Name | queueName | Dimension name of the CMQ queue | Enter a string-type dimension name, such as queueName |
| Instances.N.Dimensions.1.Value | queueName | A specific CMQ queue name | Enter a specific CMQ queue name, such as test1 |

## Input Parameters

To query the monitoring data of a CMQ queue, use the following input parameters:
&Namespace=QCE/CMQ
&Instances.N.Dimensions.0.Name=queueId
&Instances.N.Dimensions.0.Value=<CMQ queue ID>
&Instances.N.Dimensions.1.Name=queueName
&Instances.N.Dimensions.1.Value=<CMQ queue name>

