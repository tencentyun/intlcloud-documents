## Namespace

Namespace=QCE/BM_LB

## Monitoring Metrics

| Metric | Description | Unit | Dimension |
| ------------- | ---------- | ----- | ---- |
| EipOuttraffic | Public network outbound bandwidth | Mbps | vip  |
| EipIntraffic | Public network inbound bandwidth | Mbps | vip |
| EipOutpkg | Public network outbound packets | Packets/sec | vip |
| EipInpkg | Public network inbound packets | Packets/sec | vip |

> ? The statistical granularity (`period`) may vary by metrics. You can obtain the `period` supported by each metric by calling the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Overview of parameters in each dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | -------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name | vip | Dimension name of the EIP | Enter a string-type dimension name, such as vip |
| Instances.N.Dimensions.0.Value | vip | EIP | Enter a specific EIP, such as 115.115.115.115. You can query the list of EIPs under your account by calling DescribeEipBm |

## Input Parameters

To query the monitoring data of BM EIP, configure input parameters as follows:

&Namespace=QCE/BM_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value==<EIP to be queried>
