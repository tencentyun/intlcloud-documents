### Use Limits
- One network ACL can be bound with multiple subnets.
- Network ACLs are stateless. Therefore, you need to set outbound rules and inbound rules respectively.
- Network ACLs do not affect private network intercommunication among CVM instances in the associated subnets.

### Quota Limits
| Resource | Limit |
| -------------- | ----------------- |
| Number of network ACLs in each VPC | 50 |
| Number of rules per network ACL | Inbound: 20<br/>Outbound: 20 |
| Number of network ACLs associated with each subnet | 1 |

