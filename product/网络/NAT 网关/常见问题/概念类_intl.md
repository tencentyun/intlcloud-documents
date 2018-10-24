### What is the NAT gateway?

The [NAT gateway](/document/product/215/4975) can translate private and public IP addresses within a VPC when the private and public networks are isolated, allowing the VPC to access the Internet, and supports a maximum of 5 Gbps traffic surge and 10,000,000 concurrent connections. As a highly available gateway, the NAT gateway also provides master/slave hot backup, allowing automatic switching when a single server suffers a failure without affecting your use of the services. A gateway with the ability to translate private and public IP addresses within a VPC, the NAT gateway provides a way for cloud resources that exist in a VPC without a public IP to access the Internet. (Active access from the Internet to a VPC not supported.) For more information on typical application scenarios, see [Introduction to NAT Gateways](https://cloud.tencent.com/document/product/215/4975?&_ga=1.98784094.1391268748.1532045932#.E7.AE.80.E4.BB.8B).

### What is the difference between the NAT gateway and public gateway?

Both the NAT gateway and public gateway are used for CVMs in the VPC to access the Internet, but some differences exist. For more information, see [Difference Between the NAT Gateway and Public Gateway](https://cloud.tencent.com/document/product/215/4975#nat.E7.BD.91.E5.85.B3.E5.92.8C.E5.85.AC.E7.BD.91.E7.BD.91.E5.85.B3.E7.9A.84.E5.8C.BA.E5.88.AB).

### What types of configuration does the NAT gateway provide?

The NAT gateway supports binding up to 10 EIPs, while providing three configuration types. For more information, see [Configuration Types of NAT Gateway](https://cloud.tencent.com/document/product/215/4975?&_ga=1.98784094.1391268748.1532045932#.E9.85.8D.E7.BD.AE.E7.B1.BB.E5.9E.8B).

### What are the key features of the NAT gateway?

The NAT gateway features SNAT, DNAT, high performance, high availability, monitoring details display, and refined gateway traffic control. For more information, see [Key Features of the NAT Gateway](https://cloud.tencent.com/document/product/215/4975?&_ga=1.98784094.1391268748.1532045932#.E5.85.B3.E9.94.AE.E7.89.B9.E6.80.A7).

### What are the constraints of the NAT gateway?

There are constraints on the use of the NAT gateway. If an NAT gateway is deleted, its EIP is disassociated from it, but not released from the account. For more information, see [Usage Constraints of the NAT Gateway](https://cloud.tencent.com/document/product/215/4975?&_ga=1.98784094.1391268748.1532045932#.E4.BD.BF.E7.94.A8.E7.BA.A6.E6.9D.9F).

### What is the network topology of the NAT gateway?

When resources like CVMs within the VPC send outgoing data packets via the NAT gateway, the data will first move through the router and make the routing selection based on the routing policies. For more information, see [Network Topology of the NAT Gateway](https://cloud.tencent.com/document/product/215/4975?&_ga=1.98784094.1391268748.1532045932#.E7.BD.91.E7.BB.9C.E6.8B.93.E6.89.91.E5.85.B3.E7.B3.BB).

### What are the main features of the NAT gateway?

- SNAT and DNAT are supported.
- The high defense service is supported.
  For more information, see [Main Features of the NAT Gateway](https://cloud.tencent.com/document/product/215/4975?&_ga=1.98784094.1391268748.1532045932#.E4.B8.BB.E8.A6.81.E5.8A.9F.E8.83.BD).

### What is the EIP?

The EIP is a static IP designed for dynamic cloud computing, and is a fixed public IP in a certain region. With EIPs, you can quickly remap an address to another NAT gateway in your account to block instance failures. For more information, see [Elastic Public IP (EIP)](/document/product/213/5733).

### What is NAT gateway traffic control?

- NAT gateway traffic control provides "monitoring" and "controlling" capabilities at IP-gateway granularity. The refined gateway traffic visualization enables network OPS personnel to get a clear picture of the traffic in the gateway. In addition, the speed restricting capability at IP-gateway granularity helps block exceptional traffic. The advantages of gateway traffic control are as follows:
  - Featured with the capability for accurate gateway troubleshooting, it can minimize the network failure time. It can also analyze the source IP and its key metrics by using the real-time traffic query and the TOP N ranking feature, to rapidly locate the exceptional traffic.
  - With "monitoring" and "controlling" capabilities at IP-gateway granularity and by using minute-level network traffic query, it can identify exceptional traffic that maliciously occupies the bandwidth in real time, and set bandwidth limits at IP-gateway granularity to guarantee the stable operation of core businesses.
  - It has full-time and full-traffic gateway traffic analysis capability, to help reduce cloud networking costs. By means of QoS, it can restrict the bandwidth of non-key businesses to minimize cost with limited network budget.
- For example, in the wee hours one morning, the gateway traffic of a company surges. With intelligent gateway traffic control, the OPS personnel can trace data to determine which IPs caused this traffic surge based on the time when the traffic surge occurred, so as to rapidly locate its source. In addition, the gateway traffic control provides bandwidth control at IP-gateway granularity, which can restrict the bandwidth from an IP to the gateway and block exceptional traffic to guarantee key businesses.

### How can I select the most suitable region?

Region selection abides by the following principles:

- Near the user's region
  The region of a CVM should be selected based on the user's geographical location. The closer the CVM is to your users who access it, the shorter the access latency and the higher the access speed will be. For example, if most of your users are located near the Yangtze River Delta, Shanghai would be a good choice.
- Communicate via the private network in the same region
  CVMs in the same region are interconnected with each other via the private network, but those in different regions cannot communicate with each other via the private network. Users who communicate with each other using multiple CVMs via private network need to choose the same region. CVMs in the same region can communicate with each other via the private network free of charge. CVMs in different regions cannot communicate with each other via the private network, and can only communicate via the public network, where charges apply.
  What is the degree of isolation among availability zones?
  Each availability zone operates in its own separate, physically distinct infrastructure and has been designed to feature high reliability. Common points of failure like generators and cooling equipment are not shared among availability zones. In addition, they are physically independent of one another, so even in the case of rare disasters such as fires, tornadoes, or floods, only a single availability zone will be affected.

### How many NAT gateways can be created?

It depends on the limitations of specific resources. For more information, see [Detailed Resource Quota in the VPC](/document/product/215/537). [Submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC) . to apply for a higher quota if needed.
