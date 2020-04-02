### How Can I Establish Communication Between Different Subnets of a VPC?
- Each VPC supports private network interconnection by default, and you can find the default route in the corresponding route table. This route indicates that all resources in this VPC can connect with each other through the private network.
- Subnets in different VPC instances cannot intercommunicate with each other through the private network. To enable intercommunication between subnets in different VPC instances, establish [peering connections](https://intl.cloud.tencent.com/document/product/553) or use [CCN](https://intl.cloud.tencent.com/document/product/1003).

### Can I Deploy CVMs in Different Availability Zones in the Same VPC?
Yes, you can. A VPC has a region attribute (whose value can be Guangzhou, Beijing, or Seoul), and subnets in the VPC have an availability zone attribute (whose value can be Guangzhou Zone 1 or Guangzhou Zone 2). With both attributes, subnets in the same VPC can be deployed in different availability zones in the same region. The availability zone attribute of a CVM inherits that of the belonging subnet, and CVMs are purchased under subnets in availability zones. Therefore, CVMs can be deployed in different availability zones.

### How Can I Establish Communication Between CVMs and Databases in Different Availability Zones?
- In the Same VPC: CVMs and databases in the same VPC can interconnect with each other by default. If the interconnection fails, you can first troubleshoot the firewall policies of the [network ACL](https://intl.cloud.tencent.com/document/product/215/31850).
- In Different VPC Instances: CVMs and databases are isolated by default. If interconnection is required, you can establish private network interconnection between VPC instances by using [peering connections](https://intl.cloud.tencent.com/document/product/553) or [CCN](https://intl.cloud.tencent.com/document/product/1003).


