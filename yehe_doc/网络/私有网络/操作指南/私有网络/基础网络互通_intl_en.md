The Classiclink feature allows VPC-based CVMs to communicate with classic network-based CVMs. This document mainly describes how to create and manage Classiclink.

## Background
Both classic network and VPC are network spaces on the cloud. The classic network is a public network resource pool for all Tencent Cloud users (as shown on the right side of the figure below). The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses. By contrast, the VPC is a logically isolated network space in Tencent Cloud (as shown on the left side of the figure below). In a VPC, you can customize IP ranges, IP addresses, and routing policies.
VPC is more suitable for use cases requiring custom configurations.
>?
>+ As the classic network resources become increasingly scarce and cannot be expanded, Tencent Cloud accounts registered after June 13, 2017 can create instances (including CVM and TencentDB) only in a VPC rather than the classic network. If you need to use classic network service, please submit an application.
>+ You can use the `DescribeAccountVpcAttributes` API to query the network attributes of an account. If the `supportedPlatforms` value is `only-vpc`, the account is a default VPC user, who owns all cloud resources under VPCs. If the `supportedPlatforms` value is `classic`, the account is a default classic network user, who owns all cloud resources under the classic network.
>+ You can migrate your instances from the classic network to a VPC to facilitate your use of VPC. For detailed directions, see [Switching from Classic Network to VPC](https://intl.cloud.tencent.com/document/product/215/38117).
>
![](https://main.qcloudimg.com/raw/5fe7730ac2f302d960cf20443f976b6f.png)

## Overview
By default, a VPC is a fully isolated network space that is inaccessible to other VPCs or the classic network via a private network. CCN ensures interconnections between VPCs, while the following solutions provide communications between a VPC and the classic network.
+ **Classiclink**: allows the classic network-based CVMs to communicate with VPC resources such as CVM, TencentDB, and CLB instances. However, this only provides access between VPC-based CVMs and classic network-based CVMs rather than other cloud resources including TencentDB and CLB within the classic network, as shown below.
 <img src="https://main.qcloudimg.com/raw/dc641ade1dbe4761f100088edcebaf85.png" width="50%" />
+ **Terminal connection**: helps to establish communication between instances in a VPC and resources in the classic network (except CVMs) through a private network. It maps the IP of a classic network-based instance to a VPC IP, allowing you to access the classic network-based instance through the VPC IP. This feature now supports classic network-based CLB, MySQL, Memcached, Redis and MongoDB instances. However, cross-region or cross-account communication is not supported. If you want to establish a terminal connection, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


## Creating a Classiclink
A Classiclink associates classic network-based CVMs with a VPC to enable interconnection between the VPC and the classic network. This allows classic network-based CVMs to communicate with VPC resources.

### Use limits
+ The VPC IP range must be within `10.0.0.0/16-10.47.0.0/16` (including subsets), otherwise there may be IP conflicts, which may cause failure while associating and communicating with the classic network-based CVMs.
+ A classic network-based CVM can only be associated with one VPC at a time.
+ One VPC supports associating with up to 100 classic network-based CVMs.
+ VPC resources can access classic network-based CVM rather than resources including TencentDB and CLB.
+ After associating with a VPC, classic network-based CVMs can only communicate with resources in primary CIDR block rather than secondary CIDR block of the VPC.
- A VPC can only be interconnected with the classic network in the same region.

### Notes
+ The private IPs of the associated classic network-based CVMs will be automatically added to the local policy of the VPC's route table. This allows interconnection between these CVMs and VPC-based CVMs, without the need to manually modify the routing policy of the VPC.
+ After the classic network-based CVM is associated with a VPC, their firewall and network ACL settings will remain effective. That is to say, you can configure the network ACL for the VPC subnet to restrict the access from associated classic network-based CVMs. You can also configure security group rules for CVMs in both the classic network and VPC to restrict two-way network access.
+ CLB instances within a VPC cannot be bound to a classic network-based CVM that interconnects with the same VPC.
- Changing the private IP of a classic network-based CVM will invalidate its association with the VPC, and cause the configurations become invalid. To associate them, you need to add a Classiclink again on the VPC console.
- The Classiclink will not be affected by actions taken regarding the CVM such as isolation due to overdue payment, security isolation, cold migration, failover, configuration modification, and operating system switching.
- The CVM will be automatically unassociated from the VPC if the CVM is returned.
+ In Classiclink situations, the CVM traffic can only be routed to private IP addresses within the VPC rather than destinations outside the VPC. That is, the classic network-based CVM cannot access the public or private network resources outside the current VPC through network devices such as VPN gateway, direct connect gateway, public gateway, peering connection, and NAT Gateway. Likewise, the peer of a VPN gateway, direct connect gateway, and peering connection cannot access classic network-based CVMs.

### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region, and click the ID of the VPC `TomVPC` which needs Classiclink to access the details page.
3. Click the **Classiclink** tab and then click **+Associate with CVM**. 
![](https://main.qcloudimg.com/raw/29347672a8b793f0e938ceda8b39eb77.png)
4. In the pop-up window, select the CVM in the classic network to be associated with the VPC `TomCVM` and click **OK**.
![](https://main.qcloudimg.com/raw/b3511df785851f67e0d878c473cee478.png)

## Viewing Classiclink
You can view the list of classic network-based CVMs that interconnect with the VPC.
### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region, and click the ID of the VPC which needs Classiclink to access the details page.
3. Click the **Classiclink** tab to view the list of classic network-based CVMs associated with the VPC.
![](https://main.qcloudimg.com/raw/92cb69a2842ae03c54f64eb6d55ed2ef.png)
4. Enter a private IP in the top-right corner search box to quickly locate the CVM.

<span id="release" ></span>
## Deleting a Classiclink
This action disassociates classic network-based CVMs from the VPC and terminates their interconnection.

### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click the ID of the VPC which needs Classiclink to access the details page.
3. Click the **Classiclink** tab, select the CVM to be unassociated from the list of classic network-based CVMs, and click **Disassociate** in the **Operation** column.
![](https://main.qcloudimg.com/raw/a7c164f1033b93a6722faad1ed9d2f1a.png)
4. Double check the notes and click **OK**.
5. To unassociate multiple CVMs, you can select these CVMs to be unassociated and click **Disassociate** above the list.
