## Namespace

Namespace=QCE/VBC

## Monitoring Metrics

### Single-region metrics

| Metric Name | Description | Unit | Dimension |
| ------------------ | :------- | :---- | :------ |
| RegionOutPkg | Single-region outbound packets | Packets/sec | CcnId |
| RegionInPkg | Single-region inbound packets | Packets/sec | CcnId |
| RegionOutBandwidth | Single-region outbound bandwidth | Mbps | CcnId |
| RegionInBandwidth | Single-region inbound bandwidth | Mbps | CcnId |

### Cross-region metrics

| Metric Name | Description | Unit | Dimension |
| ------------------ | :------- | :---- | :------ |
| OutPkg | Cross-region outbound packets | Packets/sec | CcnId, SRegion, and DRegion |
| InPkg | Cross-region inbound packets | Packets/sec | CcnId, SRegion, and DRegion |
| OutBandwidth | Cross-region outbound bandwidth | Mbps | CcnId, SRegion, and DRegion |
| InBandwidth | Cross-region inbound bandwidth | Mbps | CcnId, SRegion, and DRegion |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.


## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | ------------------- | ------------------------------------- |
| Instances.N.Dimensions.0.Name | CcnId | Dimension name of the CCN instance ID | Enter a string-type CcnId dimension name |
| Instances.N.Dimensions.0.Value | CcnId | A specific CCN ID | Enter a specific CCN ID, such as ccn-12345adc |
| Instances.N.Dimensions.0.Name | SRegion | Dimension name of the source region | Enter a string-type SRegion dimension name |
| Instances.N.Dimensions.0.Value | SRegion | A specific source region | Enter a specific source region, such as `ap-shanghai` |
| Instances.N.Dimensions.0.Name | DRegion | Dimension name of the destination region | Enter a string-type DRegion dimension name |
| Instances.N.Dimensions.0.Value | DRegion | A specific destination region | Enter a specific destination region, such as `ap-guangzhou` |

## Input Parameters

To query the monitoring data of a CCN instance in a VPC instance, use the following input parameters:
&Namespace=QCE/VBC
&Instances.N.Dimensions.0.Name=CcnId
&Instances.N.Dimensions.0.Value=ccn-c889docn
