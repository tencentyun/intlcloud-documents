Before using Tencent Cloud VPC, you need to plan the quantity and IP range of your VPCs based on your business in order to prevent problems when you need to temporarily scale up.
- [How to Plan the Quantity of VPCs?](#planVPC)
- [How to Plan the Quantity of Subnets?](#planSubnet)
- [How to Plan the IP Ranges (CIDR Blocks) of VPCs and Subnets?](#planCIDR)
- [How to Plan the Quantity of Route Tables?](#planRoute)
- [How to Plan a Cross-region Multi-center Hybrid Cloud Network?](#planExample)

<span id="planVPC"  ></span>
## How to Plan the Quantity of VPCs?
- **Planning one VPC**
If you have small scale business that is deployed in the same region without the need for network isolation, we recommend that you plan one VPC.
You can create multiple subnets and route tables in a single VPC for detailed traffic management. In addition, we recommend that you deploy multiple subnets in different availability zones for mutual disaster recovery.
![](https://main.qcloudimg.com/raw/22c3ea70430c6eaf50c994f5cb5923bc.png)
- **Planning multiple VPCs**
We recommend that you plan multiple VPCs in any of the following scenarios:
 - **Your business is deployed in multiple regions**
If your business is deployed in multiple regions, you need to plan multiple VPCs and deploy at least one in each region because VPC cannot be deployed across regions.
By default, VPCs are not interconnected. To interconnect VPCs, use [peering connection](https://intl.cloud.tencent.com/document/product/553) or [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
![](https://main.qcloudimg.com/raw/8e08edafd53646887f337be56836e56c.png)
 - **Multiple businesses are deployed in the same region and require isolation**
If you have multiple businesses deployed in the same region and these businesses must be isolated from each other, you need to plan multiple VPCs and deploy one VPC for each business. This isolates businesses without the need for any other operations since VPCs are not interconnected by default.
![](https://main.qcloudimg.com/raw/ec02b9e821f2a723a3e2d90bfab553bb.png)
<span id="planSubnet" ></span>
## How to Plan the Quantity of Subnets?
- One VPC can have multiple (10 by default) subnets. Different subnets in the same VPC can communicate with each other over a private network by default.
- To achieve disaster recovery across availability zones, we recommend that, in each VPC, you create at least two subnets in different availability zones.

<span id="planCIDR"></span>
## How to Plan the IP Ranges (CIDR Blocks) of VPCs and Subnets?
**Once set, the IP range masks of VPCs and subnets cannot be modified.** Therefore, be sure to carefully plan VPCs and subnets based on your business scale and communication scenarios. This will facilitate smooth scaling and OPS in the future.
#### Planning VPC IP ranges
- **You can use any of the following IP ranges as your VPC IP ranges:**
 - **10.0**.0.0 - **10.255**.255.255 (**the mask range must be between 16-28**)
 - **172.16**.0.0 - **172.31**.255.255 (**the mask range must be between 16-28**)
 - **192.168**.0.0 - **192.168**.255.255 (**the mask range must be between 16-28**)
- **When planning VPC IP ranges, note that:**
 - If you need to create multiple VPCs that communicate with each other or with IDCs, make sure that the IP ranges of the VPCs do not overlap.
 - If your VPC needs to communicate with the classic network, please create a VPC within the `10.[0-47].0.0/16` IP range or a part of it, as other IP ranges cannot communicate with the classic network.
 - Once created, VPC CIDR blocks and subnet CIDR blocks cannot be modified. When VPC CIDR block or subnet CIDR block addresses are insufficient, you can [create auxiliary CIDR blocks](https://intl.cloud.tencent.com/document/product/215/31805). However, this feature is still in beta and increases operational complexity, we recommend that you carefully plan IP ranges when creating VPCs and subnets.

#### Planning subnet IP ranges
- **Subnet IP range**: you can use your VPC IP range or a part of it as the subnet IP range. For example, if the VPC IP range is 10.0.0.0/16, you can select an IP range between 10.0.0.0/16-10.0.255.255/28 as the subnet IP range.
- **Subnet size and IP capacity**: once created, subnets cannot be modified. When creating subnets, make sure that the subnet IP ranges can meet your business needs. However, subnets should not be too large. Otherwise, you may be unable to create new subnets when scaling up the business in the future.
- **Business requirements**: a single VPC can be divided into subnets based on business segments. For example, you can deploy the web layer, logic layer, and data layer in different subnets and use [network ACLs](https://intl.cloud.tencent.com/document/product/215/31850) to implement the access control.

>?
>- If the VPC in which subnets are located needs to communicate with other VPCs or IDCs, make sure that the subnet IP range does not overlap with the peer IP range. Otherwise, the interconnection via private network may fail.
>- If subnet IP ranges overlap, you can use CCN after [changing the instance subnet](https://intl.cloud.tencent.com/document/product/213/16565), or create a new VPC and purchase CVMs.

<span id="planRoute" ></span>
## How to Plan the Quantity of Route Tables?
A route table is used to control the traffic direction within a subnet. Each subnet can be bound with only one route table. Tencent Cloud VPCs support the default route table and custom route tables.
- **Planning one route table**
If different subnets in your VPC have the same or similar requirements for traffic direction, we recommend planning one route table. Then, you can create different routing policies to control the traffic direction.
![](https://main.qcloudimg.com/raw/0fdd4b7616e92011e3fd9d8141bc49a4.png)
- **Planning multiple route tables**
If different subnets in your VPC have different requirements for traffic direction, we recommend planning multiple route tables. Then, you can bind them to subnets and create routing policies to control the traffic direction.
![](https://main.qcloudimg.com/raw/6f13922803b6531e77cdeb983e27b01e.png)
<span id="planExample" ></span>
## How to Plan a Cross-region Multi-center Hybrid Cloud Network?
If you need to create multiple VPCs that communicate with each other or with IDCs, make sure that the IP ranges of the VPCs do not overlap with the peer IP range.
For example, assume that you have a local IDC with the IP range of `10.1.0.0/16` in Chengdu and want to create two cloud IDCs in Shanghai and Beijing, and that these two cloud IDCs need to communicate with the local IDC in Chengdu. In this case, we recommend that you use `10.2.0.0/16` and `10.3.0.0/16` as the VPC IP ranges of the cloud IDCs in Shanghai and Beijing respectively, to avoid communication failure caused by overlapping IP ranges. You can enable communication between local IDC and cloud IDCs and between the cloud IDCs using the following two methods.
- **Method 1:** add them to a CCN to implement the interconnection over the public and private network.
![](https://main.qcloudimg.com/raw/05d61e7d26768a3e539858ba51d90f31.png)
- **Method 2:** use Direct Connect to connect the cloud IDCs in Shanghai and Beijing to the local IDC in Chengdu, thus enabling communication between the local IDC and the cloud IDCs. To enable communication between the cloud IDCs in Shanghai and Beijing, use peering connection to connect corresponding VPCs.
![](https://main.qcloudimg.com/raw/cba1d5751f6e7f6fce991b9ed3877bf9.png)

**Suggestions for multi-VPC scenarios:**
- Try to plan different IP ranges for different VPCs.
- Try to plan different IP ranges for VPC subnets if each VPC cannot have distinct IP range.
- Ensure that the IP ranges of subnets that need to communicate are different if each subnet cannot have distinct IP range.

## Documentation
- For more information about how to quickly build a Virtual Private Cloud (VPC) with IPv4 CIDR block, including creating a VPC and subnet, purchasing a CVM, and binding an EIP to enable public network access, see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).
