## Namespace

Namespace=QCE/APIGATEWAY

## Metric Name

| Parameter | Metric Name | Description | Calculation Method | Unit |
| ------------- | ------------------------------------------------------------ | ---------------------------- | ---- | ---- |
| NumOfReq | Number of requests | Number of requests passing the API gateway | Sum based on the selected time granularity | Times |
| SucceReq | Number of valid calls | Number of valid call requests passing the API gateway | Sum based on the selected time granularity | Times |
| OutTraffic | Public outbound traffic | Traffic of public packets sent by the API gateway | Sum based on the selected time granularity | MB |
| InTraffic | Private outbound traffic | Traffic of private packets sent by the API gateway | Sum based on the selected time granularity | MB |
| ResponseTime | Response time | Time used by the API gateway to respond to a request | Average value based on the selected time granularity | ms |
| ClientError | Number of client errors | Number of invalid requests sent to the API gateway by the client, such as authentication failures or exceeding the upper limit | Sum based on the selected time granularity | Times |
| ServerError | Number of backend server errors | Number of status codes greater than or equal to 400 returned by the real server after the API gateway forwards messages to the real server | Sum based on the selected time granularity | Times |
| ConcurrentConnections | Number of concurrent connections | Number of current persistent connections of the API gateway | Average value based on the selected time granularity | Count |
| Serviceservererror404 | Number of backend 404 errors | Number of errors where the requested resource is not found on the real server | Sum based on the selected time granularity | Times |
| Serviceservererror502 | Number of server 502 errors | Number of errors where an invalid response is received by the real server when the API gateway attempts to execute a backend request | Sum based on the selected time granularity | Times |

>
> - Monitoring metrics of the API gateway support all dimensions. You can choose the dimensions of the monitoring metrics based on the [Dimension Description](#weidu).
> - The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | --------------- | ----------------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name | serviceId | Dimension name of the API gateway service ID | Enter a string-type dimension name, such as serviceId |
| Instances.N.Dimensions.0.Value | serviceId | A specific API gateway service ID | Enter a specific service ID, such as service-12345jy |
| Instances.N.Dimensions.1.Name | environmentName | Environment dimension name | Enter a string-type dimension name, such as environmentName |
| Instances.N.Dimensions.1.Value | environmentName | A specific environment name | Enter an environment name, such as release, test, or repub |
| Instances.N.Dimensions.2.Name | apiid/key | Dimension name of the APIid or the SecretKey | Enter a string-type dimension name, such as apiid or key |
| Instances.N.Dimensions.2.Value | apiid/secretid | A specific APIid or SecretId | Enter a specific APIid or SecretId |

<span id="weidu">

## Dimensions

</span>

 The API gateway provides the combinations of monitoring data in the following three dimensions: environment, API, and key pair (SecretId and SecretKey).

The following describes how to query the combinations of the API gateway in three dimensions:

#### 1. Values of the input parameters at the environment dimension

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=<serviceId value>
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=<Environment name>

#### 2. Values of the input parameters at the API dimension

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=<serviceId value>
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=<Environment name>
&Instances.N.Dimensions.2.Name=apiid
&Instances.N.Dimensions.2.Value=<API ID>

#### 3. Values of the input parameters at the key pair dimension (for allowed users only)

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=<serviceId value>
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=<Environment name>
&Instances.N.Dimensions.2.Name=key
&Instances.N.Dimensions.2.Value=<secretid of the key pair>
