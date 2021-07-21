Classiclink or terminal connection are two methods for interconnecting VPC resources and classic network resources.

## Classiclink
### Operation scenario
By default, a VPC is a fully isolated network space that cannot interconnect with other VPC instances or the classic network through a private network. [Peering connections](https://intl.cloud.tencent.com/document/product/553) enable different VPC instances to communicate with each other, and Classiclink enables VPC instances to communicate with the classic network.

As shown in the following figure, classic network CVMs can access cloud resources in a VPC, such as CVMs, cloud databases, private network CLBs, and cloud caches. However, the CVMs in the VPC can only access the classic network CVMs that are interconnected with it but not other computing resources within the classic network.
![] (https://main.qcloudimg.com/raw/ee81676f03ae38e10d71c934b9300070.png)
>Classiclink is available only for intra-region interconnection.

### Basic configuration impacts
- The private IP addresses of associated classic network CVMs will be automatically added to the local policy of the VPC's route table. In this way, CVMs in the VPC and CVMs in this classic network can communicate with each other, without needing to manually modify the route table policy in the current VPC. 
- After the classic network CVM is associated with the VPC, its security firewalls and network ACLs remain effective.
You can configure the network ACL for the VPC subnet to restrict the access from the associated classic network CVM. You can also configure security group rules for CVMs in the classic network and VPC to restrict network access attempts in both directions.

### Use limits
#### Restrictions
- Only interconnection between VPC instances and the classic network **in the same region** is supported.
- The Classiclink feature is available only for VPC instances within the network segment of `10.[0-47].0.0/16`. The IP range for VPC instances in other network segments may conflict with the classic network IP segment.
- A classic network CVM can be associated with one VPC at a time.
- A VPC can be associated with a maximum of 100 classic network CVMs.
- VPC resources can only access CVMs in the classic network rather than other resources in the classic network, such as cloud databases and CLBs.

#### Notes
- The CLB instance within a VPC cannot be bound to a classic network CVM interconnected with the same VPC.
- Changing the private IP address of a classic network CVM cancels the association with the VPC, which means the original association record will become invalid. Add the record again in VPC Console if you want to associate them again.
- The interconnection relationship with the VPC will not be unbound by actions taken regarding the CVM, such as isolation due to overdue payment, security isolation, cold migration, failover, configuration modification, and operating system switching.
- The interconnection relationship with the VPC will be automatically unbound if the CVM is returned.
- In Classiclink situations, the CVM traffic can only be routed to private IP addresses within the VPC, but not to destinations outside the VPC. That is, the classic network CVM cannot access the Internet or VPC resources outside the current VPC through network devices such as its VPN gateway, direct connect gateway, public gateway, peering connection, and NAT gateway. Likewise, the peer of a VPN gateway, direct connect gateway, and peering connection cannot access the classic network CVM.

### Steps
For information on how to operate Classiclink, see [Managing the Classic Network](https://intl.cloud.tencent.com/document/product/215/31807).

## Terminal Connections
Terminal connection is another method to connect VPC instances and the classic network. It connects instances in a VPC and non-CVM instances in the classic network through a private network. Classic network products that support terminal connections include CLB, MySQL, Memcached, Redis, and MongoDB.

A terminal connection establishes mapping between classic network instance IP addresses and VPC IP addresses so that classic network instances can be accessed by accessing VPC IP addresses.

>Cross-region or inter-account terminal connections are not supported. If you do need to establish a terminal connection in these situations, submit a [ticket to apply for it](https://console.cloud.tencent.com/workorder/category).


