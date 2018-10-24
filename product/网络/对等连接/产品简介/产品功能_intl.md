## Non-transitive Connectivity of Peering Connections
Peering connection allows connectivity between VPCs, which is not transitive.
As shown in the following figure, peering connection is established between VPC 1 and VPC 2, as is done between VPC 1 and VPC 3. However, due to the non-transitive nature of peering connection, VPC 2 and VPC 3 cannot readily interconnect.
![](//mccdn.qcloud.com/static/img/9127397dcb1df231bfd8d32bcd628223/image.png)
>**Note:**
> Even if a peering connection is established, communication cannot be achieved if routes for sending and returning packets are not configured on both ends.

## Intra-region and Cross-region Peering Connections
VPC supports both intra-region and cross-region peering connections. Due to the differences in physical distance and underlying implementation architecture, there are some differences between the two types of connections, as shown in the following table:

| Comparison Item | Intra-region Peering Connection | Cross-region Peering Connection |
| ----- | ----------------------------------- | ---------------------------------------- |
| Underlying architecture | Local private network within a single region based on Tencent Cloud | Cross-region internal MPLS network based on Tencent Cloud |
| Bandwidth | Upper limit for connecting to public clouds: 5 Gbps<br/>Upper limit for connecting to BMs: 1 Gbps | Maximum 1 Gbps. The following configurations of upper bandwidth (in Mbps) are supported:<br/>10, 20, 50, 100, 200, 500 and1000 <br/>For peering connections between Beijing, Shanghai, Guangzhou, South Korea, and Hong Kong, you can [apply for more bandwidth](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC) <br/>If you need connectivity between mainland China and other regions, please consult your business manager. |
| Pricing | Free of charge | Billed on a daily basis according to the regions where both ends of the peering connection reside and the actual network bandwidth used. For more information, see [Price Overview](https://cloud.tencent.com/doc/product/215/%E4%BB%B7%E6%A0%BC%E6%80%BB%E8%A7%88) |
| Availability | Service level for intra-region connections is gold, with availability ≥ 99.50% guaranteed. | Linkage availability is divided as: <br/>Platinum: 99.95% <br/>Gold: 99.50% <br/>Silver: 99.00% <br/>Check your [SLA agreement](https://cloud.tencent.com/document/product/215/17800#2.1-.E6.9C.8D.E5.8A.A1.E5.8F.AF.E7.94.A8.E6.80.A7) |
| Cross-account connection | Supported | Supported |
| Access permission | CVMs on both ends of a peering connection can access all resources of each other including CVMs, databases, load balancers | CVMs on both ends of a peering connection can access all resources of each other including CVMs, databases, load balancers |
| Feature limits | VPC IP address ranges to which both ends of a peering connection belong must not overlap<br/>Peering connections are independent from one another | VPC IP address ranges to which both ends of a peering connection belong must not overlap<br/>**If multiple accepter VPCs are connected to the same VPC, the IP address ranges to which these accepter VPCs belong must not overlap** |
| Scenarios | Mainly used to connect applications in different VPCs within the same region | The typical application for cross-region peering connection is **cross-region disaster recovery**<br/>VPCs within different regions are connected by means of cross-region peering connection to rapidly deploy a 2-region-3-DC solution for disaster recovery, thus meeting the needs of financial-level network disaster recovery with high bandwidth and reliability. |

## Gateway Traffic Control for Peering Connections
Peering connection gateway traffic control provides the "monitoring" and "controlling" capabilities at the granularity of **IP-gateway**. Its refined visualization of gateway traffic enables network OPS personnel to get a clear picture of the traffic through the gateway. Its speed limiting at the granularity of IP-gateway helps block exceptional traffic.
- **Example:**
In the early morning of one day, the gateway traffic of a company surges. With intelligent gateway traffic control, the OPS personnel can trace data to find which IPs cause this traffic surge based on the time when the traffic surge occurs, so as to rapidly locate its source. In addition, the gateway traffic control provides bandwidth control at IP-gateway granularity, which can restrict the bandwidth from an IP to the gateway and block exceptional traffic to guarantee key businesses.
- **The advantages of gateway traffic control:**
 - Featured with the capability for accurate gateway troubleshooting, it can minimize the network failure time. It can also analyze the source IP and its key metrics by using the real-time traffic query and the TOP N ranking feature, to rapidly locate the exceptional traffic.
 With "monitoring" and "controlling" capabilities at IP-gateway granularity and by using the minute-level network traffic query, it can find the exceptional traffic that maliciously occupies the bandwidth in real time, and set bandwidth limits at IP-gateway granularity, so as to guarantee the stable operation of core businesses.
 It has full-time and full-traffic gateway traffic analysis capability, to help reduce cloud network cost. It controls the cost through QoS, thus restricting the bandwidth of non-key businesses to reduce cost in case of limited network budget.
