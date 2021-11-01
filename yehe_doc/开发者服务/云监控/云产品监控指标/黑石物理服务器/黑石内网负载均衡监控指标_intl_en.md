## Namespace

Namespace=QCE/BM_INTRA_LB

## Monitoring Metrics

| Metric | Description | Unit |
| ---------- | ------------------------ | ----- |
| Inpkg | Inbound packets | Packets/sec |
| Outpkg | Outbound packets | Packets/sec |
| Intraffic | Inbound bandwidth | Mbps |
| Outtraffic | Outbound bandwidth | Mbps |
| Connum | Number of current connections (for the layer-4 listener) | - |
| Req | Number of requests (for the layer-7 listener) | - |

> ? 
> - The statistical granularity (`period`) may vary for different metrics. You can obtain the `period` supported by each metric by calling [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882).
> - You can query the monitoring metrics of a BM private network CLB instance from multiple dimensions. For more information, see [Input Parameters](#.E5.85.A5.E5.8F.82.E8.AF.B4.E6.98.8E).

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as vip. |
| Instances.N.Dimensions.0.Value | vip | CLB VIP | Enter a specific IP address, such as 111.111.111.11. |
| Instances.N.Dimensions.1.Name | protocol | Dimension name of the protocol value | Enter a string-type dimension name, such as protocol. |
| Instances.N.Dimensions.1.Value | protocol | Protocol | Enter a specific protocol value, such as tcp. Possible values: tcp, udp, http, and https |
| Instances.N.Dimensions.2.Name | loadBalancerPort | Dimension name of the CLB port | Enter a string-type dimension name, such as loadBalancerPort. |
| Instances.N.Dimensions.2.Value | loadBalancerPort | CLB port | Enter a specific port number, such as 80. |
| Instances.N.Dimensions.3.Name | lanIp | Dimension name of the IP address of the real server | Enter a string-type dimension name, such as lanIp. |
| Instances.N.Dimensions.3.Value | lanIp | IP address of the real server | Enter a specific IP address, such as 11.22.33.44. |
| Instances.N.Dimensions.4.Name | rsPort | Dimension name of the port of the real server | Enter a string-type dimension name, such as rsPort. |
| Instances.N.Dimensions.4.Value | rsPort | Port of the real server | Enter a specific port number of the real server, such as 8080. |
| Instances.N.Dimensions.5.Name | vpcId | Dimension name of the integer ID of the VPC instance to which the CLB instance belongs | Enter a string-type dimension name, such as vpcId. |
| Instances.N.Dimensions.5.Value | vpcId | Integer ID of the VPC instance to which the CLB instance belongs | Enter a specific integer ID of the VPC instance to which the CLB instance belongs, such as 1. You can obtain the VPC ID from the `vpcId` field returned by the API for [querying the VPC list](https://intl.cloud.tencent.com/document/product/215/15778). |


## Input Parameters

BM private network CLB allows you to obtain the monitoring data at the following four levels:
CLB, listener, listener server, and listener server port.

**1. To obtain the monitoring data at the CLB level, set the input parameters as follows:**

&Namespace=QCE/BM_INTRA_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<VIP of the CLB instance>
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=<Integer ID of the VPC instance to which the CLB instance belongs>

**2. To obtain the monitoring data at the listener level, set the input parameters as follows:**

&Namespace=QCE/BM_INTRA_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<VIP of the CLB instance>
&Instances.N.Dimensions.1.Name=protocol
&Instances.N.Dimensions.1.Value=<Protocol value>
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=<Port of the CLB instance>
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<Integer ID of the VPC instance to which the CLB instance belongs>

**3. To obtain the monitoring data at the listener server level, set the input parameters as follows:**

&Namespace=QCE/BM_INTRA_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<VIP of the CLB instance>
&Instances.N.Dimensions.1.Name=protocol
&Instances.N.Dimensions.1.Value=<Protocol value>
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=<Port of the CLB instance>
&Instances.N.Dimensions.3.Name=lanIp
&Instances.N.Dimensions.3.Value=<IP address of the real server>
&Instances.N.Dimensions.4.Name=vpcId
&Instances.N.Dimensions.4.Value=<Integer ID of the VPC instance to which the CLB instance belongs>

**4. To obtain the monitoring data at the listener server port level, set the input parameters as follows:**

&Namespace=QCE/BM_INTRA_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<VIP of the CLB instance>
&Instances.N.Dimensions.1.Name=protocol
&Instances.N.Dimensions.1.Value=<Protocol value>
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=<Port of the CLB instance>
&Instances.N.Dimensions.3.Name=lanIp
&Instances.N.Dimensions.3.Value=<IP address of the real server>
&Instances.N.Dimensions.4.Name=rsPort
&Instances.N.Dimensions.4.Value=<Port of the real server>
&Instances.N.Dimensions.5.Name=vpcId
&Instances.N.Dimensions.5.Value=<Integer ID of the VPC instance to which the CLB instance belongs>

