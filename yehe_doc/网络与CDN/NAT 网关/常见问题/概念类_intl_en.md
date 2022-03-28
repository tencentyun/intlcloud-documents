### What is a NAT Gateway?
A [NAT gateway](https://intl.cloud.tencent.com/document/product/1015) can translate the private IP address in a Virtual Private Cloud (VPC) to a public IP address if the private and public networks are isolated from each other, enabling the VPC to access the Internet. The NAT gateway supports a maximum of 5 G bps traffic surge and 10,000,000 concurrent connections. As a highly available gateway, the NAT gateway also provides master/slave hot backup, enabling automatic switching in the event of a single point of failure with an imperceptible impact on your use of the services. As a gateway with the ability to translate private and public IP addresses within a VPC, the NAT gateway provides a way for cloud resources that reside in a VPC without a public IP address to access the Internet. For more information about the typical application scenarios of the gateway, please see [NAT Gateway-Application Scenarios](https://intl.cloud.tencent.com/document/product/1015/30228).

### What are the differences between NAT gateways and public gateways?
Both NAT gateways and public gateways are used by CVMs within the VPC to access the Internet. However, there are some differences between them. For more information, please see [Differences Between NAT Gateways and Public Gateways](https://intl.cloud.tencent.com/document/product/1015/30226).

### What types of configuration do NAT gateways provide?
NAT gateways support the binding of up to 10 EIPs, and provide three configuration types. For more information, please see [Configuration Types of NAT Gateways](https://intl.cloud.tencent.com/document/product/1015/30229).

### What are the key features of NAT gateways?
NAT gateways feature SNAT, DNAT, high performance, high availability, monitoring details display, and refined gateway traffic control. For more information, please see [Features of NAT Gateways](https://intl.cloud.tencent.com/document/product/1015/30227).

### What are the constraints on the use of NAT gateways?
There are constraints on the use of NAT gateways. If a NAT gateway is deleted, its EIP is disassociated from it, but not released from the account. For more information, please see [Use Limits of NAT Gateways](https://intl.cloud.tencent.com/document/product/1015/30230).

### What is the network topology of NAT gateways?
When resources like CVMs within the VPC send outbound data packets through the NAT gateway, the data will first travel through the router and select a route based on the routing policies. For more information, please see [Network Topology of NAT Gateways](https://intl.cloud.tencent.com/document/product/1015/30226).

### What are the main features of NAT gateways?
- SNAT and DNAT are supported.
- The Anti-DDoS service is supported.
For more information, please see [Features of NAT Gateways](https://intl.cloud.tencent.com/document/product/1015/30227).

### What is an EIP?
An EIP is a static IP address designed for dynamic cloud computing, and is a static public IP address in certain regions. By using EIPs, you can quickly remap an address to another NAT gateway in your account to fail over instance failures. For more information, please see [Elastic Public IP (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).


### What can NAT Gateway Traffic Control do?
- NAT Gateway Traffic Control provides the **monitoring** and **controlling** capabilities at IP-gateway granularity. The refined gateway traffic visualization enables network OPS personnel to get a clear picture of the traffic in the gateway. In addition, the speed limiting capability at IP-gateway granularity helps to block abnormal traffic. The advantages of gateway traffic control are as follows:
 - It can accurately troubleshoot gateway exceptions to minimize network downtime. Using real-time traffic query and Top-N ranking features, it can analyze the source IP and its key metrics to quickly locate unhealthy traffic.
 - With the **monitoring** and **control** capabilities at IP-gateway granularity and by using minute-level network traffic query, it can identify abnormal traffic that maliciously consumes the bandwidth in real time, and set bandwidth limits at IP-gateway granularity to ensure the stable operation of core businesses.
 - With gateway traffic analysis capability for all traffic at all times, it helps minimize network costs. By means of QoS, it can limit the bandwidth of non-key businesses to reduce costs.
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
Each VPC support 3 NAT gateways. For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/1015/30230). If you require a higher quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


