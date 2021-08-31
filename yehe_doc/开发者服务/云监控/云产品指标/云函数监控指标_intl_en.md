## Namespace

Namespace=QCE/SCF_V2

## Monitoring Metrics

| Metric | Meaning | Description | Unit | Dimension |
| ----------------------- | ---------------- | ------------------------------------------------------------ | ---------- | ---------------------------------------- |
| Duration | Running duration | Average function running duration calculated by 1-minute or 5-minute granularity | ms | functionName, version, namspace, and alias |
| Invocation | Number of calls | Total number of function calls calculated by 1-minute or 5-minute granularity | - | functionName, version, namspace, and alias |
| Error | Number of call errors | Number of error requests generated after the function is executed, which is the sum of function errors and platform errors calculated by 1-minute or 5-minute granularity | - | functionName, version, namspace, and alias |
| ConcurrentExecutions | Concurrent executions | Maximum number of requests processed concurrently at the same point in time, which is calculated by 1-minute or 5-minute granularity | - | functionName, version, namspace, and alias |
| ConfigMem | Configure memory capacity | Configure memory capacity | MB | functionName, version, namspace, and alias |
| FunctionErrorPercentage | Function error rate | Function error rate | % | functionName, version, namspace, and alias |
| Http2xx | Successful calls | Number of successful calls | - | functionName, version, namspace, and alias |
| Http432 | Resource limit exceeded | Number of times that resource limit is exceeded | - | functionName, version, namspace, and alias |
| Http433 | Function execution timeout | Number of times that function execution times out | - | functionName, version, namspace, and alias |
| Http434 | Memory limit exceeded | Number of times that memory limit is exceeded | - | functionName, version, namspace, and alias |
| Http4xx | Function errors | Number of function errors | - | functionName, version, namspace, and alias |
| Mem | Running memory capacity | Maximum memory capacity used during function execution, which is calculated by 1-minute or 5-minute granularity | MB | functionName, version, namspace, and alias |
| MemDuration | Time memory capacity | Resource usage as the function running duration multiplied by memory capacity required for running the function, which is calculated by 1-minute or 5-minute granularity | MB/ms | - |
| OutFlow | Outbound traffic | Outbound traffic for accessing external network resources within the function, which is calculated by 1-minute or 5-minute granularity | - | functionName, version, namspace, and alias |
| ServerErrorPercentage | Platform error rate | Platform error rate | % | functionName, version, namspace, and alias |
| Syserr | System internal errors | Number of system internal errors | - | functionName, version, namspace, and alias |
| Throttle | Function execution throttles | Number of times that function execution is throttled, which is calculated by 1-minute or 5-minute granularity | - | functionName, version, namspace, and alias |

> ? The statistical granularity (`period`) may vary by metrics. To obtain the statistical granularity supported by each metric, call [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882).

## Overview of parameters in each dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------ | ---------------------- | -------------------------------------- |
| Instances.N.Dimensions.0.Name | functionName | Dimension name of cloud function | Enter a string-type dimension name, such as functionName |
| Instances.N.Dimensions.0.Value | functionName | A specific cloud function name | Enter a specific function name, such as test |
| Instances.N.Dimensions.1.Name | namespace | Dimension name of cloud function namespace | Enter a string-type dimension name, such as namspace |
| Instances.N.Dimensions.1.Value | namespace | Namespace of the cloud function | Enter a specific function name, such as test.<br>The namespace of a cloud function is customized by the user. You can call [ListNamespaces](https://intl.cloud.tencent.com/document/product/583/34411) to obtain namespace details |
| Instances.N.Dimensions.2.Value | version | Dimension name of cloud function version | Enter a string-type dimension name, such as version |
| Instances.N.Dimensions.2.Name | version | A specific cloud function version | Enter a specific function version, such as $latest |
| Instances.N.Dimensions.2.Value | alias | Dimension name of cloud function alias | Enter a string-type dimension name, such as alias |
| Instances.N.Dimensions.2.Name | alias | A specific cloud function alias | Enter a specific function alias, such as test |

## Input Parameters

You can query monitoring data using the following two dimension combinations. The input parameters are as follows: 

#### 1. Pulling metric monitoring data based on cloud function version

&Instances.N.Dimensions.0.Name=functionName
&Instances.N.Dimensions.0.Value=<Cloud function name>
&Instances.N.Dimensions.1.Name=namspace
&Instances.N.Dimensions.1.Value=<Cloud function namespace>
&Instances.N.Dimensions.2.Name=version
&Instances.N.Dimensions.2.Value=<Cloud function version> 

#### 2. Pulling metric monitoring data based on cloud function alias

 &Instances.N.Dimensions.0.Name=functionName
&Instances.N.Dimensions.0.Value=<Cloud function name>
&Instances.N.Dimensions.1.Name=namspace
&Instances.N.Dimensions.1.Value=<Cloud function namespace>
&Instances.N.Dimensions.2.Name=alias
&Instances.N.Dimensions.2.Value=<Cloud function alias> 
