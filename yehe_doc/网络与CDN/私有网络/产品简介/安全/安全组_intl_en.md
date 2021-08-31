A security group is a virtual firewall that features stateful data packet filtering. It is used to configure network access control for instances such as CVMs, CLBs, and TencentDB, in order to control inbound and outbound traffic at the instance level. Therefore, it is an important isolation method for network security.
You can configure security group rules to allow or deny inbound and outbound traffic of instances within the security group.

## Characteristics
- A security group is a logical group. You can add instances (such as CVMs, ENIs, and TencentDB) with the same network security isolation requirements in the same region to the same security group.
- By default, instances associated with the same security group do not interconnect with each other. Instead, you need to add relevant rules to allow interconnection.
- Security groups are stateful. Allowed inbound traffic is automatically permitted to flow outward and vice versa.
- You can modify security group rules at any time, and the updated rules take effect immediately.

## Security Group Rules
### Components
A security group rule consists of the following components:
- Source: indicates the IP address of the source data (inbound) or target data (outbound).
- Protocol type and protocol port: the protocol type can be TCP, UDP, or HTTP.
- Policy: allow or deny the traffic.

### Priorities of rules
- Security group rules have priorities. The priorities of rules are indicated by their positions in the list. The rule at the top of the list has the highest priority and is the first to be applied. The rule at the bottom has the lowest priority.
- In case of rule conflict, the rule that ranks higher in the list prevails by default.
- When traffic goes in and out, security group rules are one by one from the top to the bottom of the list. If a certain rule is hit, the traffic is permitted, and the system no longer matches it with subsequent rules.

### Multiple security groups
An instance can be bound with one or more security groups. When the instance is bound with multiple security groups, the system performs rule matching on the groups one by one, from the top down. You can adjust the priorities of security groups at any time.

## Security Group Templates
When creating a security group, you can use the two security group templates provided by Tencent Cloud.
- Template that opens all ports: all inbound and outbound traffic will be permitted.
- Template that opens major ports: TCP port 22 (for Linux SSH login), ports 80 and 443 (for web services), port 3389 (for Windows remote login), ICMP protocol (for ping commands), and private network ports will be open to traffic.

If the provided security group templates cannot meet your actual needs, you can create custom security groups. For details, see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/215/35506) and [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/215/35519).
