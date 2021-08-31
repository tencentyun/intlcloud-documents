### What is a NAT Gateway?
A [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) can translate the private IP address in a Virtual Private Cloud (VPC) to a public IP address if the private and public networks are isolated from each other, enabling the VPC to access the Internet. The NAT Gateway supports a maximum of 5 Gbps traffic surge and 10,000,000 concurrent connections. As a highly available gateway, the NAT Gateway also provides master/slave hot backup. When one server fails, its automatic switchover helps ensure your businesses intact. As a gateway with the ability to translate private IP addresses in a VPC to public IP addresses, the NAT Gateway provides a way for cloud resources that reside in a VPC without a public IP address to access the Internet. For more information about the typical use cases of the NAT Gateway, see [Use Cases](https://intl.cloud.tencent.com/document/product/1015/30228).

### What are the differences between NAT Gateways and public gateways?
Both are used for CVMs in a VPC to access the Internet, but there are some differences. For more information, see the “Differences Between the NAT Gateway and the Public Gateway” section in [Overview](https://intl.cloud.tencent.com/document/product/1015/30226).

### What types of configuration do NAT Gateways provide?
Each NAT Gateway can bind up to 10 EIPs, and provides three configuration types. For more information, see the “Configuration Specifications” section in [Product Specifications](https://intl.cloud.tencent.com/document/product/1015/30229).

### What are the key features of NAT Gateways?
NAT Gateways highlight features including SNAT, DNAT, high performance, high availability, monitoring details display, and refined gateway traffic control. For more information, see [Features](https://intl.cloud.tencent.com/document/product/1015/30227).

### What are the constraints of NAT Gateways?
Notice the constraints when you are using the NAT Gateway. For example, if you delete a NAT Gateway, its EIP will be disassociated, but not released from the account. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/1015/30230).

### What is the network topology of NAT Gateways?
When resources like CVMs in a VPC send out data packets through the NAT Gateway, the data will first travel through the router and select a route based on the routing policies. For more information, see the “Network Topology” section in [Overview](https://intl.cloud.tencent.com/document/product/1015/30226).

### What are the key features of NAT Gateways?
- SNAT and DNAT are supported.
- The Anti-DDoS service is supported.
For more information, see [Features](https://intl.cloud.tencent.com/document/product/1015/30227).

### What is an EIP?
An EIP is a static IP address designed for dynamic cloud computing, and is a fixed public IP address in a region. You can use EIP to quickly remap an address to another NAT Gateway under your account to shield instance failures. For more information, see [Elastic Public IP (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).


### What can the NAT Gateway bandwidth limit do?
- Role: NAT Gateway bandwidth limit provides **monitoring** and **control** capabilities at **IP-gateway** granularity. The visualization helps network OPS personnel get a clear picture of the gateway traffic. The speed limiting capability at IP-gateway granularity helps block unhealthy traffic. The gateway bandwidth limit has the following advantages:
 - It can accurately troubleshoot gateway exceptions to minimize network downtime. Using real-time traffic query and Top-N ranking features, it can analyze the source IP and its key metrics to quickly locate unhealthy traffic.
 - With **monitoring** and **control** capabilities at IP-gateway granularity as well as minute-level network traffic queries, it can efficiently identify unhealthy traffic that consumes the bandwidth. The bandwidth limit at IP-gateway granularity ensures the stable operation of key businesses.
 - With gateway traffic analysis capability for all traffic at all times, it helps minimize network costs. By means of QoS, it can limit the bandwidth of non-key businesses to reduce costs.
- For example, the gateway traffic of an enterprise surges on one morning. With intelligent gateway bandwidth limit, the OPS personnel can trace the IP that caused this surge based on a point in time. The gateway bandwidth limit features IP-gateway granularity to control the bandwidth from an IP to the gateway, blocking unhealthy traffic to protect key businesses.

### What is a region?
Different regions of Tencent Cloud are completely isolated to ensure maximal stability and fault tolerance across regions. The South China, East China, and North China nodes cover China Mainland. The Hong Kong (China) and Singapore nodes for South East Asia, the Toronto node for the North America, and the Silicon Valley node for the Western U.S, are also available. In the future, we will make more nodes available and cover more regions. We recommend you select a region closest to your customer to reduce access latency and increase access speed.

### How do I select the most Suitable region?
Select a region under the principles below:
- Close to your users.
Select the CVM region based on the user's geographical location. The closer the CVM is to your users who will access it, the shorter the access latency and the higher the access speed will be.
- In the same region.
CVMs are interconnected in the same region over a private network, but cannot communicate with each other across regions. To enable interconnection among multiple CVMs over a private network, you need to reside them in the same region. The intra-region interconnection over a private network is free of charge, while the cross-region communication is only available over a public network at a cost.
How are availability zones isolated from each other?
Each availability zone operates in its own separate, physically distinct infrastructure and has been designed to feature high reliability. Common points of failure like generators and cooling devices are not shared between availability zones. In addition, availability zones are physically independent of one another, so even in the case of rare disasters such as fires, tornadoes, or floods, only a single availability zone will be affected.

### How many NAT Gateways can I create?
It depends on the use limits of resources. To increase the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC).

