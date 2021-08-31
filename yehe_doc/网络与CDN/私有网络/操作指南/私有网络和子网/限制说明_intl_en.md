### Use limits
- The IP ranges of VPCs and subnets cannot be modified after creation.
- For each subnet, Tencent Cloud reserves its first two IP addresses and the last IP address for the purpose of IP networking. For example, if the subnet CIDR is `172.16.0.0/24`, then the IP addresses reserved by Tencent Cloud are `172.16.0.0`, `172.16.0.1`, and `172.16.0.255`.
- When you add a CVM to a VPC, the system randomly assigns a private IP address to its instance within the specified subnet, and you can reassign the private IP address for each CVM after the CVMs are created.
- In a VPC , a CVM private IP corresponds to one public IP address.
- Classic network CVMs do not support interconnection with cloud resources in the auxiliary CIDR block.
- Currently, only Cloud Communication Network (CCN) supports passing the auxiliary CIDR block. This means services in the auxiliary CIDR block cannot communicate via VPN connection, Direct Connect, or peering connection.

### Quota limits
| Resource | Limit/qty |
|---------|---------|
| Number of VPCs per region for each account | 20 |
| Number of subnets per VPC | 100 |
| Number of auxiliary CIDR blocks per VPC | 5 |

>? If you need to increase the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) to apply.

