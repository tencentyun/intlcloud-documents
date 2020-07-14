## Namespace

Namespace=QCE/CKAFKA

## Monitoring Metrics

| Metric | Description | Unit | Dimension |
| ------------------------ | ----------- | ---- | ---------------------- |
| CtopicProFlow | Production traffic of the topic | MB | instanceId and topicId |
| CtopicConFlow | Consumption traffic of the topic | MB | instanceId and topicId |
| CtopicMsgHeap | Number of messages stored in the topic disk | MB | instanceId and topicId |
| CtopicProCount | Number of messages produced in the topic | Count | instanceId and topicId |
| CtopicProReqCount | Number of production requests in the topic | Count | instanceId and topicId |
| CtopicConReqCount | Number of consumption requests in the topic | Count | instanceId and topicId |
| CtopicMsgCount | Number of messages stored in the topic disk | Count | instanceId and topicId |
| CtopicConCount | Number of messages consumed in the topic | Count | instanceId and topicId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | instanceId | Dimension name of the CKafka instance ID | Enter a string-type dimension name, such as instanceId |
| Instances.N.Dimensions.0.Value | instanceId | A specific CKafka instance ID | Enter a specific instance ID, such as ckafka-test |
| Instances.N.Dimensions.1.Name | topicId | Dimension name of the topic ID | Enter a string-type dimension name, such as topicId |
| Instances.N.Dimensions.1.Value | topicId | A specific topic ID | Enter a specific topic ID, such as topic-test |

## Input Parameters

To query the monitoring data of a CKafka topic, use the following input parameters:
&Namespace=QCE/CKAFKA
&Instances.N.Dimensions.0.Name=instanceId
&Instances.N.Dimensions.0.Value=<Instance ID>
&Instances.N.Dimensions.1.Name=topicId
&Instances.N.Dimensions.1.Value=<Topic ID> 

