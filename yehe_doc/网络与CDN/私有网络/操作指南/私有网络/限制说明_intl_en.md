### Use limits
- The IP ranges of the VPC and subnet cannot be modified after creation.
- For each subnet, Tencent Cloud reserves its first two IPs and the last one for IP networking. For example, if the [subnet CIDR block](https://intl.cloud.tencent.com/document/product/215/4925) is `172.16.0.0/24`, then `172.16.0.0`, `172.16.0.1`, and `172.16.0.255` are reserved by Tencent Cloud.
- When you add a CVM to a VPC, the instance will be randomly assigned with a private IP from a specified subnet. You can reassign a private IP to it after the instance is created.
- In a VPC, a CVM private IP corresponds to one public IP address.
- Classic network-based CVMs cannot interconnect with cloud resources in the secondary CIDR block.
- A peering connection does not support secondary CIDR blocks.
- Cloud Connect Network, VPN gateway, and standard direct connect gateway support secondary CIDR blocks.

### Quota limits
| Resource | Limits |
|---------|---------|
| Number of VPC instances per region per account | 20 | 
| Number of subnets per VPC | 100 | 
| Number of secondary CIDR blocks per VPC | 5 |

>?If you want to increase the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) to apply.
