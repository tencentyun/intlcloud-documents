### What is a NAT Gateway?
A [NAT gateway](https://cloud.tencent.com/document/product/215/4975) can translate the private IP address in a Virtual Private Cloud (VPC) to a public IP address if the private and public networks are isolated from each other, enabling the VPC to access the Internet. The NAT gateway supports a maximum of 5 Gbps traffic surge and 10,000,000 concurrent connections. As a highly available gateway, the NAT gateway also provides master/slave hot backup, enabling automatic switching in the event of a single point of failure with an imperceptible impact on your use of the services. As a gateway with the ability to translate private and public IP addresses within a VPC, the NAT gateway provides a way for cloud resources that reside in a VPC without a public IP address to access the Internet (active access from the Internet to a VPC is not supported). For more information about the typical application scenarios of the gateway, see [Introduction to the NAT Gateway](https://cloud.tencent.com/document/product/215/4975?&_ga=1.98784094.1391268748.1532045932#.E7.AE.80.E4.BB.8B).

### What are the differences between NAT gateways and Public gateways?
Both NAT gateways and public gateways are used for CVMs in the VPC to access the Internet. For more information, see [Differences Between NAT Gateways and Public Gateways](https://cloud.tencent.com/document/product/552/12951#.E4.B8.8E.E5.85.AC.E7.BD.91.E7.BD.91.E5.85.B3.E7.9A.84.E5.8C.BA.E5.88.AB).

### What types of configuration do NAT gateways provide?
NAT gateways support the binding of up to 10 EIPs, and provide three configuration types. For more information, see [Configuration Types of NAT Gateways](https://cloud.tencent.com/document/product/552/12954#.E9.85.8D.E7.BD.AE.E7.B1.BB.E5.9E.8B).

### What are the key features of NAT gateways?
NAT gateways feature SNAT, DNAT, high performance, high availability, monitoring details display, and refined gateway traffic control. For more information, see [Key Features of NAT Gateways](https://cloud.tencent.com/document/product/552/12952).

### What are the constraints of NAT gateways?
There are constraints on the use of NAT gateways. If a NAT gateway is deleted, its EIP is disassociated from it, but not released from the account. For more information, see [Use Limits of NAT Gateways](https://cloud.tencent.com/document/product/552/12955).

### What is the network topology of NAT gateways?
When resources like CVMs within the VPC send outbound data packets through the NAT gateway, the data will first travel through the router and select a route based on the routing policies. For more information, see [Network Topology of NAT Gateways](https://cloud.tencent.com/document/product/552/12951#.E7.BD.91.E7.BB.9C.E6.8B.93.E6.89.91.E5.85.B3.E7.B3.BB).

### What are the main features of NAT gateways?
- SNAT and DNAT are supported.
- The Anti-DDoS service is supported.
For more information, see [Key Features of NAT Gateways](https://cloud.tencent.com/document/product/552/12952).

### What is an EIP?
An EIP is a static IP address designed for dynamic cloud computing, and is a static public IP address in certain regions. By using EIPs, you can quickly remap an address to another NAT gateway in your account to fail over instance failures. For more information, see [Elastic Public IP (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).


### What can Gateway Traffic Monitoring and Control do?
- NAT Gateway Traffic Monitoring and Control provides the **monitoring** and **controlling** capabilities at IP-gateway granularity. The refined gateway traffic visualization enables network OPS personnel to get a clear picture of the traffic in the gateway. In addition, the speed limiting capability at IP-gateway granularity helps to block abnormal traffic. The advantages of gateway traffic control are as follows:
 - With the capability for accurate gateway troubleshooting, it can minimize network downtime. It can also analyze the source IP address and its key metrics by using the real-time traffic query and the TOP N ranking feature, to rapidly locate abnormal traffic.
 - With the **monitoring** and **control** capabilities at IP-gateway granularity and by using minute-level network traffic query, it can identify abnormal traffic that maliciously consumes the bandwidth in real time, and set bandwidth limits at IP-gateway granularity to ensure the stable operation of core businesses.
 - It has a full-time and full-traffic gateway traffic analysis capability, to help minimize cloud network costs. By means of QoS, it can limit the bandwidth of non-key businesses to minimize costs for limited network budgets.
- For example, in an early morning, the gateway traffic of an enterprise surges. With intelligent gateway traffic control, the OPS personnel can trace data to find which IP addresses caused this traffic surge according to the time when the traffic surge occurred, so as to rapidly locate its source. In addition, the gateway traffic control feature provides bandwidth control at IP-gateway granularity, which can restrict the bandwidth from an IP address to the gateway and block abnormal traffic to safeguard key businesses.

### What is a region?
Different regions of Tencent Cloud are completely isolated to ensure maximal stability and fault tolerance between regions. The South China, East China, and North China nodes cover China mainland. The Hong Kong (China) and Singapore nodes, which cover South East Asia, the Toronto node which covers North America, and the Silicon Valley node for the Western U.S, are also available. In the future, we will provide more available nodes to cover more regions. We recommend that you choose the region closest to your customers to minimize access latency and improve download speeds.

### How do I select the most Suitable region?
Region selection abides by the following principles:
- Be close to your users.
The region of a CVM should be selected based on the user's geographical location. The closer the CVM is to your users who will access it, the shorter the access latency and the higher the access speed will be. 
- In the same region.
CVMs in the same region are interconnected with each other via the private network, but those in different regions cannot communicate with each other via the private network. Users who communicate with each other using multiple CVMs via a private network should choose the same region. CVMs in the same region can communicate with each other via a private network free of charge. CVMs in different regions cannot communicate with each other via a private network but only via a public network with a charge.
How are availability zones isolated from each other?
Each availability zone operates in its own separate, physically distinct infrastructure and has been designed to feature high reliability. Common points of failure like generators and cooling devices are not shared between availability zones. In addition, availability zones are physically independent of one another, so even in the case of rare disasters such as fires, tornadoes, or floods, only a single availability zone will be affected.

### How many NAT gateways can I create?
It depends on the limitations of specific resources. For more information, see [Detailed Resource Quota for a VPC](https://cloud.tencent.com/document/product/215/537). [Submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC) to apply for a higher quota if needed.

