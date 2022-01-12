### What are the limits on the IP ranges of VPCs and subnets?
Tencent Cloud VPC CIDR block supports the use of any one of the following private IP ranges:
- `10.0.0.0` - `10.255.255.255` (mask range between 16 and 28)
- `172.16.0.0` - `172.31.255.255` (mask range between 16 and 28)
- `192.168.0.0` - `192.168.255.255` (mask range between 16 and 28)

The subnet CIDR block must be within or the same as the VPC CIDR block.

### Can the IP ranges of VPCs and subnets be modified?
- When creating the VPC and subnet, you need to designate their CIDR blocks, and they cannot be changed once they are created.
- If you cannot establish a peering connection due to the overlapping of VPC IP ranges, you can try [Cloud Connect Network](https://intl.cloud.tencent.com/product/ccn), which has smaller limit granularity (only subnet IP ranges cannot overlap) or migrate the instances to another VPC. For details, see [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### What should be done when a peering connection fails to be established because of a VPC IP range conflict?
When establishing a peering connection, the CIDR blocks of the two VPCs cannot overlap, or else the peering connection will fail to be established.
- If the subnet IP ranges of two VPCs that need to communicate do not overlap, then you can use [CCN](https://intl.cloud.tencent.com/product/ccn) to establish communication. CCN lowers the IP range limits to the subnet level when VPCs communicate.
For example, if the IP ranges of the two VPCs that need to communicate with each other are `10.0.0.0/16`, but the subnets are respectively `10.0.1.0/24` and `10.0.2.0/24`, then you can establish communication using CCN. Refer to [CCN Product Documentation](https://intl.cloud.tencent.com/document/product/1003).
- If your needs are not met by using CCN, then you need to migrate the resources inside the overlapping subnets.
    - For details on changing the subnet of the CVM, see [Changing Instance Subnet](http://intl.cloud.tencent.com/document/product/213/16565).
    - Migrate the instances within VPC as instructed in [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### Can I modify the private IPs of resources in VPCs (CVMs and databases)?
- You can modify the primary private IP of a CVM’s primary ENI, but the primary private IP of a secondary ENI cannot be modified. For details, see [Modifying Private IP Addresses](https://intl.cloud.tencent.com/document/product/213/16561).
- You can modify the private IP of TencentDB instances (such as MySQL instances). See [Customizing IP and Port](https://intl.cloud.tencent.com/document/product/236/31915).
- The private IP of CLB cannot be modified.

### Can I migrate CVMs or databases from one VPC to another?
- For now, you can migrate CVM instances and TencentDB for MySQL instances to another VPC under the same account. Other TencentDB instances are not supported.
- To migrate CVM instances, see [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).
- To migrate TencentDB for MySQL instances, see [Network Switch](https://intl.cloud.tencent.com/document/product/236/31915).

### What do EIPs do?
ElPs are applicable to the following scenarios:
1. **Disaster recovery**
We strongly recommend that you use EIPs for disaster recovery. When one of your CVMs fails to normally provide services, you can unbind the EIP from this CVM and rebind it to a healthy CVM to resume service quickly.
2. **Retaining a specific public IP**
If you need to retain a specific public IP under your account, you can convert it to an EIP, which then can be used to access public networks after being bound to the device. This EIP will be retained under your account until it is "released" by you.
3. **Other special scenarios**
When you need to change an IP in other special cases, you can convert the ordinary public IP to an EIP and then bind/unbind the EIP. However, with limited EIP resources available, a quota is imposed on the number of EIPs for each region under a single account. Therefore, reasonable planning and use of EIPs are very important.

### How do I keep a public IP unchanged?
If you need to retain a specific public IP under your account, you can convert it to an EIP, which then can be used to access public networks after being bound to the device. This EIP will be retained under your account until it is "released" by you.
For directions, see [Converting common public IPs to EIPs](https://intl.cloud.tencent.com/document/product/213/16586#convert-a-public-ip-to-an-eip).

### Can an EIP be converted back to a public IP?
An EIP cannot be converted back to a public IP.



