## Namespace

Namespace=QCE/LB_PUBLIC

>?Metrics in this namespace are public network CLB monitoring metrics in four dimensions: CLB instance, listener, real server, and real server port.



## Monitoring Metrics

| Parameter | Metric | Description | Unit | Statistical Granularity |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------------- |
| ClientConnum        | Client-CLB active connections   | Number of active connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period. | -      | 10, 60, 300       |
| ClientInactiveConn  | Client-CLB inactive connections | Number of inactive connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period. | -      | 10, 60, 300       |
| ClientConcurConn    | Client-CLB concurrent connections   | Number of concurrent connections initiated from the client to the CLB instance or listener at a certain time point in the statistical period. | -      | 10, 60, 300       |
| ClientNewConn       | Client-CLB new connections   | Number of new connections initiated from the client to the CLB instance in the statistical period.     | -   | 10, 60, 300       |
| ClientInpkg         | Client-CLB inbound packets       | Number of data packets sent from the client to the CLB instance per second in the statistical period.         | Count/s   | 10, 60, 300       |
| ClientOutpkg        | Client-CLB outbound packets       | Number of data packets sent from the CLB instance to the client per second in the statistical period.         | Count/s   | 10, 60, 300       |
| ClientAccIntraffic  | Client-CLB inbound traffic       | Volume of inbound traffic from the client to the CLB instance in the statistical period.                   | MB      | 10, 60, 300       |
| ClientAccOuttraffic | Client-CLB outbound traffic       | Volume of outbound traffic from the CLB instance to the client in the statistical period.                   | MB      | 10, 60, 300       |
| ClientIntraffic     | Client-CLB inbound bandwidth       | Inbound bandwidth used by the traffic from the client to the CLB instance in the statistical period.               | Mbps    | 10, 60, 300       |
| ClientOuttraffic    | Client-CLB outbound bandwidth       | Outbound bandwidth used by the traffic from the CLB instance to the client in the statistical period.               | Mbps    | 10, 60, 300       |
| InTraffic           | CLB-real server inbound bandwidth          | Inbound bandwidth used by the traffic from the CLB instance to real servers in the statistical period.              | Mbps    | 10, 60, 300, 3600 |
| OutTraffic          | CLB-real server outbound bandwidth          | Outbound bandwidth used by the traffic from real servers to the CLB instance in the statistical period.             | Mbps    | 10, 60, 300, 3600 |
| InPkg               | CLB-real server inbound packets          | Number of data packets sent from the CLB instance to real servers per second in the statistical period.       | Count/s   | 10, 60, 300, 3600 |
| OutPkg              | CLB-real server outbound packets          | Number of data packets sent from real servers to the CLB instance per second in the statistical period.       | Count/s   | 10, 60, 300, 3600 |
| ConNum              | CLB-real server connections          | Number of connections initiated from the CLB instance to real servers in the statistical period.                 | -      | 60, 300, 3600     |
| NewConn             | CLB-real server new connections      | Number of new connections initiated from the CLB instance to real servers in the statistical period.             | Count/min | 60, 300, 3600     |
| AccOuttraffic       | CLB-real server outbound traffic          | Volume of traffic from the CLB instance to real servers in the statistical period.                 | MB      | 10, 60, 300, 3600 |
| DropTotalConns      | Dropped connections                 | Number of connections dropped by the CLB instance or listener in the statistical period. <br/>This metric is supported by only standard accounts but not traditional accounts. | -      | 60, 300, 3600     |
| InDropBits          | Dropped inbound bandwidth                 | Bandwidth dropped when the client accesses CLB over the public network within a reference period. <br/>This metric is supported by only standard accounts but not traditional accounts. | Byte    | 60, 300, 3600     |
| OutDropBits         | Dropped outbound traffic                 | Bandwidth dropped when the CLB instance accesses the public network in the statistical period.<br/>This metric is supported by only standard accounts but not traditional accounts. | Byte    | 60, 300, 3600     |
| InDropPkts          | Dropped inbound packets             | Number of data packets dropped when the client accesses the CLB instance over the public network in the statistical period.<br/>This metric is supported by only standard accounts. | Count/s   | 60, 300, 3600     |
| OutDropPkts         | Dropped outbound packets             | Number of data packets dropped when the CLB instance accesses the public network in the statistical period.<br/>This metric is supported by only standard accounts but not traditional accounts. | Count/s   | 60, 300, 3600     |
| DropQps             | Dropped QPS                   | Number of requests dropped by the CLB instance or listener in the statistical period.<br/>This metric is available to layer-7 listeners only and supported by only standard accounts but not traditional accounts. | -      | 60, 300           |
| IntrafficVipRatio   | Inbound bandwidth utilization               | Utilization of the bandwidth for the client to access the CLB instance over the public network in the statistical period.<br/>This metric is supported by only standard accounts but not traditional accounts. It is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application. | %       | 60, 300, 3600     |
| OuttrafficVipRatio  | Outbound bandwidth utilization               | Utilization of the bandwidth for the CLB instance to access the public network in the statistical period.<br/>This metric is supported by only standard accounts but not traditional accounts. It is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application. | %      | 60, 300, 3600     |
| ReqAvg              | Average request time               | Average request time of the CLB instance in the statistical period.<br/>This metric is available to layer-7 listeners only. | ms    | 60, 300, 3600     |
| ReqMax              | Maximum request time               | Maximum request time of the CLB instance in the statistical period.<br/>This metric is available to layer-7 listeners only. | ms | 60, 300, 3600     |
| RspAvg              | Average response time               | Average response time of the CLB instance in the statistical period.<br/>This metric is available to layer-7 listeners only. | ms | 60, 300, 3600     |
| RspMax              | Maximum response time               | Maximum response time of the CLB instance in the statistical period.<br/>This metric is available to layer-7 listeners only. | ms | 60, 300, 3600     |
| RspTimeout          | Timed-out responses               | Number of timed-out responses of the CLB instance per minute in the statistical period.<br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| SuccReq             | Successful requests per minute           | Number of successful requests of the CLB instance per minute in the statistical period.<br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| TotalReq            | Requests per second                 | Number of requests of the CLB instance per second in the statistical period.<br/>This metric is available to layer-7 listeners only. | -      | 60, 300, 3600     |
| ClbHttp3xx          | 3xx status codes returned by CLB      | Total number of 3xx status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| ClbHttp4xx          | 4xx status codes returned by CLB      | Total number of 4xx status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| ClbHttp5xx          | 5xx status codes returned by CLB      | Total number of 5xx status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| ClbHttp404          | 404 status codes returned by CLB      | Total number of 404 status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| ClbHttp499          | 499 status codes returned by CLB      | Total number of 499 status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| ClbHttp502          | 502 status codes returned by CLB      | Total number of 502 status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| ClbHttp503          | 503 status codes returned by CLB      | Total number of 503 status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| ClbHttp504          | 504 status codes returned by CLB      | Total number of 504 status codes returned by the CLB instance and real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http2xx             | 2xx status codes                 | Number of 2xx status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http3xx             | 3xx status codes                 | Number of 3xx status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http4xx             | 4xx status codes                 | Number of 4xx status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http5xx             | 5xx status codes                 | Number of 5xx status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http404             | 404 status codes                 | Number of 404 status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http499             | 499 status codes                 | Number of 499 status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http502             | 502 status codes                 | Number of 502 status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http503             | 503 status codes                 | Number of 503 status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| Http504             | 504 status codes                 | Number of 504 status codes returned by real servers in the statistical period. <br/>This metric is available to layer-7 listeners only. | Count/min | 60, 300, 3600     |
| OverloadCurConn     | Concurrent SNAT connections            | Number of concurrent connections to the CLB instance's SNAT IPs per minute in the statistical period. <br/>This metric is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application. | Count/min | 60, 300           |
| ConnRatio           | SNAT port utilization            | Utilization of ports of the CLB instance's SNAT IPs in the statistical period.<br/>Port utilization = number of concurrent SNAT connections / (number of SNAT IPs * 55,000 * number of real servers).<br/>This metric is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application. | %       | 60, 300           |
| SnatFail            | SNAT failures                | Number of failed connections established between the CLB instance's SNAT IPs and real servers per minute in the statistical period.<br/> This metric is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application. | Count/min | 60, 300           |
| UnhealthRsCount     | Health check exceptions             | Number of health check exceptions of the CLB instance in the statistical period.                   | -      | 60, 300           |



> ?
>
> - The statistical granularity (`period`) may vary by metric. You can call the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API to obtain the `period` supported by each metric.
> - The metric values of public network inbound packets (InPkg) and outbound packets (OutPkg) as well as public network inbound bandwidth (InTraffic) and outbound bandwidth (OutTraffic) are calculated as follows: for the ten-second statistical granularity, the metric value is the average value; for the one-minute granularity, the metric value is the maximum of the average values of every ten seconds; for the five-minute granularity, the metric value is the maximum of the average values of every minute; and so on.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Description | Format |
| ------------------------------ | ---------------- | ------------------------------------------------------------ | ------------------------------------------ |
| Instances.N.Dimensions.0.name  | vip              | Dimension name of the CLB VIP | Enter a string-type dimension name, such as `vip` |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | loadBalancerPort | Dimension name of the CLB listener port                                | Enter a string-type dimension name, such as `loadBalancerPort` |
| Instances.N.Dimensions.1.value | loadBalancerPort | Specific CLB listener port                                     | Enter a specific port number, such as 80                   |
| Instances.N.Dimensions.2.name  | protocol         | Dimension name of the listener protocol                                          | Enter a string-type dimension name, such as `protocol`         |
| Instances.N.Dimensions.2.value | protocol         | Specific listener protocol                                               | Enter a specific protocol name, such as `http`             |
| Instances.N.Dimensions.3.name  | vpcId            | Dimension name of the VPC ID                                       | Enter a string-type dimension name, such as `vpcId`            |
| Instances.N.Dimensions.3.value | vpcId            | Specific CLB VPC ID. To bind a CLB v1.0 instance across regions, see the notes below the table. | Enter a specific VPC ID, such as `5436123`         |
| Instances.N.Dimensions.4.name  | lanIp            | Dimension name of the real server IP address                                 | Enter a string-type dimension name, such as `lanIp`            |
| Instances.N.Dimensions.4.value | lanIp            | Specific real server IP address                                     | Enter a specific IP address, such as `111.222.111.22`     |
| Instances.N.Dimensions.5.name  | port             | Dimension name of the real server port                                     | Enter a string-type dimension name, such as `port`             |
| Instances.N.Dimensions.5.value | port             | Specific real server port number                                   | Enter a specific port number, such as `80`                   |

>?The `Instances.N.Dimensions.3.value` parameter is the specific ID of the VPC where the CLB instance resides. However, it is the ID of the VPC in the other region in case of binding a CLB v1.0 instance across regions.

## Input Parameter Description

Monitoring data of public network CLB can be queried based on the following four combinations of dimensions. The values for input parameters are as follows:

#### 1. Values of input parameters in public network CLB instance dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name = vip
&Instances.N.Dimensions.0.Value = IP address

#### 2. Values of input parameters in public network CLB listener dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name = vip
&Instances.N.Dimensions.0.Value = IP address
&Instances.N.Dimensions.1.Name = loadBalancerPort
&Instances.N.Dimensions.1.Value = port number
&Instances.N.Dimensions.2.Name = protocol
&Instances.N.Dimensions.2.Value = protocol type

#### 3. Values of input parameters in public network CLB real server dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name = vip
&Instances.N.Dimensions.0.Value = IP address
&Instances.N.Dimensions.1.Name = loadBalancerPort
&Instances.N.Dimensions.1.Value = port number
&Instances.N.Dimensions.2.Name = protocol
&Instances.N.Dimensions.2.Value = protocol type
&Instances.N.Dimensions.3.Name = vpcId
&Instances.N.Dimensions.3.Value = VPC ID of real server
&Instances.N.Dimensions.4.Name = lanIp
&Instances.N.Dimensions.4.Value = real server IP of CLB instance

#### 4. Values of input parameters in public network CLB real server port dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name = vip
&Instances.N.Dimensions.0.Value = IP address
&Instances.N.Dimensions.1.Name = loadBalancerPort
&Instances.N.Dimensions.1.Value = port number
&Instances.N.Dimensions.2.Name = protocol
&Instances.N.Dimensions.2.Value = protocol type
&Instances.N.Dimensions.3.Name = vpcId
&Instances.N.Dimensions.3.Value = VPC ID of CLB instance
&Instances.N.Dimensions.4.Name = lanIp
&Instances.N.Dimensions.4.Value = real server IP of CLB instance
&Instances.N.Dimensions.5.Name = port
&Instances.N.Dimensions.5.Value = Real server port number of CLB instance
