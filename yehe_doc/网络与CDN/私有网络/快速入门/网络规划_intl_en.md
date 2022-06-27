Before using Tencent Cloud VPCs, you need to plan the number and IP ranges of the VPCs based on your business needs to avoid issues caused by temporary scaling.
- [How do I plan the number of VPCs?](#planVPC)
- [How do I plan the number of subnets?](#planSubnet)
- [How do I plan the IP ranges (CIDR blocks) of VPCs and subnets?](#planCIDR)
- [How do I plan the number of route tables?](#planRoute)
- [How do I plan a cross-region multi-center hybrid cloud network?](#planExample)

## How do I plan the number of VPCs?[](id:planVPC)
- **Planning one VPC**
If your businesses involve a small amount of data and are deployed in the same region without the need to be isolated through VPCs, we recommend you plan one VPC.
You can create multiple subnets and route tables in a VPC for refined traffic management. In addition, we recommend you deploy subnets in different AZs for disaster recovery.
![](https://main.qcloudimg.com/raw/22c3ea70430c6eaf50c994f5cb5923bc.png)
- **Planning multiple VPCs**
We recommend you plan multiple VPCs in any of the following use cases:
   - **Your business is deployed in multiple regions**
If your business is deployed in multiple regions, you need to plan multiple VPCs and deploy at least one in each region because a VPC cannot be deployed across regions.
VPCs are not interconnected by default. To interconnect VPCs, use a [peering connection](https://intl.cloud.tencent.com/document/product/553) or [Cloud Connect Network instance](https://intl.cloud.tencent.com/document/product/1003).
![](https://main.qcloudimg.com/raw/8e08edafd53646887f337be56836e56c.png)
   - **Multiple businesses are deployed in the same region and require isolation**
If you have multiple businesses deployed in the same region and these businesses must be isolated from each other, you need to plan multiple VPCs and deploy one VPC for each business. Doing this can isolate businesses because VPCs are not interconnected by default.
![](https://main.qcloudimg.com/raw/ec02b9e821f2a723a3e2d90bfab553bb.png)

## How do I plan the number of subnets?[](id:planSubnet)
- One VPC can have multiple (100 by default) subnets. Different subnets in the same VPC can communicate with each other over a private network by default.
- To implement cross-AZ disaster recovery, we recommend you create at least two subnets in different AZs in a VPC.


## How do I plan the IP ranges (CIDR blocks) of VPCs and subnets?[](id:planCIDR)
**Once set, the IP range masks of VPCs and subnets cannot be modified.** Therefore, be sure to carefully plan VPCs and subnets based on your business scale and communication scenarios. This will facilitate smooth scaling and Ops in the future.
>?
>- Both IPv4 and IPv6 addresses are supported in VPCs. IPv6 addresses are GUAs rather than private addresses, so custom planning is not supported. This document describes how to plan private IPv4 ranges.
>- IPv6 addresses are assigned based on the following rules: a `/56` IPv6 CIDR block is assigned to each VPC, a `/64` IPv6 CIDR block is assigned to each subnet, and an IPv6 address is assigned to each ENI.
>
#### Planning VPC IP ranges
- **You can use any of the following IP ranges as your VPC IP ranges:**
   - **10.0**.0.0 - **10.255**.255.255 (**the mask range must be 12 to 28**)
   - **172.16**.0.0 - **172.31**.255.255 (**the mask range must be 12 to 28**)
   - **192.168**.0.0 - **192.168**.255.255 (**the mask range must be 16 to 28**)
- **When planning VPC IP ranges, note that:**
   - If you need to create multiple VPCs that communicate with each other or with IDCs, make sure that the IP ranges of the VPCs do not overlap.
   - If your VPC needs to communicate with the [classic network](https://intl.cloud.tencent.com/document/product/215/41417), create a VPC with an IP range of `10.[0~47].0.0/16` and its subset, as VPCs with other IP ranges cannot communicate with the classic network.
   - Neither the CIDR blocks of a VPC nor its subnets can be modified after the VPC creation. When either the CIDR blocks of a VPC or its subnets are insufficient, you can [create secondary CIDR blocks](https://intl.cloud.tencent.com/document/product/215/40070).

#### Planning subnet IP ranges
- **Subnet IP range**: You can use your VPC IP range or a part of it as the subnet IP range. For example, if the VPC IP range is `10.0.0.0/16`, the subnet IP range can be between `10.0.0.0/16` and `10.0.255.255/28`.
- **Subnet size and IP capacity**: As subnets cannot be modified once created, make sure that the subnet IP ranges can meet your business needs when creating subnets. However, you also need to control the subnet size, so that you can create subnets later for the scale-out.
- **Business requirements**: A VPC can be divided into subnets based on business modules. For example, you can deploy the web layer, logic layer, and data layer in different subnets and use a [network ACL](https://intl.cloud.tencent.com/document/product/215/31850) to implement the access control.

>?
>- If the VPC of subnets needs to communicate with other VPCs or IDCs, make sure that the subnet IP range does not overlap with the peer IP range; otherwise, the interconnection over the private network may fail.
>- If subnet IP ranges overlap, you can [change the instance subnet](https://intl.cloud.tencent.com/document/product/213/16565) and use CCN, or create a VPC and purchase a CVM instance.

## How do I plan the number of route tables?[](id:planRoute)
A route table is used to control the traffic direction within a subnet. Each subnet can be bound to only one route table. Default and custom route tables can be used in Tencent Cloud VPCs.
- **Planning one route table**
If different subnets in your VPC have the same or similar requirements for traffic direction, we recommend you plan one route table. Then, you can create different routing policies to control the traffic direction.
![](https://main.qcloudimg.com/raw/0fdd4b7616e92011e3fd9d8141bc49a4.png)
- **Planning multiple route tables**
If different subnets in your VPC have different requirements for traffic direction, we recommend you plan multiple route tables, bind subnets with different requirements to corresponding routing tables, and use routing policies to control the traffic direction.
![](https://main.qcloudimg.com/raw/6f13922803b6531e77cdeb983e27b01e.png)

## How do I plan a cross-region multi-center hybrid cloud network?[](id:planExample)
If you need to create multiple VPCs that communicate with each other or with IDCs, make sure that the IP ranges of the VPCs do not overlap with the peer IP range.

Suppose you have a local IDC with the IP range of `10.1.0.0/16` in Chengdu region and want to create two on-cloud IDCs in Shanghai and Beijing regions that need to communicate with the local IDC. In this case, we recommend you use `10.2.0.0/16` and `10.3.0.0/16` as the VPC IP ranges of the two on-cloud IDCs to avoid communication failure caused by overlapping IP ranges. You can establish communication between the local IDC and the on-cloud IDCs (that is, between the IDC and VPC 1 and between the IDC and VPC 2) and between the on-cloud IDCs (that is, between VPCs 1 and 2) by using the following two methods.
- **Method 1.** Connect them over a CCN instance for global connectivity.
![](https://main.qcloudimg.com/raw/05d61e7d26768a3e539858ba51d90f31.png)
- **Method 2.** Connect the on-cloud IDCs in Shanghai and Beijing regions to the local IDC in Chengdu region through Direct Connect to implement communication between the local IDC and the on-cloud IDCs, and connect the VPCs of the on-cloud IDCs in Shanghai and Beijing regions through a peer connection to implement communication between the on-cloud IDCs.
![](https://qcloudimg.tencent-cloud.cn/raw/21d2268615b2daeb1f2df09dc37e0334.png)

**Suggestions for multi-VPC use cases:**
- Try to plan different IP ranges for each VPC.
- If each VPC cannot have a distinct IP range, then plan different IP ranges for subnets in different VPCs.
- If each VPC subnet cannot have a distinct IP range, make sure that the IP ranges of subnets needed for communication are different.

## References
- For more information on how to quickly build a VPC with an IPv4 CIDR block, including creating a VPC and subnet, purchasing a CVM instance, binding an EIP, and eventually implementing public network access, see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).

