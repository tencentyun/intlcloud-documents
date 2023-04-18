Tencent Cloud direct connect maximizes the high availability of business in various failure scenarios, such as port exception/fiber optic component failure, network device failure, failure of data center at the access point etc. It provides [four-line dual access point (recommended)](https://intl.cloud.tencent.com/document/product/216/38527), [two-line dual access point](https://intl.cloud.tencent.com/document/product/216/38527), [two-line single access point](https://intl.cloud.tencent.com/document/product/216/38527) and other network architectures, where, the four-line dual access point network architecture provides higher level of [Tencent Cloud Direct Connect Service Level Agreement](https://intl.cloud.tencent.com/document/product/216/39619). In this document, we take four-line dual access point architecture as an example to describe the high availability design and practices of Tencent Cloud direction connect.

## Network Architecture with High Availability
![]()
- User IDC accesses at least two Tencent Cloud direct connect access points through connections to achieve high availability and load balancing at the physical level.
- Direct connect gateway integrates with DSR clusters based on DSR system design. It acts as the bridge between Tencent Cloud and IDC to form a virtual dedicated tunnel together with the local router at IDC side and achieve resources intercommunication via Tencent Cloud VPC or CCN.
- DSR clusters provide two Tencent Cloud border IP addresses to implement active-active routing system at the control plane. Thus, the local router on IDC side has created BGP neighbor adjacency with the two clusters respectively via BGP protocol to effectively ensure high availability of business in case of DSR cluster upgrade or single cluster failure and avoid impact on business caused by single BGP neighbor adjacency interruption and route convergence.
- Meanwhile, DSR adjusts and removes exceptional service nodes dynamically through real-time monitoring mechanism in the cluster to ensure the availability of single cluster. It adopts large-scale cluster scaling technique to enable horizontal scaling among multiple clusters for the business to ensure availability across clusters.

### Hot switching in case of failure

#### Switching in case of connection failure
The system switches the traffic to connection 2 automatically when it detects a failure in connection 1 to ensure normal operation of the business. The traffic will be switched back automatically when the failure is recovered.
![]()

#### Switching in case of exchange failure
The system switches the traffic to connection 2 automatically when it detects a failure in exchange 1 to ensure normal operation of the business. The traffic will be switched back automatically when the failure is recovered.
![]()

#### Switching in case of DSR failure
The system switches the traffic to connection 2 automatically when it detects a failure in the DSR cluster to ensure normal operation of the business. The traffic will be switched back automatically when the failure is recovered.
![]()

#### Switching in case of access point failure
The system switches the traffic to access point 2 automatically when it detects a failure in access point 1 to ensure normal operation of the business. The traffic will be switched back automatically when the failure is recovered.
![]()

#### Switching in case of over capacity
According to [capacity planning](https://intl.cloud.tencent.com/document/product/216/38527), the usage of each connection is not allowed to be over 50%. If the usage of connection 1 is over 50%, the system will switch traffic to connection 2 automatically. Then, the traffic will be switched back to connection 1 when the usage is below 50%.
![]()


## Limits and Suggestions for Practices

### Network layer (dedicated tunnel)
- BGP IP needs to be configured on both Tencent Cloud side and the user IDC side to establish a session, and BGP session must be kept in active-active status.
  See the figure below for the configuration on Tencent Cloud side. For more information, see [Exclusive Virtual Interface-Advanced Configuration](https://www.tencentcloud.com/document/product/216/48574).
![]()
- BFD and NQA needs to be provided for health check to ensure robustness of the tunnel. For more information on the configuration of health check, see [Health Check for the Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/46292).

### Physical layer (connection)
On the IDC side, users can use the same port of an edge device to connect primary/secondary connections to ensure high availability of the connections, or use two edge devices to connect primary/secondary connections.
