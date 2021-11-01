## Namespace

Namespace=QCE/ECM_LB

## Monitoring Metrics

| Parameter | Meaning | Description | Unit | Statistical Periods |
| ---------- | ---------- | -------------------------------------------------- | ----- | -------------------- |
| ConNum        | Current connections | Number of connections on the CLB or its listeners in the statistical period | Connections | 60s, 300s, 3600s, 86400s |
| NewConn  | New connections | Number of newly established connections on the CLB or its listeners in the statistical period |Connections/sec| 60s, 300s, 3600s, 86400s |
| InPkg         | Inbound packets | Number of request data packets received by the CLB per second in the statistical period |Packets/sec | 10s, 60s, 300s, 3600s, 86400s |
| InTraffic     | Inbound bandwidth | Bandwidth used by the client to access the CLB via public networks in the statistical period | Mbps|10s, 60s, 300s, 3600s, 86400s |
| OutPkg | Outbound packets | Number of data packets sent by the CLB per second in the statistical period | Packets/sec |10s, 60s, 300s, 3600s, 86400s |
| OutTraffic  | Outbound bandwidth | Bandwidth used by the CLB to access public networks in the statistical period |Mbps    |10s, 60s, 300s, 3600s, 86400s  |

> ?Statistical periods (Period) may vary from metric to metric. You can get the periods different metrics support by calling the `DescribeBaseMetrics` API.


## Dimensions and Parameters

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------ |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name: `vip`. |
| Instances.N.Dimensions.0.value | vip | A CLB VIP | Enter an IP address, e.g., `111.111.111.11`. |
| Instances.N.Dimensions.1.name | loadBalancerPort | Dimension name of the CLB port | Enter a string-type dimension name: `loadBalancerPort`. |
| Instances.N.Dimensions.1.value | loadBalancerPort | A CLB listener port | Enter a port number, e.g., `80`. |
| Instances.N.Dimensions.2.name | protocol | Dimension name of the listener protocol | Enter a string-type dimension name: `protocol`. |
| Instances.N.Dimensions.2.value | protocol | A listener protocol | Enter a protocol, e.g., `TCP` or `UDP`. |
| Instances.N.Dimensions.3.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name: `vpcId`. |
| Instances.N.Dimensions.3.value | vpcId | VPC ID of the CLB instance | Enter a VPC ID, e.g., `vpc-1ywqac83`. |
| Instances.N.Dimensions.4.name | lanIp | Dimension name of the IP address of the real server | Enter a string-type dimension name: `lanIp`. |
| Instances.N.Dimensions.4.value | lanIp | Private IP address of the real server | Enter an IP address, e.g., `10.12.111.22`. |
| Instances.N.Dimensions.5.name | port | Dimension name of the real server port | Enter a string-type dimension name: `port`. |
| Instances.N.Dimensions.5.Value | port | Service port number of the real server | Enter a port number, e.g., `80`. |

## Input Parameters

You can query the monitoring data of CLB instances in four dimensions, the input parameters for which are as follows:

#### 1. Query at the instance-level

&Namespace: `QCE`/`ECM_LB`
&Instances.N.Dimensions.0.Name=`vip`
&Instances.N.Dimensions.0.Value=VIP of the CLB instance

#### 2. Query at the listener-level

&Namespace: `QCE`/`ECM_LB`
&Instances.N.Dimensions.0.Name=`vip`
&Instances.N.Dimensions.0.Value=VIP of the CLB instance
&Instances.N.Dimensions.1.Name=`loadBalancerPort`
&Instances.N.Dimensions.1.Value=Listener port number
&Instances.N.Dimensions.2.Name=`protocol`
&Instances.N.Dimensions.2.Value=Protocol

#### 3 Query at the real server-level

&Namespace: `QCE`/`ECM_LB`
&Instances.N.Dimensions.0.Name=`vip`
&Instances.N.Dimensions.0.Value=VIP of the CLB instance
&Instances.N.Dimensions.1.Name=`loadBalancerPort`
&Instances.N.Dimensions.1.Value=Listener port number
&Instances.N.Dimensions.2.Name=`protocol`
&Instances.N.Dimensions.2.Value=Protocol
&Instances.N.Dimensions.3.Name=`vpcId`
&Instances.N.Dimensions.3.Value=VPC ID of the CLB instance
&Instances.N.Dimensions.4.Name=`lanIp`
&Instances.N.Dimensions.4.Value=Private IP address of the real server

#### 4. Query at the real server port-level

&Namespace: `QCE`/`ECM_LB`
&Instances.N.Dimensions.0.Name=`vip`
&Instances.N.Dimensions.0.Value=VIP of the CLB instance
&Instances.N.Dimensions.1.Name=`loadBalancerPort`
&Instances.N.Dimensions.1.Value=Listener port number
&Instances.N.Dimensions.2.Name=`protocol`
&Instances.N.Dimensions.2.Value=Protocol
&Instances.N.Dimensions.3.Name=`vpcId`
&Instances.N.Dimensions.3.Value=VPC ID of the CLB instance
&Instances.N.Dimensions.4.Name=`lanIp`
&Instances.N.Dimensions.4.Value=Private IP address of the real server
&Instances.N.Dimensions.5.Name=`port`
&Instances.N.Dimensions.5.Value=Service port number of the real server
