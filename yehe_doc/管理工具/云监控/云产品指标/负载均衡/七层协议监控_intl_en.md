## Namespace

Namespace=QCE/LOADBALANCE

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| -------------- | ------------------ | ------------------------------------------------------------ | ---------------------- | -------------------- | ----------------------------------------------- |
| Clbhttp404     | 404 status codes returned by CLB | Number of 404 status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Clbhttp4xx     | 4xx status codes returned by CLB | Number of 4xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Clbhttp502     | 502 status codes returned by CLB | Number of 502 status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Clbhttp5xx     | 5xx status codes returned by CLB | Number of 5xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| PortConnum     | Active connections         | Number of active connections from the client to the layer-7 CLB in the statistical period   | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Http2xx        | 2xx status codes         | Number of 2xx status codes returned by the real server in the statistical period                | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Http3xx        | 3xx status codes         | Number of 3xx status codes returned by the real server in the statistical period                | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Http404        | 404 status codes         | Number of 404 status codes returned by the real server in the statistical period                | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Http4xx        | 4xx status codes         | Number of 4xx status codes returned by the real server in the statistical period                | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Http502        | 502 status codes         | Number of 502 status codes returned by the real server in the statistical period                | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Http5xx        | 5xx status codes         | Number of 5xx status codes returned by the real server in the statistical period                | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Clbhttp3xx     | 3xx status codes returned by CLB | Number of 3xx status codes returned by CLB in the statistical period (sum of CLB and real server return codes) | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Portinpkg      | Inbound packets     | Number of request packets received by the layer-7 CLB per second                    | Packets/sec                  | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Portintraffic  | Inbound bandwidth     | Bandwidth consumed when the layer-7 CLB is accessed externally                       | bps                    | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Portnewconn    | New connections | Number of new connections established from the client to the layer-7 CLB in the statistical period | -                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Portoutpkg     | Outbound packets     | Number of packets sent by the layer-7 CLB per second                         | Packets/sec                  | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Portouttraffic | Outbound bandwidth     | Bandwidth consumed when the layer-7 CLB accesses externally                         | bps                    | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Rspavg         | Average response time       | Average response time of CLB in the statistical period                            | ms                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Rspmax         | Maximum response time       | Maximum response time of CLB in the statistical period                            | ms                     | vip, protocol, vpcId | 60, 300, 3600, 86400 |
| Totalreq       | Requests per second         | Number of CLB requests per second in the statistical period, i.e., QPS                  | Requests/sec                  | vip, protocol, vpcId | 60, 300, 3600, 86400 |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------- | :--------------------------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | protocol | Protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.1.value | protocol | Specific protocol name                | Enter a specific protocol name, such as `http`            |
| Instances.N.Dimensions.2.name  | vpcId    | VPC ID dimension name       | Enter a String-type dimension name: vpcId                              |
| Instances.N.Dimensions.2.value | vpcId    | Specific CLB VPC ID | Enter a specific VPC ID, such as `1111`. You should enter a numerical `vpcId`. For more information on how to get a `NumericalvpcId`, please see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |


## Input Parameter Description

**Input parameters for monitoring layer-7 CLB:**

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=protocol
&Instances.N.Dimensions.1.Name=Protocol type
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=vpcId
&Instances.N.Dimensions.2.Value=VPC ID of CLB instance

