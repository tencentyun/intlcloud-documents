## Namespace

Namespace=QCE/LB_PUBLIC

> ?This namespace includes monitoring data in the CLB instance and real server dimensions.

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Statistical Period |
| ------------- | ------------------- | ------------------------------------------------------------ | ------- | ----------------- |
| AccOuttraffic |Public network outbound traffic | Traffic used by CLB to access the public network within the statistical period  | MB      | 10, 60, 300, 3600 |
| Clbhttp3xx     | 3xx status codes returned by CLB | Number of 3xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600 |
| Clbhttp404     | 404 status codes returned by CLB | Number of 404 status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600 |
| ClbHttp4xx     | 4xx status codes returned by CLB | Number of 4xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600 |
| ClbHttp502     | 502 status codes returned by CLB | Number of 502 status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600 |
| ClbHttp5xx     | 5xx status codes returned by CLB | Number of 5xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600 |
| ConNum        | Current connections | Number of connections on CLB or the listener within the statistical period | - | 60, 300, 3600 |
| Http2xx        | 2xx status codes         | Number of 2xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600 |
| Http3xx        | 3xx status codes         | Number of 3xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600 |
| Http404        | 404 status codes         | Number of 404 status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600 |
| Http4xx        | 4xx status codes         | Number of 4xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600 |
| Http502        | 502 status codes         | Number of 502 status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600 |
| Http5xx        | 5xx status codes         | Number of 5xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600 |
| InactiveConn | Inactive connections | Inactive connections on CLB or the listener within the statistical period| - | 60, 300, 3600 |
| InPkg         | Public network inbound packets | Number of request data packets received by CLB per second within the statistical period |Packets/sec | 10, 60, 300, 3600 |
| InTraffic     | Public inbound bandwidth | Bandwidth used by the client to access CLB over the public network within the statistical period |Mbps    | 10, 60, 300, 3600 |
| NewConn  | New connections | Number of newly established connections on CLB or the listener within the statistical period | Connections/sec |60, 300, 3600 |
| OutPkg | Public network outbound packets | Number of data packets sent by CLB per second within the statistical period |Packets/sec|10, 60, 300, 3600 |
| OutTraffic  | Public network outbound bandwidth | Bandwidth used by CLB to access the public network within the statistical period |Mbps    |10, 60, 300, 3600 |
| ReqAvg        | Average request time       | Average request time of CLB within the statistical period|ms    | 60, 300, 3600      |
| ReqMax        | Maximum request time       | Maximum request time of CLB within the statistical period|ms    | 60, 300, 3600      |
| RspAvg        | Average response time       | Average response time of CLB within the statistical period| ms    | 60, 300, 3600      |
| RspMax        | Maximum response time       | Maximum response time of CLB within the statistical period| ms    | 60, 300, 3600      |
| RspTimeout    | Timed-out responses       | The number of CLB’s timed-out responses within the statistical period| Responses/min | 60, 300, 3600      |
| SuccReq       | Successful requests per minute   | The number of CLB’s successful requests per minute within the statistical period|Requests/min | 60, 300, 3600      |
| TotalReq      | Requests per second         | The number of CLB’s requests per second within the statistical period| -      | 60, 300, 3600      |



> ?The statistical granularity (`period`) may vary by metrics. You can obtain the `period` supported by each metric by calling the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------ |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as `vip` |
| Instances.N.Dimensions.0.value | vip | A specific CLB VIP | Enter a specific IP address, such as `111.111.111.11` |
| Instances.N.Dimensions.1.name | loadBalancerPort | Dimension name of the CLB listener port | Enter a string-type dimension name, such as `loadBalancerPort` |
| Instances.N.Dimensions.1.value | loadBalancerPort | A specific CLB listener port | Enter a specific port number, such as `80` |
| Instances.N.Dimensions.2.name | protocol | Dimension name of the listening protocol | Enter a string-type dimension name, such as `protocol` |
| Instances.N.Dimensions.2.value | protocol | A specific listening protocol | Enter a specific protocol name, such as `http` |
| Instances.N.Dimensions.3.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name, such as `vpcId` |
| Instances.N.Dimensions.3.value | vpcId | VPC ID of the CLB instance | Enter a specific VPC ID, such as `vpc-1ywqac83` |
| Instances.N.Dimensions.4.name | lanIp | Dimension name of the IP address of the real server | Enter a string-type dimension name, such as `lanIp` |
| Instances.N.Dimensions.4.value | lanIp | IP address of the real server | Enter a specific IP address, such as `111.222.111.22` |
| Instances.N.Dimensions.5.name | port | Dimension name of the real server | Enter a string-type dimension name, such as `port` |
| Instances.N.Dimensions.5.Value | port | The specific service port number of the real server | Enter a specific port number, such as `80` |

## Input Parameters

Public network CLB instances support the combinations of the following four dimensions for querying monitoring data. The values for the four types of input parameters are as follows:

#### 1. Values of the input parameters at the public network CLB instance dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>

#### 2. Values of the input parameters at the public network CLB listener dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>

#### 3 Values of the input parameters at the public network CLB real server dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<VPC ID of the real server>
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>

#### 4. Values of the input parameters at the public network CLB real server port dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>
&Instances.N.Dimensions.5.Name=port
&Instances.N.Dimensions.5.Value=<Port number of the real server bound to the CLB instance>
