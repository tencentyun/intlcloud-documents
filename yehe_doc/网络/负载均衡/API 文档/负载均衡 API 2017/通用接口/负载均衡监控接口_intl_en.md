## API Description

This API is used to get the monitoring data of the CLB instance by passing in the namespace, object dimension description, and monitoring metric of the instance.

Domain name for API calls: `monitor.api.qcloud.com`

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `GetMonitorData`.

<table class="t">
<tbody>
<tr>
<th><b>Parameter</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> namespace
<td> Yes
<td> String
<td> Namespace. Each Tencent Cloud service has a namespace. There are two namespaces for CLB: qce/lb_public for public network CLB and qce/lb_private for private network CLB.
<tr>
<td> metricName
<td> Yes
<td> String
<td> Monitoring metric to be obtained, such as `connum` for current connection, and `intraffic` for inbound bandwidth. For more information, see the table below.
<tr>
<td> dimensions.n.name
<td> Yes
<td> String
<td>Dimension name. You can use a combination of dimensions to get the monitoring data. Each namespace has different dimension structures as shown in the table below. This parameter should be used with `dimensions.n.value`.
<tr>
<td> dimensions.n.value
<td> Yes
<td> String
<td> Values of a specified dimension.
<tr>
<td> startTime
<td> No
<td> Datetime
<td> Start time such as 2017-01-01 00:00:00. The default time is 00:00:00 on the current day.
<tr>
<td> endTime
<td> No
<td> Datetime
<td> End time such as 2017-01-01 10:00:00. The current time is used by default. <br>Note: it cannot be earlier than `startTime`, and we recommend configuring it on the same day as `startTime`.
<tr>
<td> period
<td> No
<td> Int
<td> Statistical period for monitoring data. Valid values: 60s and 300s. If this parameter is not passed in, 300s will be used by default.
</tbody>
</table>




Currently, CLB supports displaying the following metrics (metricName)

| Metric | Description | Unit |
|---------|---------|---------|
| Connum | Current connections | - |
| new_conn | New connections | - |
| Intraffic | Inbound bandwidth | Mbps |
| outtraffic | Outbound bandwidth | Mbps |
| inpkg | Inbound packets | Packets/sec |
| outpkg | Outbound packets | Packets/sec |

The namespaces of CLB instances and their respective monitoring dimensions are described as follows:

###  Public network CLB instance namespace qce/lb_public
The `qce/lb_public` namespace can be used to query all the monitoring data of the public network CLB instances.
qce/lb_public supports the following dimension groups:
- Public network CLB dimension
This dimension reflects the overall monitoring metric of a public network CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
|  VIP | CLB VIP | IP address, such as 111.111.111.11 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a> &gt;
&namespace=qce/lb_public
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
</pre>

- Public network CLB port dimension
This dimension reflects the monitoring metric of the port on a public network CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP| CLB VIP | IP address, such as 111.111.111.11|
|  loadBalancerPort | Port | Int, such as 80 |
|  protocol | Protocol | String, such as TCP |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a> &gt;
&namespace=qce/lb_public
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=loadBalancerPort
&dimensions.1.value=80
&dimensions.2.name=protocol
&dimensions.2.value=tcp
</pre>

- Public network CLB real server dimension
This dimension reflects the monitoring metric of the real server bound to a public network CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11 |
| loadBalancerPort | CLB port | Int, such as 80 |
| protocol | Protocol | String, such as TCP |
| vpcId | VPC ID of the CLB instance | Int, such as 1111 |
| lanIp | IP address of the real server bound to the CLB instance | IP address, such as 111.111.111.11 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a> &gt;
&namespace=qce/lb_public
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=loadBalancerPort
&dimensions.1.value=80
&dimensions.2.name=protocol
&dimensions.2.value=tcp
&dimensions.3.name=vpcId
&dimensions.3.value=1111
&dimensions.4.name=lanIp
&dimensions.4.value=111.222.111.22
</pre>

- Public network CLB real server port dimension
This dimension reflects the monitoring metric of a port on the real server bound to a public network CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11 |
| loadBalancerPort | CLB port | Int, such as 80 |
|  protocol | Protocol | String, such as TCP |
| vpcId | VPC ID of the CLB instance | Int, such as 1111 |
| lanIp | IP address of the real server bound to the CLB instance | IP address, such as 111.111.111.11 |
|  port | Port number of the real server bound to the CLB instance | Int, such as 80 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a> &gt;
&namespace=qce/lb_public
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=loadBalancerPort
&dimensions.1.value=80
&dimensions.2.name=protocol
&dimensions.2.value=tcp
&dimensions.3.name=vpcId
&dimensions.3.value=1111
&dimensions.4.name=lanIp
&dimensions.4.value=111.222.111.22
&dimensions.5.name=port
&dimensions.5.value=80
</pre>

### Private network CLB instance namespace qce/lb_private
The `qce/lb_private` namespace can be used to query all monitoring data of the private network CLB instance.

- Private network CLB dimension
This dimension reflects the overall monitoring metric of a private network CLB instance. The dimension (dimensions.n.name) to be specified is as follows. Since the private VIP may be repeated, `vpcId` is also required to uniquely specify a CLB instance:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP| CLB VIP | IP address, such as 111.111.111.11 |
| vpcId | VPC ID of the CLB instance | Int, such as 1111 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&<<a href="https://intl.cloud.tencent.com/document/api/214">Common request parameters</a>>
&namespace=qce/lb_private
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=vpcId
&dimensions.1.value=1111
</pre>

- Private network CLB port dimension
This dimension reflects the monitoring metric of the port on a private network instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11 |
| vpcId | VPC ID of the CLB instance | Int, such as 1111 |
| loadBalancerPort | CLB port | Int, such as 80 |
|  protocol | Protocol | String, such as http |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&<<a href="https://intl.cloud.tencent.com/document/api/214">Common request parameters</a>>
&namespace=qce/lb_private
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=vpcId
&dimensions.1.value=1111
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
</pre>



- Private network CLB real server dimension
This dimension reflects the monitoring metric of the real server bound to a private network CLB instance. The dimension (dimensions.n.name) to be specified is as follows. Since the private VIP may be repeated, `vpcId` is also required to uniquely specify a CLB instance:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11 |
| vpcId | VPC ID of the CLB instance | Int, such as 1111 |
| loadBalancerPort | CLB port | Int, such as 80 |
| protocol | Protocol | String, such as http |
| lanIp | IP address of the real server bound to the CLB instance | IP address, such as 111.111.111.11 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&<<a href="https://intl.cloud.tencent.com/document/api/214">Common request parameters</a>>
&namespace=qce/lb_private
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=vpcId
&dimensions.1.value=1111
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
&dimensions.4.name=lanIp
&dimensions.4.value=111.222.111.22
</pre>

- Private network CLB real server port dimension
This dimension reflects the monitoring metric of a port on the real server bound to a private network CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11 |
| vpcId | VPC ID of the CLB instance | Int, such as 1111 |
| loadBalancerPort | CLB port | Int, such as 80 |
| protocol | Protocol | String, such as http |
| lanIp | IP address of the real server bound to the CLB instance | IP address, such as 111.111.111.11 |
| port | Port number of the real server bound to the CLB instance | Int, such as 80 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&<<a href="https://intl.cloud.tencent.com/document/api/214">Common request parameters</a>>
&namespace=qce/lb_private
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=vpcId
&dimensions.1.value=1111
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
&dimensions.4.name=lanIp
&dimensions.4.value=111.222.111.22
&dimensions.5.name=port
&dimensions.5.value=80
</pre>

### CLB instance dimension namespace qce/loadbalance (updated)
The `qce/loadbalance` namespace can be used to query the monitoring data of the CLB instance at the application layer. 

Currently, the CLB instance namespace supports displaying the metrics (metricName) as follows:

| Metric | Description | Unit |
|---------|---------|---------|
| connum | Current (active) connections | Connections/min |
| new_conn | New connections | Connections/min |
| intraffic | Inbound traffic | Mbps |
| outtraffic | Outbound traffic | Mbps |
| inpkg | Inbound packets | Packets/sec |
| outpkg | Outbound packets | Packets/sec |
| httpCode_2XX | 2xx status codes | Codes/min |
| httpCode_3XX | 3xx status codes | Codes/min |
| httpCode_4XX | 4xx status codes | Codes/min |
| httpCode_5XX | 5xx status codes | Codes/min |
| httpCode_404 | 404 status codes | Codes/min |
| httpCode_502 | 502 status codes | Codes/min |
| response_time_max | Maximum response time | ms |
| response_time_average | Average response time | ms |
| response_timeout_num | Timed-out responses | Responses/min |
| QPS | Requests per second | - |

qce/loadbalance supports the following dimension groups:

- CLB VPI dimension
This dimension reflects the overall monitoring metric of a CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11 |


API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/loadbalance
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
</pre>


- CLB listener port dimension
This dimension reflects the monitoring metric of the port on a CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
|VIP | CLB VIP | IP address, such as 111.111.111.11|
|  loadBalancerPort | Port | Int, such as 80 |
|  protocol | Protocol | String, such as http |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/loadbalance
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
</pre>


- CLB forwarding domain name dimension
This dimension reflects the monitoring metric of the CLB forwarding domain name. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11|
|  loadBalancerPort | Port | Int, such as 80 |
|  protocol | Protocol | String, such as http |
|  domain| Forwarding domain name | String, such as www.domain.com |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/loadbalance
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=domain
&dimensions.1.value=www.domian.com
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
</pre>

- CLB forwarding path dimension
This dimension reflects the monitoring metric of the CLB forwarding path. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11|
| loadBalancerPort | Port | Int, such as 80 |
| protocol | Portocol | String, such as http |
| domain| Forwarding domain name | String, such as www.domain.com|
| url | Forwarding path | String, such as /url |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/loadbalance
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=domain
&dimensions.1.value=www.domian.com
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
&dimensions.3.name=url
&dimensions.3.value=/url
</pre>

- CLB real server IP dimension
This dimension reflects the monitoring metric of the IP of the real server bound to a CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
| VIP | CLB VIP | IP address, such as 111.111.111.11|
| loadBalancerPort | Port | Int, such as 80 |
| protocol | Portocol | String, such as http |
| domain| Forwarding domain name | String, such as www.domain.com |
| url | Forwarding path | String, such as /url |
| vpcId | VPC ID of the CLB instance | Int, such as 1111 |
| lanIp | IP address of the real server bound to the CLB instance | IP address, such as 111.111.111.11 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/loadbalance
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=vpcId
&dimensions.1.value=1111
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
&dimensions.4.name=lanIp
&dimensions.4.value=111.222.111.22
&dimensions.1.name=domain
&dimensions.1.value=www.domian.com
&dimensions.3.name=url
&dimensions.3.value=/url
</pre>

- CLB real server port dimension
This dimension reflects the monitoring metric of the port on the real server bound to a CLB instance. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
|  VIP | CLB VIP | IP address, such as 111.111.111.11 |
| loadBalancerPort | Port | Int, such as 80 |
|  protocol | Protocol | String, such as http |
| domain| Forwarding domain name | String, such as www.domain.com |
| url | Forwarding path | String, such as /url |
|  vpcId | VPC ID of the CLB instance | Int, such as 1111 |
| lanIp | IP address of the real server bound to the CLB instance | IP address, such as 111.111.111.11 |
|  port | Port number of the real server bound to the CLB instance | Int, such as 80 |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/loadbalance
&metricName=connum
&dimensions.0.name=vip
&dimensions.0.value=111.111.111.11
&dimensions.1.name=vpcId
&dimensions.1.value=1111
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&dimensions.3.name=protocol
&dimensions.3.value=http
&dimensions.4.name=lanIp
&dimensions.4.value=111.222.111.22
&dimensions.5.name=port
&dimensions.5.value=80
&dimensions.1.name=domain
&dimensions.1.value=www.domian.com
&dimensions.3.name=url
&dimensions.3.value=/url
</pre>

## Response Parameters

<table class="t"><tbody><tr>
<th><b>Parameter</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> code
<td> Int
<td>Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Common Error Codes" target="_blank">Common Error Codes</a>.
<tr>
<td> codeDesc
<td> String
<td> Error code.
<tr>
<td> message
<td> String
<td> Detailed error message.
<tr>
<td> startTime
<td> Datetime
<td> Start time.
<tr>
<td> endTime
<td> Datetime
<td> End time.
<tr>
<td> metricName
<td> String
<td> Metric name.
<tr>
<td> period
<td> Int
<td> Statistical period for monitoring data.
<tr>
<td> dataPoints
<td> Object
<td> Monitoring data list. Each element of the array stands for the data read at the monitoring time point.
</tbody></table>

## Example
Request
<pre>
 
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/lb_public
&metricName=connum
&dimensions.0.name=protocol
&dimensions.0.value=HTTP
&dimensions.1.name=vip
&dimensions.1.value=111.111.111.111
&dimensions.2.name=loadBalancerPort
&dimensions.2.value=80
&startTime=2015-12-28 14:00:00
&endTime=2015-12-28 14:05:00
&period=300
</pre>
Response
```
{
    "code": 0,
    "message": "",
    "metricName": "connum",
    "startTime": "2015-12-28 14:00:00",
    "endTime": "2015-12-28 14:05:00",
    "period": 300,
    "dataPoints":  [
           0
        ]
}
```
- Forwarding domain name dimension
This dimension reflects the monitoring metric of the CLB instance(s) which configured the same forwarding domain name. The dimension (dimensions.n.name) to be specified is as follows:

| Dimension | Description | Format |
|---------|---------|---------|
|  loadBalancerPort | Port | Int, such as 80 |
|  protocol | Protocol | String, such as http |
| domain| Forwarding domain name | String, such as www.domain.com |

API calling sample using the dimension:
<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&&lt;<a href="https://intl.cloud.tencent.com/document/product/213/31574" target="_blank">Common request parameters</a>&gt;
&namespace=qce/loadbalance
&metricName=QPS
&dimensions.0.name=domain
&dimensions.0.value=www.domian.com
&dimensions.1.name=loadBalancerPort
&dimensions.1.value=80
&dimensions.2.name=protocol
&dimensions.2.value=http
</pre>

 
