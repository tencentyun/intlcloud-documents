## Namespace

Namespace=QCE/CEIP_SUMMARY

## Monitoring Metrics

#### Anycast EIP

| Parameter | Metric | Description | Unit | Dimension |
| ------------- | ---------- | ----------------------- | ----- | ---- |
| VipInpkg      | Inbound packets     | Inbound packets of Anycast EIP | Packets/sec | vip |
| VipOutpkg     | Outbound packets     | Outbound packets of Anycast EIP | Packets/sec | vip |
| VipIntraffic  | Inbound bandwidth     | Inbound bandwidth of Anycast EIP | Mbps  | vip |
| VipOuttraffic | Outbound bandwidth     | Outbound bandwidth of Anycast EIP | Mbps  | vip  |

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | ---------------------- | -------------------------------------- |
| Instances.N.Dimensions.0.Name  | vip | EIP dimension name | Enter a String-type dimension name: vip           |
| Instances.N.Dimensions.0.Value | vip      | Specific EIP address  | Enter a specific IP address, such as `111.111.111.11` |

## Input Parameter Description

**To query the monitoring data of an EIP in a VPC, set the following input parameters:**
&Namespace=QCE/CEIP_SUMMARY
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=unique EIP ID

