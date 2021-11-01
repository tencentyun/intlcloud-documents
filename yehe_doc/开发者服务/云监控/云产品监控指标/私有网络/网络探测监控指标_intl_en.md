## Namespace

Namespace=QCE/VPC_NET_DETECT

## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension |
| ---------- | ---------- | -------------- | ---- | ----------- |
| PkgDrop | Packet loss rate | Network detection packet loss rate | % | netdetectid |
| Delay | Delay | Network detection delay | ms | netdetectid |

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ----------- | -------------------- | ------------------------------------- |
| Instances.N.Dimensions.0.Name  | netdetectid | Network detection instance dimension name | Enter a String-type dimension name: netdetectid  |
| Instances.N.Dimensions.0.Value | netdetectid | Specific network detection instance ID  | Enter a specific instance ID, such as `netd-12345678` |

## Input Parameter Description

**To query the monitoring data of an EIP in a VPC, set the following input parameters:**
&Namespace=QCE/VPC_NET_DETECT
&Instances.N.Dimensions.0.Name=netdetectid
&Instances.N.Dimensions.0.Value=specific network detection instance ID
