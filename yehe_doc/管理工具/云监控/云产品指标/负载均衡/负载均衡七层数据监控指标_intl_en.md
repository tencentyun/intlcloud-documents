## Namespace

Namespace: QCE/LOADBALANCE

## Monitoring Metrics

| Parameter | Metric Name | Unit |
| ---------------- | ----- | ---- |
| Connum | Current (active) connections | Connections/min |
| NewConn | New connections | Connections/min |
| Intraffic | Inbound traffic | Mbps |
| Outtraffic | Outbound traffic | Mbps |
| Inpkg | Inbound packets | Packets/sec |
| Outpkg | Outbound packets | Packets/sec |
| HttpCode2XX | 2xx status codes | Codes/min |
| HttpCode3XX | 3xx status codes | Codes/min |
| HttpCode4XX | 4xx status codes | Codes/min |
| HttpCode5XX | 5xx status codes | Codes/min |
| HttpCode404 | 404 status codes | Codes/min |
| HttpCode502 | 502 status codes | Codes/min |
| ResponseTimeMax | Maximum response time | ms |
| ResponseTimeAverage | Average response time | ms |
| ResponseTimeoutNum | Timed-out responses | Responses/min |
| QPS | Queries per second | Count |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ---------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as vip |
| Instances.N.Dimensions.0.value | vip | A specific CLB VIP | Enter a specific IP address, such as 111.111.111.11 |
| Instances.N.Dimensions.1.name | loadBalancerPort | Dimension name of the CLB port | Enter a string-type dimension name, such as loadBalancerPort |
| Instances.N.Dimensions.1.value | loadBalancerPort | A specific CLB port | Enter a specific port number, such as 80 |
| Instances.N.Dimensions.2.name | protocol | Dimension name of the protocol | Enter a string-type dimension name, such as protocol |
| Instances.N.Dimensions.2.value | protocol | A specific protocol name | Enter a specific protocol name, such as http |
| Instances.N.Dimensions.3.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name, such as vpcId |
| Instances.N.Dimensions.3.value | vpcId | A specific VPC ID (of the CLB instance) | Enter a specific VPC ID, such as 1111. We recommend that you enter a numeric vpcId. For information on obtaining the numeric vpcId, see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |
| Instances.N.Dimensions.4.name | lanIp | Dimension name of the lanIp | Enter a string-type dimension name, such as lanIp |
| Instances.N.Dimensions.4.value | lanIp | A specific IP address of the real server bound to the CLB instance | Enter a specific IP address, such as 111.222.111.22 |
| Instances.N.Dimensions.5.name | port | Dimension name of the port number | Enter a string-type dimension name, such as port |
| Instances.N.Dimensions.5.value | port | A specific port number of the real server bound to the CLB instance | Enter a specific port number, such as 80 |
| Instances.N.Dimensions.6.name | domain | Dimension name of the domain | Enter a string-type dimension name, such as domain |
| Instances.N.Dimensions.6.value | domain | A specific domain name | Enter a specific domain name, such as www.cloud.tencent.com |
| Instances.N.Dimensions.7.name | url | Dimension name of the URL | Enter a string-type dimension name, such as url |
| Instances.N.Dimensions.7.value | url | A specific URL | Enter a specific URL, such as /aaa |





## Input Parameters

CLB layer-7 data supports the combinations of the following four dimensions for querying monitoring data. The values for the four types of input parameters are as follows:

#### 1. Values of the input parameters at the CLB instance dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>

#### 2. Values of the input parameters at the CLB instance port dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>

#### 3. Values of the input parameters at the single-CLB-instance domain name dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=<Domain name>

#### 4. Values of the input parameters at the single-CLB-instance URL dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=<Domain name>
&Instances.N.Dimensions.4.Name=url
&Instances.N.Dimensions.4.Value=<URL under the domain name>

#### 5. Values of the input parameters at the all-CLB-instances domain name dimension (if one domain name is shared by multiple VIPs, the monitoring data will be aggregated.) The values of the input parameters are as follows:

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=<Domain name>

#### 6. Values of the input parameters at the CLB real server dimension

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
&Instances.N.Dimensions.4.Value=<Domain name>
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=<URL under the domain name>
&Instances.N.Dimensions.6.Name=lanIp
&Instances.N.Dimensions.6.Value=<IP address of the real server bound to the CLB instance>

#### 7. Values of the input parameters at the CLB real server port dimension

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
&Instances.N.Dimensions.4.Value=<Domain name>
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=<URL under the domain name>
&Instances.N.Dimensions.6.Name=lanIp
&Instances.N.Dimensions.6.Value=<IP address of the real server bound to the CLB instance>
&Instances.N.Dimensions.7.Name=port
&Instances.N.Dimensions.7.Value=<Port number of the real server bound to the CLB instance>
