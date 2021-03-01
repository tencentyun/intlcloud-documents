Other than your CVM model and VPC configuration, these factors also influence how much your service costs:
- Billing method
- Resource used
- Quantity

### Billing method
- **Pay as you go** is a flexible billing method for CVM instances. You can launch/terminate a CVM at any time and are billed by the actual usage of the CVM. You pay by the second and no up-front payment is required. A bill is generated every hour on the dot. This billing method is suitable for use cases such as an e-commerce flash sale where the demand for resources can fluctuate greatly.
- **Spot Instance** is a new way to use and pay for CVM instances. Similar to Pay as you go, you pay for Spot Instances by the second, every hour. The price of Spot Instances fluctuates according to market demand. You get a sizable discount for them when the demand is low (usually 10 to 20%). However, they might be repossessed automatically by the system as the demand becomes high.

### Resources used
- Region:
	- The price is the same for the same instance model in different regions in Mainland China.
	- The price might be the same for the same instance model in different regions outside Mainland China.
- Image:
	- Public images: all public images in Mainland China hosted by Tencent Cloud are free. Windows images outside Mainland China require licensing fees.
	- Custom image: creating custom images, importing custom images, and copying custom images across regions are free of charge.
	- Shared images: shared images from other Tencent Cloud users are free of charge.
Network:
	- VPC, Subnet, Route Table, Network ACL, Security Group, Direct Connect Gateway, VPN Tunnel, and Customer Gateway are free of charge.
	- Bandwidth costs are not applicable to inter-instance communication within different subnets. Intra-region peering connections are free as well.
	- Refer to [this article](https://intl.cloud.tencent.com/document/product/213/10578) for details on the public network billing method.
	- For details on charges for NAT Gateway, VPN Gateway, and Cross-region Peering connection.
- Storage:
	For the prices of local disks and cloud disks, refer to [this article](https://intl.cloud.tencent.com/document/product/362/2413)


### Quantity

The number of CVMs you purchase also affects the price you pay. More CVMs means a higher price.
