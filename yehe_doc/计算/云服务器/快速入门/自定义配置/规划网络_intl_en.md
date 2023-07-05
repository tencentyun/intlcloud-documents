A Tencent Cloud Virtual Private Cloud (VPC) instance is a user-defined logically isolated network space on Tencent Cloud. In this instance, users can customize IP ranges, IP addresses, and routing policies. Therefore, Tencent Cloud recommends that you use a VPC instance for your businesses.

To help you better use Tencent Cloud VPC instances, Tencent Cloud provides the following network planning recommendations.

### Determining the number of VPC instances

- Features:
	- VPC instances are region-specific. By default, CVMs in different regions cannot communicate with each other. If cross-region communication is required, establish a [peering connection](https://intl.cloud.tencent.com/document/product/553).
	- By default, different VPC instances in the same region cannot communicate with each other. If cross-VPC communication is required, establish a [peering connection](https://intl.cloud.tencent.com/document/product/553).
	- By default, different availability zones in the same VPC instance can communicate with each other.
- Recommendations:
	- If your business requires cross-region system deployment, multiple VPC instances are required. In this case, you can build a VPC instance that is close to the region where your customers are located to reduce access latency and improve the access speed.
	- If you have deployed multiple businesses in the current region and want to implement network isolation among different businesses, you can build a VPC instance for each business in the current region.
	- If you do not require cross-region business deployment or network isolation among businesses, you can use one VPC instance.

### Determining subnet division
- Features:
	- Subnets are IP address blocks in a VPC instance. All cloud resources in a VPC instance must be deployed in subnets.
	- In the same VPC instance, the IP ranges of subnets must not overlap.
	- Tencent Cloud automatically assigns initial private IP addresses from VPC IP ranges. The Tencent Cloud VPC CIDR block can be any of the following VPC IP ranges. For an IP address within these ranges, its mask ranges from 16 to 28, and the actual mask is determined by the private network where the instance resides.
	 - **10.0**.0.0-**10.255**.255.255
	 - **172.16**.0.0-**172.31**.255.255
	 - **192.168**.0.0-**192.168**.255.255
	- After a VPC instance is created, its IP range cannot be modified.
- Recommendations:
	- If only VPC subnets need to be divided and communication with the basic network or IDC is not involved, choose any of the preceding IP ranges to create a subnet.
	- If communication with the basic network is required, establish a VPC instance with the IP range of 10.[0-47].0.0/16 and its subsets as required.
	- If a VPN is required, the local IP range (of the VPC instance) and the peer IP range (of your IDC) cannot overlap. Therefore, do not use the peer IP range when creating a subnet.
	- During subnet division, you also need to consider the number of available IP addresses within an IP range.
	- We recommend that subnets be divided according to the business modules for businesses in the same VPC instance. For example, subnet A is used for the web layer, subnet B is used for the logic layer, and subnet C is used for the database layer. This facilitates access control and filtering by using the network ACL.

### Determining route policies

- Features:
	- A route table consists of a series of routing rules that control the traffic flow of subnets in a VPC instance.
	- Each subnet must be associated with only one route table.
	- A single route table can be associated with multiple subnets.
	- When a VPC instance is created, the system automatically generates a default route table for the instance, which defines that VPC instances can communicate with each other through the private network.
- Recommendations:
	- If you do not need to control the traffic flow of subnets and VPC instances are interconnected through the private network by default, you can use the default route table without needing to configure a custom routing policy.
	- If you need to control the traffic flow of subnets, see [Overview](https://intl.cloud.tencent.com/document/product/215/31810) on the official website.


For more information on VPC instances, see [VPC](https://intl.cloud.tencent.com/document/product/215).



