## Namespace

Namespace=QCE/CMQTOPIC

## Monitoring Metrics

| Metric | Description | Unit | Dimension |
| ------------------------ | ----------- | ---------------------- | ---------------------- |
| NumOfMsgPublished | Number of published messages | Count | topicId |
| NumOfMsgBatchPublished | Number of messages published in batches | Count | topicId |
| CountOfMsgPublished | Number of requests for published messages | Count | topicId |
| CountOfMsgBatchPublished | Number of requests for messages published in batches | Count | topicId |
| PublishSize | Size of published messages | MB | topicId |
| BatchPublishSize | Size of messages published in batches | MB | topicId |
| MsgHeapNum | Number of stored messages | Count | topicId |
| LanOuttraffic | Outbound traffic of private network requests | MB | topicId |
| WanOuttraffic | Outbound traffic of public network requests | MB | topicId |
| NumOfNotify | Total number of published messages | Count | topicId and subscriptionId |
| NumOfSuccNotify | Total number of messages published successfully | Count | topicId and subscriptionId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.




## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | topicId | Dimension name of the CMQ topic ID | Enter a string-type dimension name, such as topicId |
| Instances.N.Dimensions.0.Value | topicId | A specific CMQ topic ID | Enter a specific topic ID, such as topic-i4p4k0u0 |
| Instances.N.Dimensions.1.Name | subscriptionId | Dimension name of the CMQ subscription ID | Enter a string-type dimension name, such as subscriptionId |
| Instances.N.Dimensions.1.Value | subscriptionId | A specific CMQ subscription ID. This field is required if the dimensions corresponding to the metric are `topicId` and `subscriptionId` | Enter a specific `subscriptionId`, such as test1 |

## Input Parameters

To query the subscription monitoring data of a CMQ topic, use the following input parameters:
&Namespace= QCE/CMQTOPIC
&Instances.N.Dimensions.0.Name=topicId
&Instances.N.Dimensions.0.Value=<CMQ topic ID>
