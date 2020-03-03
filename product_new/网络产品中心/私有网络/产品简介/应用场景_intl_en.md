## Accessing the Internet
### Single CVM
When the traffic to your business is low and only one CVM is available, you can apply for a public IP address and bind it with the CVM to gain access to the Internet.
![](https://main.qcloudimg.com/raw/fb98506f00fb522bd6d120e6ccf9b957.png)

### Multiple CVMs
When you have multiple CVMs that need to access the Internet simultaneously and you do not want the private network addresses of the CVMs to be exposed, you can use [NAT Gateway](https://cloud.tencent.com/document/product/552). The NAT gateway provides the SNAT feature and allows multiple CVMs to access the Internet with public IP addresses on the NAT gateway. Moreover, without the configuration of the DNAT feature, external users cannot directly access the NAT gateway, ensuring security. When multiple public IP addresses exist on the NAT gateway, the NAT gateway automatically performs load balancing.
![](https://main.qcloudimg.com/raw/9abb0e48ea6c36b07d53b6a02e703918.png)

## Providing Services to the Internet
### Single CVM
You can host services (such as website services) on a VPC-based CVM and use a public IP address to provide services to external users.
![](https://main.qcloudimg.com/raw/fb98506f00fb522bd6d120e6ccf9b957.png)

### Mutiple CVMs
When you have many CVMs for deploying complex services and the Internet traffic is high, you can use the [Cloud Load Balancer (CLB)](https://cloud.tencent.com/document/product/214). The CLB can automatically distribute application access traffic among CVM instances in the cloud, enhancing fault tolerance for applications.
![](https://main.qcloudimg.com/raw/1acf28ecd51df472da98e5ad6c270e8f.png)

## Disaster Recovery for Applications
### Cross-Availability Zone Disaster Recovery
A subnet is associated with a availability zone. You can create subnets in different availability zones of one VPC in a region. By default, different subnets of the same VPC interconnect through the private network. You can deploy resources in subnets of different availability zones to achieve cross-availability zone disaster recovery.
![](https://main.qcloudimg.com/raw/b12f674709f77926154f8ccee6c636e8.png)

### Cross-Region Disaster Recovery
You can deploy businesses across regions (for example, the 2-region-3-DC solution) to achieve cross-region disaster recovery.
![](https://main.qcloudimg.com/raw/690af219dc4f4f3cfe6cef54259789ac.png)

## Deploying a Hybrid Cloud
### Connecting to Local IDCs
VPC provides multiple connection modes, such as direct connect and VPN connection, which can connect your local IDCs with VPC instances in the cloud to easily create a hybrid cloud architecture. Using local IDCs ensures the security of your core data. You can expand resources (such as CVMs and TencentDB) in the cloud based on your business volume to reduce IT Ops costs.
![](https://main.qcloudimg.com/raw/013d4f4b17c0996f70f2f73a99ba687c.png)

### Global Multi-Point Interconnection
When you have businesses deployed in multiple regions around the world and interconnection among regions is needed, you can use products or features such as [CCN](https://cloud.tencent.com/document/product/877) and [Direct Connect](https://cloud.tencent.com/document/product/216) to enable global multi-point interconnection through single-point access.
![](https://main.qcloudimg.com/raw/0f40ad294f674a9befb85aaa73bf5720.png)
