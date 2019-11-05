>! The number of IP addresses bound to a single ENI only represents the upper limit of IP addresses that ENIs can bind to. It’s not the available EIP quota. For the EIP quota of your account, please refer to EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).

## VPC Basic Quota
| Resource | Limit | 
|---------|:---------:|
| Number of VPCs per region for each account | 5 | 
| Number of subnets per VPC | 10 | 
| Number of basic network CVMs to be associated per VPC | 100 |
| Number of route tables per VPC | 10 | 
| Number of routing policies per route table | 50 | 
| Number of peering connections per VPC | 10 | 
| Number of NAT gateways per VPC | 3 | 
| Number of EIPs per NAT gateway | 10 |
| Maximum forwarding capability per NAT gateway | 5 Gbit/s |
| Number of VPN gateways per VPC | 10	 | 
| Number of customer gateways in a region | 20 | 
| Number of VPN tunnels per customer gateway | 10 | 
| Number of VPN tunnels that can be created on a VPN gateway | 20 | 
| Number of SPDs per VPN tunnel | 10 | 
| Number of peer IP address ranges per SPD | 50 | 
| Number of network ACLs per VPC | 50 |
| Number of rules per network ACL | Inbound: 20, outbound: 20. |
| Number of associated network ACLs per subnet | 1 |

## Direct Connect Quota
| Resource | Limit | Support requesting a higher quota |
|------|:-----:|:-----:|
| Connections per user | 10 | Yes |
| Dedicated tunnels per connection | 20 | No |
| Direct connect gateways (with NAT supported) per VPC | 1 | No |
| Direct connect gateways (with NAT unsupported) per VPC | 1 | No |
| Local IP translations per direct connect gateway | 100 | Yes |
| Peer IP translations per direct connect gateway | 100 | Yes |
| Number of IP addresses for local source IP port translation per direct connect gateway | 20 | Yes |
| Number of IP addresses for local destination IP port translation per direct connect gateway | 100 | Yes |

