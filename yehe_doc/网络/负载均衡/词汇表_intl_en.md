
### Security group

A security group is a stateful virtual firewall capable of filtering packets. It can be used to set network access controls for one or more CVM instances. Instances with the same network security isolation demands in one region can be put into the same security group, and their outbound and inbound traffic can be filtered through the network policy of the group.

### CLB

For more information, please see [Cloud Load Balancer](#clb).

### Region

A region is where Tencent Cloud managed data centers are located. There can be different availability zones (AZs) in one region.
For example, Beijing is a region where managed data centers are located, while Beijing Zone 1 is an AZ. Tencent Cloud services in the same region can communicate with each other over the private network, while those in different regions cannot. You are recommended to select the region closest to your end users so as to minimize access latency and improve download speed.

<span id="clb"></span>
### Cloud Load Balancer

Cloud Load Balancer (CLB) is a secure, stable, and elastically scalable traffic distribution service provided by Tencent Cloud. It can improve system availability by avoiding single points of failure.

### CLB listener

A CLB listener provides request distribution rules and consists of listening ports, load balancing policies, and health check configurations. Requests are forwarded to the real server according to listener configurations. A CLB instance should have at least one listener.

### CLB instance

A CLB instance is a running CLB service. To use CLB, a CLB instance must be created first.

<span id="RS"></span>
### Real server

A real server (RS) is a set of CVM instances that are used to process the requests distributed by CLB.

### RS

For more information, please see [Real server](#RS).

<span id="vpc"></span>
### Virtual private cloud

A virtual private cloud (VPC) builds a separate network space in Tencent Cloud, which is very similar to a traditional network run in your IDC, except that the services hosted in a VPC are resources of your Tencent Cloud services such as [CVM](https://intl.cloud.tencent.com/document/product/213), [CLB](https://intl.cloud.tencent.com/document/product/214), and [TencentDB](https://intl.cloud.tencent.com/document/product/236). You don't have to care about the procurement and OPS of network devices at all; instead, you only need to customize IP ranges, IP addresses, routing policies, etc. through easy-to-use software programs. You can use [EIPs](https://intl.cloud.tencent.com/document/product/213/16586), [NAT gateways](https://intl.cloud.tencent.com/document/product/1015), and [public gateways](https://intl.cloud.tencent.com/document/product/213/34835) to flexibly access the internet or interconnect a VPC with your IDC through [VPN](https://intl.cloud.tencent.com/document/product/215) or [Direct Connect](https://intl.cloud.tencent.com/document/product/216). In addition, the [peering connection](https://intl.cloud.tencent.com/document/product/553) service of VPC can help you easily implement unified server for global access and 2-region-3-DC disaster recovery, and the security group and [network ACL](https://intl.cloud.tencent.com/document/product/215/31850) features of VPC can satisfy your network security needs in a multi-dimension and comprehensive manner.

### VIP

For more information, please see [Virtual IP](#vip).

### VPC

For more information, please see [Virtual Private Cloud](#vpc).

<span id="vip"></span>
### Virtual IP

A virtual IP (VIP) is an IP address assigned by the system to a CLB instance. You can choose whether to open it to the internet so as to create a private network or public network CLB instance. You can resolve a domain name to a public VIP to provide services.
