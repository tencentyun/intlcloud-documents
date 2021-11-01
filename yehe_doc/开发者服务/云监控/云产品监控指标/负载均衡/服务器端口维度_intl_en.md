## Namespace

Namespace=QCE/LB_RS_UNHEALTH

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ---------------- | ----- | ---- |---- |---- |---- |
| PacketLoss     | Exceptional server ports | 	Number of server ports in an exceptional status | - |vpcid, protocol, vip, port|60s, 300s, 600s|
| Rspacketloss       | Server port exceptions | 	Number of server ports in an exceptional status |-|vip, port, domain, vpcid, protocol, url|60s, 300s, 600s|

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------- | :--------------------------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | port     | CLB port dimension name  | Enter a String-type dimension name: Port                    |
| Instances.N.Dimensions.1.value | port    | Specific CLB port    | Enter a specific port number, such as `80`                  |
| Instances.N.Dimensions.2.name  | protocol | Protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.2.value | protocol | Specific protocol name                | Enter a specific protocol name, such as `http`            |
| Instances.N.Dimensions.3.name  | vpcId    | VPC ID dimension name       | Enter a String-type dimension name: vpcId                              |
| Instances.N.Dimensions.3.value | vpcId    | Specific CLB VPC ID | Enter a specific VPC ID, such as `1111`. You should enter a numerical `vpcId`. For more information on how to get a `NumericalvpcId`, please see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |
| Instances.N.Dimensions.4.name  | domain   | Domain name dimension name              | Enter a String-type dimension name: domain                             |
| Instances.N.Dimensions.4.value | domain   | Specific domain name                     | Enter a specific domain name, such as `www.cloud.tencent.com`.                   |
| Instances.N.Dimensions.5.name  | url      | URL dimension name               | Enter a String-type dimension name: url                                |
| Instances.N.Dimensions.5.value | url      | Specific URL                     | Enter a specific URL, such as `/aaa`                                     |


## Input Parameter Description

**Input parameters for CLB - server port (other) - server port dimension:**

&Namespace=QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=port
&Instances.N.Dimensions.1.Value=Specific port of CLB instance
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Specific protocol name
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=VPC ID of CLB instance
&Instances.N.Dimensions.4.Name=domain
&Instances.N.Dimensions.4.Value=Specific domain name
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=Specific URL

