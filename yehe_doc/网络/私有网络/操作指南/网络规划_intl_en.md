Before you use Tencent Cloud’s VPC services, you need to plan the quantity and IP range of your VPCs based on your business in order to prevent problems when you need to temporarily scale up.
- [How to Plan the Quantity of VPCs?](#planVPC)
- [How to Plan the Quantity of Subnets?](#planSubnet)
- [How to Plan the IP Ranges (CIDR Blocks) of VPCs and Subnets?](#planCIDR)
- [How to Plan the Quantity of Route Tables?](#planRoute)
- [How to Plan a Cross-region Multi-center Hybrid Cloud Network?](#planExample)

<span id="planVPC"  ></span>
## How to Plan the Quantity of VPCs?
- **Planning one VPC**
If your business is relatively small in volume and deployed in the same region with no need for VPC isolation, we recommend that you plan one VPC.
You can create multiple subnets and route tables in a single VPC for detailed traffic management. In addition, we recommend that you deploy multiple subnets in different availability zones for mutual disaster recovery between these zones.
![](https://main.qcloudimg.com/raw/22c3ea70430c6eaf50c994f5cb5923bc.png)
- **Planning multiple VPCs**
In any of the following scenarios, we recommend that you plan multiple VPCs:
 - **Your business is deployed in multiple regions.**
If your business is deployed in multiple regions, you need to plan multiple VPCs. A VPC cannot be deployed across regions. When you have businesses deployed in multiple regions, you need to deploy at least one VPC in each region.
By default, VPCs are not interconnected. Interconnection between VPCs can be achieved via [peering connection](https://intl.cloud.tencent.com/document/product/553) or [CCN](https://intl.cloud.tencent.com/document/product/1003).
![](https://main.qcloudimg.com/raw/8e08edafd53646887f337be56836e56c.png)
 - **Multiple businesses are deployed in the same region and require isolation.**
If you have multiple businesses deployed in the same region and these businesses must be isolated from each other, you need to plan multiple VPCs and deploy one VPC for each business. As VPCs do not intercommunicate by default, isolation between businesses can be achieved without the need for any other operations.
![](https://main.qcloudimg.com/raw/ec02b9e821f2a723a3e2d90bfab553bb.png)
<span id="planSubnet" ></span>
## How to Plan the Quantity of Subnets?
- One VPC can have multiple subnets (the default quota is 10) at a time, and different subnets in the same VPC intercommunicate with each other via private network by default.
- To achieve disaster recovery across availability zones, we recommend that you create at least two subnets in different availability zones in each VPC.

<span id="planCIDR"></span>
## How to Plan the IP Ranges (CIDR Blocks) of VPCs and Subnets?
**Once set, the IP range masks of VPCs and subnets cannot be modified.** Therefore, be sure to carefully plan VPCs and subnets based on your business scale and communication scenarios. This will facilitate smooth scaling and O&M in the future.
#### Planning VPC IP ranges
- **You can use any of the following IP ranges as your VPC’s IP range:**
 - **10.0**.0.0 - **10.255**.255.255 (**Mask range required to be between 16 - 28**)
 - **172.16**.0.0 - **172.31**.255.255 (**Mask range required to be between 16 - 28**)
 - **192.168**.0.0 - **192.168**.255.255 (**Mask range required to be between 16 - 28**)
- **When planning VPC IP ranges, note that:**
 - If you need to create multiple VPCs that must intercommunicate with each other or communicate with IDCs, make sure that the IP ranges of the VPCs do not overlap.
 - If your VPC needs to intercommunicate with the classic network, then create a VPC with the IP range of `10.[0-47].0.0/16` and its subsets. VPCs of other IP ranges cannot intercommunicate with the classic network.
 - Once created, VPC CIDR blocks and subnet CIDR blocks cannot be modified. When VPC CIDR block or subnet CIDR block addresses are insufficient, you can [create auxiliary CIDR blocks](https://intl.cloud.tencent.com/document/product/215/31805). However, as the auxiliary CIDR block feature is still in beta testing and increases operational complexity, we recommend that you carefully plan IP ranges when creating VPCs and subnets.

#### Planning subnet IP ranges
- **Subnet IP range:** you can select an IP range within your VPC’s IP range or equal to your VPC’s IP range as your subnet IP range. For example, if your VPC’s IP range is 10.0.0.0/16, you can select an IP range within 10.0.0.0/16 - 10.0.255.255/28 as the subnet IP range.
- **Subnet size and IP capacity**: once created, subnets cannot be modified. Therefore, when creating subnets, make sure that the IP capacity meets the needs of the subnet IP range. However, subnets should not be too large. Otherwise, you may be unable to create new subnets when scaling up the business in the future.
- **Business requirements**: a single VPC can be divided into subnets based on business modules. For example, you can deploy the web layer, logic layer, and data layer in different subnets. Access between subnets can be controlled using [network ACLs](https://intl.cloud.tencent.com/document/product/215/31850).

>?
>- If the VPC in which subnets are located needs to communicate with other VPCs or IDCs, make sure that the subnet IP range does not overlap with the peer IP range. Otherwise, private network intercommunication will not be possible.
>- If subnet IP ranges overlap, you can use CCN after [changing the subnets of instances](https://intl.cloud.tencent.com/document/product/213/16565), or create a new VPC and purchase CVMs.

<span id="planRoute" ></span>
## How to Plan the Quantity of Route Tables?
A route table is used to control the traffic direction within a subnet. Each subnet can be bound with only one route table. Tencent Cloud VPCs support the default route table and custom route tables.
- **Planning a route table**
If the traffic direction requirements of different subnets in your VPC are the same or similar, we recommend that you plan one route table. Then, you can create different routing policies to control the traffic directions.
![](https://main.qcloudimg.com/raw/0fdd4b7616e92011e3fd9d8141bc49a4.png)
- **Planning multiple route tables**
If the traffic direction requirements of different subnets in your VPC are very different, we recommend that you plan multiple route tables. Then, you can bind subnets with corresponding route tables based on different requirements and control the traffic directions through routing policies.
![](https://main.qcloudimg.com/raw/6f13922803b6531e77cdeb983e27b01e.png)
<span id="planExample" ></span>
## How to Plan a Cross-region Multi-center Hybrid Cloud Network?
If you need to create multiple VPCs that must intercommunicate with each other or communicate with IDCs, make sure that the IP ranges of the VPCs do not overlap with the IP ranges of the entities with which they need to communicate.
For example, assume that you have a local IDC with the IP range of `10.1.0.0/16` in Chengdu and need to create two cloud IDCs in Shanghai and Beijing, and that these two cloud IDCs need to communicate with the local IDC in Chengdu. In this case, we recommend that you plan the VPC IP ranges of the cloud IDCs in Shanghai and Beijing as `10.2.0.0/16` and `10.3.0.0/16`, respectively, to avoid communication failure caused by IP range overlap. You can enable intercommunication between the local IDC and the cloud IDCs and between the cloud IDCs using the following two methods.
- **Method 1:** use CCN to enable interconnection and intercommunication over both public and private networks.
![](https://main.qcloudimg.com/raw/05d61e7d26768a3e539858ba51d90f31.png)
- **Method 2:** use dedicated connections to connect the cloud IDCs in Shanghai and Beijing to the local IDC in Chengdu, thus enabling communication between the local IDC and the cloud IDCs. To enable communication between the cloud IDCs in Shanghai and Beijing, use peering connections to connect to the corresponding VPCs.
![](https://main.qcloudimg.com/raw/cba1d5751f6e7f6fce991b9ed3877bf9.png)

**Suggestions for multi-VPC scenarios:**
- Try to plan different IP ranges for different VPCs if possible.
- If you cannot plan different IP ranges for different VPCs, try to plan different IP ranges for the subnets of different VPCs.
- If you cannot plan different IP ranges for the subnets of different VPCs, ensure that the IP ranges of subnets that need to communicate are different.
