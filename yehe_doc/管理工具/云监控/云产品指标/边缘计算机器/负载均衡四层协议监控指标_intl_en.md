## Namespace

Namespace=QCE/ECM_LB

## Monitored Metrics

| Parameter | Metric Name | Description | Unit | Statistical Period |
| ---------- | ---------- | -------------------------------------------------- | ----- | -------------------- |
| ConNum        | Number of connections | Number of connections on CLB or the listener within the statistical period |-  | 60, 300, 3600, 86400 |
| InPkg         | Inbound packets | Number of request data packets received by CLB per second within the statistical period |Packets/sec | 60, 300, 3600, 86400 |
| InTraffic     | Inbound bandwidth | Bandwidth used by the client to access CLB over the public network within the statistical period | Mbps  |  60, 300, 3600, 86400 |
| NewConn  | New connections | Number of newly established connections on CLB or the listener within the statistical period |Connections/sec|60, 300, 3600, 86400 |
| OutPkg | Outbound packets | Number of data packets sent by CLB per second within the statistical period |Packets/sec|60, 300, 3600, 86400 |
| OutTraffic  | Outbound bandwidth | Bandwidth used by CLB to access the public network within the statistical period |Mbps    | 60, 300, 3600, 86400 |

> ?Statistical periods of each metric may differ. You can call the `DescribeBaseMetrics` API to obtain the supported periods of each metric.


## Dimension Parameters

| Parameter | Dimension | Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------ |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as `vip` |
| Instances.N.Dimensions.0.value | vip | A specific CLB VIP | Enter a specific IP address, such as `111.111.111.11` |
| Instances.N.Dimensions.1.name | loadBalancerPort | Dimension name of the CLB port | Enter a string-type dimension name, such as `loadBalancerPort` |
| Instances.N.Dimensions.1.value | loadBalancerPort | A specific CLB listener port | Enter a specific port number, such as `80` |
| Instances.N.Dimensions.2.name | protocol | Dimension name of the listening protocol | Enter a string-type dimension name, such as `protocol` |
| Instances.N.Dimensions.2.value | protocol | A specific listening protocol | Enter a specific protocol name, such as `TCP` or `UDP` |
| Instances.N.Dimensions.3.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name, such as `vpcId` |
| Instances.N.Dimensions.3.value | vpcId | VPC ID of the CLB instance | Enter a specific VPC ID, such as `vpc-1ywqac83` |
| Instances.N.Dimensions.4.name | lanIp | Dimension name of the IP address of the real server | Enter a string-type dimension name, such as `lanIp` |
| Instances.N.Dimensions.4.value | lanIp | IP address of the real server | Enter a specific IP address, such as `111.222.111.22` |
| Instances.N.Dimensions.5.name | port | Dimension name of the real server | Enter a string-type dimension name, such as `port` |
| Instances.N.Dimensions.5.Value | port | A specific service port number of the real server | Enter a specific port number, such as `80` |

## Input Parameters

CLB instances support querying the monitoring data with four dimension combinations. Input parameters of each combination are described respectively as follows:

#### 1. Values of the input parameters at the CLB instance dimension

&Namespace: QCE/ECM_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address

#### 2. Values of the input parameters at the CLB listener dimension

&Namespace: QCE/ECM_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type

#### 3 Values of the input parameters at the CLB real server dimension

&Namespace: QCE/ECM_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<VPC ID of the real server>
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>

#### 4. Values of the input parameters at the CLB real server port dimension

&Namespace: QCE/ECM_LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=VPC ID of the CLB instance
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>
&Instances.N.Dimensions.5.Name=port
&Instances.N.Dimensions.5.Value=Port number of the server bound to the CLB instance
