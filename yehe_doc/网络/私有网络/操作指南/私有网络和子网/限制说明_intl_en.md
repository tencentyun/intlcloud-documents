### Use Limits
- The IP ranges of VPC instances and subnets cannot be modified after creation.
- For each subnet, Tencent Cloud reserves its first two IP addresses and the last IP address for IP networking. For example, if the subnet CIDR block is `172.16.0.0/24`, `172.16.0.0`, `172.16.0.1`, and `172.16.0.255` are reserved by Tencent Cloud.
- When you add a CVM to a VPC, the system randomly assigns a private IP address to this instance within the specified subnet. After creating CVMs, you can reassign the private IP address for each CVM.
- A CVM in a VPC can be bound to one private IP address and one public IP address.

## Quota Limits
| Resource | Limit |
|---------|---------|
| Number of VPC instances per region for each account | 5 | 
| Number of subnets per VPC | 10 | 
