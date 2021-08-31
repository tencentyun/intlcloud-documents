## Namespace

Namespace=QCE/LB

## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension |
| ------------- | ---------- | ---------------- | ----- | ---- |
| VipIntraffic  | Inbound bandwidth     | Inbound bandwidth of EIP | Mbps  | eip  |
| VipOuttraffic | Outbound bandwidth     | Outbound bandwidth of EIP | Mbps  | eip  |
| VipInpkg      | Inbound packets     | Inbound packets of EIP | Packets/sec | eip  |
| VipOutpkg     | Outbound packets     | Outbound packets of EIP | Packets/sec | eip  |
| AccOuttraffic | Outbound traffic     | Outbound traffic of EIP | MB    | eip  |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | ------------------------------ | -------------------------------------- |
| Instances.N.Dimensions.0.Name  | eip      | EIP or IPv6 dimension name | Enter a String-type dimension name: eip     |
| Instances.N.Dimensions.0.Value | eip      | EIP or IPv6 address  | Enter a specific IP address, such as `111.111.111.11` |

## Input Parameter Description

**To query the monitoring data of an EIP in a VPC, set the following input parameters:**
&Namespace=QCE/LB
&Instances.N.Dimensions.0.Name=eip
&Instances.N.Dimensions.0.Value=unique EIP ID
