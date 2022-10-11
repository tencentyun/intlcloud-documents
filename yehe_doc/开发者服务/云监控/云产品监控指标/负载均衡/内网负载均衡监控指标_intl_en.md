## Namespace

Namespace=QCE/LB_PRIVATE

>?Metrics in this namespace are private network CLB monitoring metrics in four dimensions: CLB instance, listener, real server (RS), and RS port.

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Statistical Period |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------- |
| ClientConnum        | Client-to-CLB active connections   | Number of active connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientInactiveConn  | Client-to-CLB inactive connections | Number of inactive connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientConcurConn    | Client-to-CLB concurrent connections   | Number of concurrent connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period | -      | 10s, 60s, 300s       |
| ClientNewConn       | Client-to-CLB new connections   | Number of new connections initiated from the client to the CLB instance in the statistical period     | -   | 10s, 60s, 300s       |
| ClientInpkg         | Client-to-CLB inbound packets       | Number of data packets sent from the client to the CLB instance per second in the statistical period         | Count/sec   | 10s, 60s, 300s       |
| ClientOutpkg        | Client-to-CLB outbound packets       | Number of data packets sent from the CLB instance to the client per second in the statistical period         | Count/sec   | 10s, 60s, 300s       |
| ClientAccIntraffic  | Client-to-CLB inbound traffic       | Volume of inbound traffic from the client to the CLB instance in the statistical period                   | MB      | 10s, 60s, 300s       |
| ClientAccOuttraffic | Client-to-CLB outbound traffic       | Volume of outbound traffic from the CLB instance to the client in the statistical period                  | MB      | 10s, 60s, 300s       |
| ClientOuttraffic    | Client-to-CLB outbound bandwidth       | Outbound bandwidth used by the traffic from the CLB instance to the client in the statistical period               | Mbps    | 10s, 60s, 300s       |
| ClientIntraffic | Client-to-CLB inbound bandwidth | Inbound bandwidth used by the traffic from the client to the CLB instance in the statistical period               | Mbps | 10s, 60s, 300s |
| OutTraffic | CLB-to-RS outbound bandwidth | Outbound bandwidth used by the traffic from the RS to the CLB instance in the statistical period | Mbps | 60s, 300s |
| InTraffic | CLB-to-RS inbound bandwidth | Inbound bandwidth used by the traffic from the CLB instance to the RS in the statistical period | Mbps | 60s, 300s |
| OutPkg | CLB-to-RS outbound packets | Number of data packets sent from the RS to the CLB instance per second in the statistical period | Count/sec | 60s, 300s |
| InPkg | CLB-to-RS inbound packets | Number of data packets sent from the CLB instance to the RS per second in the statistical period | Count/sec | 60s, 300s |
| ConNum | CLB-to-RS connections | Number of connections initiated from the CLB instance to the RS in the statistical period | - | 60s, 300s |
| NewConn | CLB-to-RS new connections | Number of new connections initiated from the CLB instance to the RS in the statistical period | Count/min | 60s, 300s |
| DropTotalConns      | Dropped connections                 | Number of connections dropped by the CLB instance or listener in the statistical period. <br/>This metric is only supported for bill-by-IP accounts. | -      | 10s, 60s, 300s     |
| InDropBits          | Dropped inbound bandwidth                 | Bandwidth dropped when the client accesses the CLB instance over the public network in the statistical period. <br/>This metric is only supported for bill-by-IP accounts. | Byte    | 10s, 60s, 300s     |
| OutDropBits         | Dropped outbound bandwidth                 | Bandwidth dropped when the CLB instance accesses the public network in the statistical period.<br/>This metric is only supported for bill-by-IP accounts. | Byte    | 10s, 60s, 300s     |
| InDropPkts          | Dropped inbound packets             | Number of data packets dropped when the client accesses the CLB instance over the public network in the statistical period.<br/>This metric is only supported for bill-by-IP accounts. | Count/sec   | 10s, 60s, 300s     |
| OutDropPkts         | Dropped outbound packets             | Number of data packets dropped when the CLB instance accesses the public network in the statistical period.<br/>This metric is only supported for bill-by-IP accounts. | Count/sec   | 10s, 60s, 300s     |
| DropQps             | Dropped QPS                   | Number of requests dropped by the CLB instance or listener in the statistical period. <br/>This metric is dedicated to layer-7 listeners and only supported for bill-by-IP accounts. | -      | 60s, 300s           |
| IntrafficVipRatio   | Inbound bandwidth utilization               | Utilization of the bandwidth for the client to access the CLB instance over the public network in the statistical period.<br/>This metric is only supported for bill-by-IP accounts and is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).| %       | 10s, 60s, 300s     |
| OuttrafficVipRatio  | Outbound bandwidth utilization               | Utilization of the bandwidth for the CLB instance to access the public network in the statistical period.<br/>This metric is only supported for bill-by-IP accounts and is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).| %       | 10s, 60s, 300s     |
| ReqAvg | Average request time | The average request time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| ReqMax | Maximum request time | The maximum request time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspAvg | Average response time | The average response time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspMax | Maximum response time | The maximum response time of the CLB instance in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Millisecond | 60s, 300s |
| RspTimeout | Number of response timeouts | The number of CLB response timeouts in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| SuccReq | Successful requests per minute | The number of successful CLB requests per minute in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| TotalReq | Requests per second | The number of CLB requests per second in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | - | 60s, 300s |
| ClbHttp3xx | 3xx status codes returned by CLB | The number of 3xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp4xx | 4xx status codes returned by CLB | The number of 4xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp5xx | 5xx status codes returned by CLB | The number of 5xx status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp404 | 404 status codes returned by CLB | The number of 404 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp499 | 499 status codes returned by CLB | The number of 499 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp502 | 502 status codes returned by CLB | The number of 502 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp503 | 503 status codes returned by CLB | The number of 503 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| ClbHttp504 | 504 status codes returned by CLB | The number of 504 status codes returned by CLB in the statistical period (sum of CLB and RS return codes). <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http2xx | 2xx status codes | The number of 2xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http3xx | 3xx status codes | The number of 3xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http4xx | 4xx status codes | The number of 4xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http5xx | 5xx status codes | The number of 5xx status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http404 | 404 status codes | The number of 404 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http499 | 499 status codes | The number of 499 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http502 | 502 status codes | The number of 502 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http503 | 503 status codes | The number of 503 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| Http504 | 504 status codes | The number of 504 status codes returned by the RS in the statistical period. <br/>This metric is dedicated to layer-7 listeners. | Count/min | 60s, 300s |
| OverloadCurConn | Concurrent SNAT connections | The concurrent connections of the CLB instance’s SNAT IP per minute in the statistical period. <br/>This metric is currently in beta. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category). | Count/min | 60s |
| ConnRatio           | SNAT port utilization            | Utilization of ports of the CLB instance's SNAT IPs in the statistical period.<br/>Port utilization = number of concurrent SNAT connections / (number of SNAT IPs * 55,000 * number of real servers). <br/>This metric is currently in beta. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category). | %       | 60s           |
| SnatFail | Failed SNAT connections | The number of failed connections between the CLB instance’s SNAT IP and the RS per minute in the statistical period.<br/>This metric is currently in beta. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category). | Count/min | 60s |
| UnhealthRsCount     | Health check exceptions             | Number of health check exceptions of the CLB instance in the statistical period.                   | -      | 60s, 300s           |



> ?Statistical periods (`period`) may vary by metric. You can get the statistical periods for different metrics by calling the [`DescribeBaseMetrics`](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Dimensions and Parameters

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------ |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name: `vip`. |
| Instances.N.Dimensions.0.value | vip | A CLB VIP | Enter an IP address, such as `111.111.111.11`. |
| Instances.N.Dimensions.1.name | loadBalancerPort | Dimension name of the CLB listener port | Enter a string-type dimension name: `loadBalancerPort`. |
| Instances.N.Dimensions.1.value | loadBalancerPort | A CLB listener port | Enter a port number, such as `80`. |
| Instances.N.Dimensions.2.name | protocol | Dimension name of the listener protocol | Enter a string-type dimension name: `protocol`. |
| Instances.N.Dimensions.2.value | protocol | A listener protocol | Enter a protocol, such as `TCP` or `UDP`. |
| Instances.N.Dimensions.3.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name: `vpcId`. |
| Instances.N.Dimensions.3.Value | vpcId | VPC ID of the CLB instance | Enter a specific VPC ID, such as `5436123` |
| Instances.N.Dimensions.4.name | lanIp | Dimension name of the IP address of the RS | Enter a string-type dimension name: `lanIp`. |
| Instances.N.Dimensions.4.value | lanIp | IP address of the RS | Enter a specific IP address, such as `111.222.111.22` |
| Instances.N.Dimensions.5.name | port | Dimension name of the RS port | Enter a string-type dimension name: `port`. |
| Instances.N.Dimensions.5.Value | port | Service port number of the RS | Enter a port number, such as `80`. |

## Input Parameters

Private network CLB instances support the combination of the following four dimensions for querying monitoring data. The values of the four types of input parameters are as follows:

#### 1. Values of the input parameters in the private network CLB instance dimension

&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name = `vip`
&Instances.N.Dimensions.0.Value = IP address
&Instances.N.Dimensions.1.Name = `vpcId`
&Instances.N.Dimensions.1.Value = VPC ID of the CLB instance

#### 2. Values of the input parameters in the private network CLB listener dimension

&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name = `vip`
&Instances.N.Dimensions.0.Value = IP address
&Instances.N.Dimensions.1.Name = `vpcId`
&Instances.N.Dimensions.1.Value = VPC ID of the CLB instance
&Instances.N.Dimensions.2.Name =`loadBalancerPort`
&Instances.N.Dimensions.2.Value = Port number
&Instances.N.Dimensions.3.Name = `protocol`
&Instances.N.Dimensions.3.Value= Protocol type

#### 3 Values of the input parameters in the private network CLB RS dimension

&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name = `vip`
&Instances.N.Dimensions.0.Value = IP address
&Instances.N.Dimensions.1.Name = `loadBalancerPort`
&Instances.N.Dimensions.1.Value = Port number
&Instances.N.Dimensions.2.Name = `protocol`
&Instances.N.Dimensions.2.Value = Protocol type
&Instances.N.Dimensions.3.Name = `vpcId`
&Instances.N.Dimensions.3.Value = VPC ID of the CLB instance
&Instances.N.Dimensions.4.Name = `lanIp`
&Instances.N.Dimensions.4.Value = IP address of the RS bound to the CLB instance

#### 4. Values of the input parameters in the private network CLB RS port dimension

&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name = `vip`
&Instances.N.Dimensions.0.Value = IP address
&Instances.N.Dimensions.1.Name = `loadBalancerPort`
&Instances.N.Dimensions.1.Value = Port number
&Instances.N.Dimensions.2.Name = `protocol`
&Instances.N.Dimensions.2.Value = Protocol type
&Instances.N.Dimensions.3.Name = `vpcId`
&Instances.N.Dimensions.3.Value = VPC ID of the CLB instance
&Instances.N.Dimensions.4.Name = `lanIp`
&Instances.N.Dimensions.4.Value = IP address of the RS bound to the CLB instance
&Instances.N.Dimensions.5.Name = `port`
&Instances.N.Dimensions.5.Value = Port number of the RS bound to the CLB instance
