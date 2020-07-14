## Namespace

Namespace=QCE/SCF_V2

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
|---------|---------|---------|---------|---------|
| Duration | Running duration | Function running duration, which is the average value based on the granularity (1 minute or 5 minutes) | ms | functionName and version |
| Invocation | Number of calls | Number of function calls, which is the sum based on the granularity (1 minute or 5 minutes) | Times | functionName and version |
| Error | Number of call errors | Number of failed requests (currently including function errors and platform errors) after the functions are run, which is the sum based on the granularity (1 minute or 5 minutes) | Times | functionName and version |
| ConcurrentExecutions | Number of concurrent executions | Number of concurrent processing requests at a point of time, which takes the maximum value based on the granularity (1 minute or 5 minutes) | Times | functionName and version |
| ConfigMem | Memory configuration | Size of the memory configured | MB | functionName and version |
| FunctionErrorPercentage | Function error rate | Function error rate | % | functionName and version |
| Http2xx | Number of successful calls | Number of successful calls | Times | functionName and version |
| Http432 | Resource usage exceeds the limit | Number of times that the resource usage exceeds the limit | Times | functionName and version |
| Http433 | Function execution time outs | Number of times that the function execution times out | Times | functionName and version |
| Http434 | Memory usage exceeds the limit | Number of times that the memory usage exceeds the limit | Times | functionName and version |
| Http4xx | Number of function errors | Number of function errors | Times | functionName and version |
| Mem | RAM | Memory capacity actually used during the running of a function, which takes the maximum value based on the granularity (1 minute or 5 minutes) | MB | functionName and version |
| MemDuration | Memory capacity used over a period of time | Amount of used memory resources. This parameter is calculated by multiplying the duration in which a function is run with the memory capacity used for the running of the function. The value of this parameter is the sum based on the granularity (1 minute or 5 minutes) | MB/ms | - |
| OutFlow | Public outbound traffic | External traffic generated when public resources are accessed in a function, which is the sum based on the granularity (1 minute or 5 minutes) | Times | functionName and version |
| ServerErrorPercentage | Platform error rate | Platform error rate | % | functionName and version |
| Syserr | Number of system internal errors | Number of system internal errors | Count | functionName and version |
| Throttle | Number of throttled function executions | Number of throttled function executions, which is the sum based on the granularity (1 minute or 5 minutes) | Count | functionName and version |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | functionName | Dimension name of the cloud function | Enter a string-type dimension name, such as functionName |
| Instances.N.Dimensions.0.Value | functionName | A specific cloud function name | Enter a specific function name, such as test |
| Instances.N.Dimensions.1.Name | version | Dimension name of the cloud function version | Enter a string-type dimension name, such as version |
| Instances.N.Dimensions.1.Value | version | A specific cloud function version | Enter a specific version of a function, such as $latest |

## Input Parameters

To query the monitoring data of a cloud function, use the following input parameters:
&Namespace=QCE/SCF_V2
&Instances.N.Dimensions.0.Name=functionName
&Instances.N.Dimensions.0.Value=test 
