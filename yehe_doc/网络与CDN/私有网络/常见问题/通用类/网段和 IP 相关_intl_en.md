### What Are the Limits on the IP Ranges of VPC Instances and Subnets?
Tencent Cloud VPC CIDR supports one of the following private IP ranges:
- `10.0.0.0` - `10.255.255.255` (mask range: 16 - 28)
- `172.16.0.0` - `172.31.255.255` (mask range: 16 - 28)
- `192.168.0.0` - `192.168.255.255` (mask range: 16 - 28)

The CIDR blocks of subnets must be within or identical to those of the VPC.

### Can I Modify the IP Ranges of VPC Instances and Subnets?
- When creating a VPC and subnet, you need to designate their CIDR blocks, and they cannot be changed once created.
- If you cannot establish peering connections due to VPC IP range overlapping, we recommend that you use [CCN](https://intl.cloud.tencent.com/product/ccn) that has a smaller limit granularity (ensure that subnet IP ranges do not overlap) or migrate the instances in the VPC. For details on inter-VPC migration, see [Switching VPC Instances](https://intl.cloud.tencent.com/document/product/213/20278).

### What Should I Do When a Peering Connection Fails to Be Established Due to a VPC IP Range Conflict?
When you try to establish a peering connection, the CIDR blocks of VPC instances on both ends cannot overlap, otherwise the peering connection will fail to be established.
- If the subnet IP address ranges of both VPC instances that need to communicate do not overlap, you can use [CCN](https://intl.cloud.tencent.com/product/ccn) to establish communication. CCN lowers the IP range limits to the subnet level when VPC instances communicate.
For example, if the IP ranges of VPC instances that need to communicate with each other are both `10.0.0.0/16`, but those of the subnets are `10.0.1.0/24` and `10.0.2.0/24`, you can establish communication by using CCN. For more information, see [CCN Product Documentation](https://intl.cloud.tencent.com/document/product/1003).
- If your needs cannot be met by using CCN, you need to migrate the resources within the overlapping subnets.
    - For information on changing the subnets of CVMs, see [Changing Subnets of Instances](https://intl.cloud.tencent.com/document/product/213/16565).
    - For information on inter-VPC migration, see [Switching VPC Instances](https://intl.cloud.tencent.com/document/product/213/20278).

### Can I Modify the Private IP Addresses of Resources (CVMs and Databases) in VPC Instances?
- Modifying the primary private IP address of a CVM’s primary ENI is supported, but modifying the primary private IP of a secondary ENI is not supported. For details, see [Modifying a Private IP Address](https://intl.cloud.tencent.com/document/product/213/16561).
- The private IP addresses of private network cloud load balancers (CLBs) or cloud databases (TencentDB) cannot be modified.

### Can I Switch the CVMs or Databases in a VPC to Another VPC?
- CVM migration is currently supported, but the migration of databases and other resources is not supported at this time.
- CVMs can be migrated from the current VPC to another VPC under the same account. For details on the steps and instructions, see [Switching VPC Instances](https://intl.cloud.tencent.com/document/product/213/20278).

### What Do EIPs Do?
ElPs apply to the following scenarios:
1. **Disaster recovery**
We strongly recommend that you use EIPs for disaster recovery. When one of your CVMs fails to provide service, you can unbind the EIP from this CVM and rebind it to a healthy CVM to restore service quickly.
2. **Retaining a specific public IP address**
To retain a specific public IP address under your account, you can convert it to an EIP, which then can be used to access public networks after being bound to a device. This EIP will be retained under your account until it is "released" by you.
3. **Other special scenarios**
When you need to change an IP address in other special cases, you can convert the common public IP address to an EIP and then bind or unbind the EIP as needed. However, with limited EIP resources available, a quota is imposed on the number of EIPs for each region under a single account. Therefore, we recommend that you plan and use EIPs reasonably.

### How Can I Keep a Public IP Address Unchanged?
To retain a specific public IP address under your account, you can convert it to an EIP, which then can be used to access public networks after being bound to a device. This EIP will be retained under your account until it is "released" by you.

For relevant instructions, see [Converting a Public IP Address to an EIP](https://intl.cloud.tencent.com/document/product/213/16586).

### Can I Convert an EIP Back to a Public IP Address?
An EIP cannot be converted back to a public IP address.

