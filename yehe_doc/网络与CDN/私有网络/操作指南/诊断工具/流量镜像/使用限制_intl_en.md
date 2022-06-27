Assess the following limits before using a traffic mirror, so that your businesses will not be affected.
- The traffic mirror feature is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. Save the link to the Traffic Mirror console for later logins; otherwise, you may need to apply again.
- Using the traffic mirror feature will consume the CPU, memory, bandwidth, and other resources of the server.
Mirrored traffic will be included in the instance bandwidth, and the impact on system resources depends on your traffic volume and type. For example, if a network interface has 1 Gbps inbound traffic and 1 Gbps outbound traffic and uses the traffic mirror feature, its application system will need to handle 1 Gbps inbound traffic and 3 Gbps outbound traffic (including 1 Gbps outbound traffic, 1 Gbps mirrored inbound traffic, and 1 Gbps mirrored outbound traffic).
- Flow logs cannot be used to capture traffic mirror data.
- Security group limits:
  - Collection source: Mirrored traffic is not subject to security group policies.
  - Receiver: It is subject to security group policies.
- Traffic mirror cannot be used for the following data services:
 - ARP
 - DHCP
 - Instance metadata service
 - NTP
 - Windows activation
- The collection source and the receiver of a traffic mirror support the following models:
Standard S1, Standard S2, Standard S3, Memory Optimized M1, M2, and M3, High IO I1, I2, and I3, Compute C2 and C3, Compute Enhanced CN3, and Big Data D1.
- CVM ENIs are subject to the following limits:
  - When a traffic mirror is set, the upper ENI bandwidth limit of the target CVM instance must be at least 1/9 of the total ENI bandwidth of all CVM instances in the collection scope.
For example, if there are six S3.6XLARGE48 instances in the collection scope of a traffic mirror, and the total ENI bandwidth is 3 Gbps * 6 = 18 Gbps, then the inbound bandwidth at the receiver must be at least 2 Gbps (18/9 = 2), that is, at least two S3.MEDIUM8 instances or one S3.4XLARGE32 instance.
  - To avoid the situation where the mirrored traffic exceeds the capacity of the receiving ENI, increase the number of receivers and CVM instance specifications to cater to the business traffic volume. For more information on CVM instance specifications, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).


