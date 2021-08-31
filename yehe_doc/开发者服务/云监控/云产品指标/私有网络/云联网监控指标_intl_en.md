## Namespace

Namespace=QCE/VBC

## Monitoring Metrics

### Cross-region metrics

| Parameter | Metric | Description | Unit | Dimension |
| ------------ | ---------- | ------------ | ----- | ----------------------- |
| InBandwidth | Inbound bandwidth | Cross-region inbound bandwidth | Mbps | CcnId, SRegion, DRegion |
| OutBandwidth | Outbound bandwidth | Cross-region outbound bandwidth | Mbps | CcnId, SRegion, DRegion |
| InPkg | Inbound packets | Cross-region inbound packets | Packets/sec | CcnId, SRegion, DRegion |
| OutPkg | Outbound packets | Cross-region outbound packets | Packets/sec | CcnId, SRegion, DRegion |

### Single-region metrics

| Parameter | Metric | Description | Unit | Dimension |
| -------------------- | ---------- | ------------ | ----- | ------------- |
| RegionInBandwidthBM | Inbound bandwidth | Single-region inbound bandwidth | Mbps | CcnId, SRegion |
| RegionOutBandwidthBM | Outbound bandwidth | Single-region outbound bandwidth | Mbps | CcnId, SRegion |
| RegionInPkgBM | Inbound packets | Single-region inbound packets | Packets/sec | CcnId, SRegion |
| RegionOutPkgBM | Outbound packets | Single-region outbound packets | Packets/sec | CcnId, SRegion |


>?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.


## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | ------------------- | ------------------------------------- |
| Instances.N.Dimensions.0.Name | CcnId | CCN instance ID dimension name | Enter a String-type dimension name: CcnId |
| Instances.N.Dimensions.0.Value | CcnId | Specific CCN instance ID | Enter a specific CCN instance ID, such as `ccn-12345adc` |
| Instances.N.Dimensions.0.Name | SRegion | Source region dimension name | Enter a String-type dimension name: SRegion |
| Instances.N.Dimensions.0.Value | SRegion | Specific source region | Enter a specific source region, such as `ap-shanghai` |
| Instances.N.Dimensions.0.Name | DRegion | Destination region dimension name | Enter a String-type dimension name: DRegion |
| Instances.N.Dimensions.0.Value | DRegion | Specific destination region | Enter a specific destination region, such as `ap-guangzhou` |

## Input Parameter Description

**To query the monitoring data of a CCN instance in a VPC, set the following input parameters:**
&Namespace=QCE/VBC
&Instances.N.Dimensions.0.Name=CcnId
&Instances.N.Dimensions.0.Value=specific CCN instance ID
