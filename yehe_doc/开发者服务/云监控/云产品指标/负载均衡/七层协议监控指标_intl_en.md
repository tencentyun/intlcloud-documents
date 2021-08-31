## Namespace

Namespace=QCE/LOADBALANCE

## Monitoring Metrics

| Parameter | Metric Name | Description |Unit |  Statistical Period |
| ------------------- | ------------------- | ------------------------------------------------------------ | ------- | -------------------- |
| Clbhttp3xx     | 3xx status codes returned by CLB | Number of 3xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600, 86400 |
| Clbhttp404     | 404 status codes returned by CLB | Number of 404 status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600, 86400 |
| ClbHttp4xx     | 4xx status codes returned by CLB | Number of 4xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600, 86400 |
| ClbHttp502     | 502 status codes returned by CLB | Number of 502 status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600, 86400 |
| ClbHttp5xx     | 5xxx status codes returned by CLB | Number of 5xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | Codes/min  | 60, 300, 3600, 86400 |
| ConNum        | Number of connections | Number of connections on CLB or the listener within the statistical period |-  | 60, 300, 3600, 86400 |
| HttpCode2XX        | 2xx status codes         | Number of 2xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600, 86400 |
| HttpCode3XX        | 3xx status codes         | Number of 3xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600, 86400 |
| HttpCode404        | 404 status codes         | Number of 404 status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600, 86400 |
| HttpCode4XX        | 4xx status codes         | Number of 4xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600, 86400 |
| HttpCode502        | 502 status codes         | Number of 502 status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600, 86400 |
| HttpCode5XX        | 5xx status codes         | Number of 5xx status codes returned by the real server in the statistical period                | Codes/min  | 60, 300, 3600, 86400 |
| InPkg         | Inbound packets | Number of request data packets received by CLB per second within the statistical period |Packets/sec | 60, 300, 3600, 86400 |
| InTraffic     | Inbound bandwidth | Bandwidth used by the client to access CLB over the public network within the statistical period | Mbps|60, 300, 3600, 86400 |
| NewConn  | New connections | Number of newly established connections on CLB or the listener within the statistical period |Connections/min | 60, 300, 3600, 86400 |
| OutPkg | Outbound packets | Number of data packets sent by CLB per second within the statistical period |Packets/sec|60, 300, 3600, 86400 |
| OutTraffic  | Public network outbound bandwidth | Bandwidth used by CLB to access the public network within the statistical period |Mbps    |60, 300, 3600, 86400  |
| QPS       | Requests per minute   | The number of CLB’s requests per minute within the statistical period|- | 60, 300, 3600, 86400       |
| RequestTimeAverage  | Average request time       | CLB’s average request time within the statistical period| ms    | 60, 300, 3600, 86400 |
| RequestTimeMax        | Maximum request time       | Maximum request time of CLB within the statistical period|ms    | 60, 300, 3600, 86400 |
| ResponseTimeoutNum | Timed-out responses  |Number of timed-out responses of CLB within the statistical period | Responses/min   | 60, 300, 3600, 86400 |
| ResponseTimeAverage        | Average response time       | Average response time of CLB within the statistical period| ms    | 60, 300, 3600, 86400     |
| ResponseTimeMax        | Maximum response time       | Maximum response time of CLB within the statistical period| ms    | 60, 300, 3600, 86400      |



> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------- |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as `vip` |
| Instances.N.Dimensions.0.value | vip | A specific CLB VIP | Enter a specific IP address, such as `111.111.111.11` |
| Instances.N.Dimensions.1.name | loadBalancerPort | Dimension name of the CLB port | Enter a string-type dimension name, such as `loadBalancerPort` |
| Instances.N.Dimensions.1.value | loadBalancerPort | A specific CLB listener port | Enter a specific port number, such as `80` |
| Instances.N.Dimensions.2.name | protocol | Dimension name of the protocol | Enter a string-type dimension name, such as `protocol` |
| Instances.N.Dimensions.2.value | protocol | A specific listening protocol | Enter a specific protocol name, such as `http` |
| Instances.N.Dimensions.3.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name, such as `vpcId` |
| Instances.N.Dimensions.3.value | vpcId | VPC ID of the CLB instance | Enter a specific VPC ID, such as `vpc-1ywqac83` |
| Instances.N.Dimensions.4.name | domain | Dimension name of the domain | Enter a string-type dimension name, such as `domain` |
| Instances.N.Dimensions.4.value | domain   | Specific domain name                     | Enter a specific domain name, such as `www.cloud.tencent.com`       |
| Instances.N.Dimensions.5.name | url | Dimension name of the URL | Enter a string-type dimension name, such as `url` |
| Instances.N.Dimensions.5.value | url      | Specific URL                     | Enter a specific URL, such as `/aaa`                                     |
| Instances.N.Dimensions.6.Name | lanIp | Dimension name of the IP address of the real server | Enter a string-type dimension name, such as `lanIp` |
| Instances.N.Dimensions.6.value | lanIp | IP address of the real server | Enter a specific IP address, such as `111.222.111.22` |
| Instances.N.Dimensions.7.name | port | Dimension name of the real server | Enter a string-type dimension name, such as `port` |
| Instances.N.Dimensions.7.Value | port | The specific service port number of the real server | Enter a specific port number, such as `80` |





## Input Parameters

CLB layer-7 data supports the combinations of the following six dimensions for querying monitoring data. The values for the six types of input parameters are as follows:

#### 1. Values of the input parameters at the CLB instance dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>

#### 2. Values of the input parameters at the CLB listener dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>

#### 3. Values of input parameters in CLB domain name dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=domain name

#### 4. Values of input parameters in CLB domain name URL dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=domain name
&Instances.N.Dimensions.4.Name=url
&Instances.N.Dimensions.4.Value=<URL under the domain name>

#### 5. Values of the input parameters at the CLB real server dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.4.Name=domain
&Instances.N.Dimensions.4.Value=domain name
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=<URL under the domain name>
&Instances.N.Dimensions.6.Name=lanIp
&Instances.N.Dimensions.6.Value=<IP address of the real server bound to the CLB instance>

#### 6. Values of the input parameters at the CLB real server port dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.4.Name=domain
&Instances.N.Dimensions.4.Value=domain name
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=<URL under the domain name>
&Instances.N.Dimensions.6.Name=lanIp
&Instances.N.Dimensions.6.Value=<IP address of the real server bound to the CLB instance>
&Instances.N.Dimensions.7.Name=port
&Instances.N.Dimensions.7.Value=<Port number of the real server bound to the CLB instance>
