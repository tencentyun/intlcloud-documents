### How Do CVMs or Databases Interconnect through the Private Network?
The private network communication of CVMs or databases in a VPC is actually the communication of private IP addresses at the network level, and therefore there is no difference between them. The communication methods under different private IP address scenarios are as follows:

| Communication Scenario | Communication Method |
|---------------|------------|
| Different regions | CVMs or databases in different regions belong to different VPC instances and communicate with each other through [peering connections](https://intl.cloud.tencent.com/document/product/553/18836) or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Both same-account and cross-account communication are supported.) |
| Different availability zones | Same VPC: support interconnection by default.<br>Different VPC instances: communicate through [peering connections](https://intl.cloud.tencent.com/document/product/553/18836) or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Both same-account and cross-account communication are supported.) |
| Different VPC instances | Communicate through [peering connections](https://intl.cloud.tencent.com/document/product/553/18836) or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Both same-account and cross-account communication are supported.) |
| Different subnets | Same VPC: support interconnection by default.<br>Different VPCs: communicate through [peering connections](https://intl.cloud.tencent.com/document/product/553/18836) or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Both same-account and cross-account communication are supported.) |
| Cross-account | Cross-account communication through [peering connections](https://intl.cloud.tencent.com/document/product/553/18836) or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Both same-region and cross-region communication are supported.) |
 
>!
>- For the cross-account VPC interconnection through peering connection or CCN, take note of  the following: 
    - The root account owns resources. If you want to communicate with another account through peering connection or CCN, enter the root account. 
    - The sub-account only has the operation permission by default. Apply for permission from the root account to establish the peering connection or CCN if needed.
>- **Private network default interconnection** is present between different subnets of the same VPC (whether or not they are in the same availability zone). If they cannot connect with each other, you can first troubleshoot the firewall policies of the [security group](https://intl.cloud.tencent.com/document/product/213/12452) and the [network ACL](https://intl.cloud.tencent.com/document/product/215/5132).


### What Should I Do When a Peering Connection Fails to Be Established Due to a VPC IP Range Conflict?
When you try to establish a peering connection, the CIDR blocks of the two VPC instances cannot overlap, otherwise the peering connection cannot be established.

- If the IP ranges of both VPC instances that need to intercommunicate overlap but the subnet IP ranges do not overlap, then you can try to establish communication through [CCN](https://intl.cloud.tencent.com/product/ccn). CCN can lower IP address range limits to the subnet level when VPC instances communicate with each other.
For example, the IP ranges of both VPC instances that need to communicate with each other are both `10.0.0.0/16`, but the subnets are `10.0.1.0/24` and `10.0.2.0/24` respectively. In this case, you can establish communication through CCN. For more information, see [CCN](https://intl.cloud.tencent.com/document/product/1003).
- If your needs cannot be met by using CCN, you need to migrate the resources inside the overlapping subnets.
    - For details on changing the subnets of CVMs, see [Changing the Subnets of Instances](https://intl.cloud.tencent.com/document/product/213/16565).
    - For details on inter-VPC migration, see [Switching VPC Instances](https://intl.cloud.tencent.com/document/product/213/20278).

### If VPC1 Separately Establishes Peering Connections With VPC2 and VPC3, Then Can VPC2 and VPC3 Communicate with Each Other?
No, they cannot. Two VPC instances can establish interconnection through a peering connection, but this interconnection relationship is not transitive. This means that when a peering connection is established between VPC1 and VPC2 while another peering connection is established between VPC1 and VPC3, traffic interconnection is unavailable between VPC2 and VPC3 because the peering connection is not transitive.

