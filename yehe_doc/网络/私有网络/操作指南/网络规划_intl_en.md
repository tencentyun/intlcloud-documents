Before using Tencent Cloud VPC, you need to plan the quantity and IP range of your VPC instances based on your business to prevent problems resulting from temporary scale-out or similar.
During planning, pay attention to the belonging region, VPC instances, number of subnets, IP ranges, and route tables.

## Planning Regions
Each VPC belongs to a specific region (for example, Guangzhou), and each region contains one or more availability zones (such as Guangzhou Zone 1 and Guangzhou Zone 2). You can choose an appropriate region to create VPC instances and subnets.
Note that even if two VPC instances are present in the same region and isolated from each other by default within the private network, private network communication is enabled only in the same VPC by default. To enable private network communication between different VPC instances, establish a [peering connection](https://intl.cloud.tencent.com/document/product/553) or use [CCN](https://intl.cloud.tencent.com/document/product/1003).
![](https://main.qcloudimg.com/raw/f0eb1a194187ec95a03881db3d4ae1b3.png)

## Planning VPC Instances
### Planning a VPC
If your business volume is relatively small and the business is deployed in the same region without the demand for network isolation, we recommend that you plan one VPC.
You can create multiple subnets and route tables in a single VPC to achieve refined traffic management.
![](https://main.qcloudimg.com/raw/e858339e22584215e9e9af4286d03468.png)

### Planning multiple VPC instances
In the following scenarios, we recommend that you plan multiple VPC instances:
- **Your business is deployed in multiple regions**
As VPC instances are region-specific, they cannot be deployed across different regions. When your business is deployed in multiple regions, you must plan multiple VPC instances.
VPC instances in different regions can implement private network communication through [peering connection](https://intl.cloud.tencent.com/document/product/553) or [CCN](https://intl.cloud.tencent.com/document/product/1003).
- **Multiple businesses need to be isolated from each other**
As private network communication is enabled within the same VPC by default, if you have different businesses in the same region need to be isolated from each other, you must plan multiple VPC instances.
![](https://main.qcloudimg.com/raw/4de88098290c378caf1cabbd2b040266.png)

## Planning Subnets
Each Tencent Cloud VPC supports creating a maximum of 10 subnets, which are IP address blocks within VPC instances. The IP range of subnets must fall within or be identical to the VPC’s IP range. One VPC can simultaneously contain multiple subnets, and different subnets in the same VPC intercommunicate with each other through the private network by default.
Consider the following when planning subnets:
- **Subnet size and number of IP addresses**
When creating subnets, ensure that the number of IP addresses in the subnet IP range meets your requirements. However, the size of the subnets should not be too big in case you may need to create new subnets when expanding business in the future.
- **Subnet IP range**
If the VPC in which subnets are located needs to communicate with other VPC instances or IDCs, ensure that the subnet IP range does not overlap with the IP range of the peer end. Otherwise, private network communication fails.
- **Business requirements**
A single VPC can be divided into multiple subnets based on business modules, such as deploying the web layer, logic layer, and data layer in different subnets. Access to subnets can be controlled by using [Network ACLs](https://intl.cloud.tencent.com/document/product/215/5132).
![](https://main.qcloudimg.com/raw/7cf89e24bc7bba66fec60c8142b454ad.png)

## Planning IP Ranges
Tencent Cloud VPC CIDR supports using any of the following private IP ranges:
- **10.0**.0.0 - **10.255**.255.255 (**The mask must range from 16 to 28.**)
- **172.16**.0.0 - **172.31**.255.255 (**The mask must range from 16 to 28.**)
- **192.168**.0.0 - **192.168**.255.255 (**The mask must range from 16 to 28.**)

#### IP range explanation
- To create multiple VPC instances that need to communicate with each other or with IDCs, ensure that the IP ranges of VPC instances do not overlap with each other. Otherwise, peering connections and CCN do not work.
- If your VPC needs to communicate with the basic network, create a VPC with the IP range falling within `10.[0-47].0.0/16` or its subsets. Classiclink cannot be created for VPC instances in other IP ranges.
- If subnet IP ranges overlap, you can [change subnets of instance](https://intl.cloud.tencent.com/document/product/213/16565) and then use CCN. Alternatively, you can re-create a VPC or purchase a CVM.


## Planning Route Tables
A route table is used to control the traffic route within a subnet. Each subnet can be bound to one route table. Tencent Cloud VPC instances support the default route table and custom route tables.
### Planning a route table
If the traffic route requirements of different subnets in your VPC are the same or similar, we recommend that you plan one route table. You can create different routing policies to control different traffic routes.
![](https://main.qcloudimg.com/raw/266543085902f18e038017a63162c5f4.png)
### Planning multiple route tables
If the traffic route requirements of different subnets in your VPC are different, we recommend that you plan multiple route tables. To do this, bind subnets with corresponding route tables based on different requirements, and control specific traffic routes by defining routing policies.
![](https://main.qcloudimg.com/raw/0f13fc52b27f01ae1b2e278d6f09c70a.png)

