A security group is a virtual firewall that features stateful data packet filtering. It is used to configure the network access control of CVM, Cloud Load Balancer, TencentDB, and other instances while controlling their outbound and inbound traffic. It is an important means of network security isolation.

You can configure security group rules to allow or reject inbound and outbound traffic of instances within the security group.

## Features
- A security group is a logical group. You can add CVM, ENI, TencentDB, and other instances in the same region with the same network security isolation requirements to the same security group.
- If a security group has no rules, it will reject all traffic by default, and you need to add rules to it to allow traffic.
- Security groups are stateful. Inbound traffic you have allowed can automatically become outbound and vice versa.
- You can modify security group rules at any time, and the new rules will take effect immediately.

## Use Limits
For use limits and quotas of security groups, see [Use Limits Overview](https://intl.cloud.tencent.com/document/product/213/15379).

## Security Group Rules

### Components

A security group rule consists of:
- **Source** or **Destination**: The source IP for an inbound rule, or the destination IP for an outbound rule. It can be an IP address, an IP range, or a security group. For more information, see [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35513).
- **Protocol Type and Protocol Port**: Protocol type, such as TCP and UDP.
- **Policy**: Allow or reject.

### Rule priorities

- The rules in a security group are prioritized from top to bottom. The rule at the top of the list has the highest priority and will take effect first, while the rule at the bottom has the lowest priority and will take effect last.
- If there is a rule conflict, the rule with the higher priority will prevail by default.
- When traffic goes in or out of an instance bound to a security group, the security group rules will be matched sequentially from top to bottom. If a rule is matched successfully and takes effect, the subsequent rules will not be matched.

### Multiple security groups

An instance can be bound to one or multiple security groups. When it is bound to multiple security groups, these security groups are executed from top to bottom. You can adjust their priorities at any time.

## Security Group Templates

Tencent Cloud provides the following two security group templates:

- **Open all ports**: All inbound and outbound traffic will be allowed to pass.
- **Open major ports**: Port TCP 22 (for Linux SSH login), ports 80 and 443 (for web service), port 3389 (for Windows remote login), the ICMP protocol (for ping commands), and the private network (for the VPC IP range) will be open to the internet.

> ?
> - If these templates cannot meet your actual needs, you can create custom security groups. For more information, see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/215/35506) and [Application Cases of Security Groups](https://intl.cloud.tencent.com/document/product/215/35519).
> - If you need to protect the application layer (HTTP/HTTPS), you can purchase [Tencent Cloud Web Application Firewall (WAF)](https://intl.cloud.tencent.com/product/waf), which provides web security at the application layer to defend against web vulnerabilities, malicious crawlers, and CC attacks, protecting your websites and web applications.

## Directions
The following figure shows how to use a security group:
![](https://main.qcloudimg.com/raw/2fccad4c688f66f28cfb3d41dbbb7134.png)

## Security Group Best Practices

### Creating security group
- We recommend you specify a security group when purchasing a CVM instance via the API; otherwise, the default security group will be used. The default security group cannot be deleted. It adopts the default security rule (i.e., allowing all IPv4 addresses), which can be modified as needed after the security group is created.
- If you need to change the instance protection policy, we recommend you modify the existing rules instead of creating a security group.

### Managing rules
- Export and back up the security group rules before you modify them, so you can import and restore them if an error occurs.
- To create multiple security group rules, use a [parameter template](https://intl.cloud.tencent.com/document/product/215/31867).

### Associating security group
- You can add instances with the same protection requirements to the same security group, instead of configuring a separate security group for each instance.
- We recommend you not bind one instance to too many security groups, which may cause rule conflicts and result in network disconnection.

## Security Group and Cloud Firewall
Tencent Cloud Firewall (CFW) is a native Tencent Cloud SaaS firewall that integrates different capabilities, including vulnerability scanning, IPS intrusion block, internet-wide threat intelligence, and advanced threat source analysis, making it the traffic security and policy management center in the cloud environment. It also serves as the first security portal for cloud business.

In practice, a security group is generally associated with Tencent Cloud products including CVM to implement the access control at the security group level. CFW is deployed in a VPC or the internet to implement the access control between VPCs or between Tencent Cloud and the internet as shown below:
![]()
You can use CFW to implement access control when a security group is insufficient to support the following use cases:

1. You need to understand the exposure and vulnerability of CVM assets on the internet and strengthen protection against network vulnerabilities through IPS intrusion prevention and virtual patching features.
2. You need to control the proactive access to the internet by domain and enhance the business security.
3. You need to implement access control by region, for example, blocking all IPs outside the Chinese mainland quickly.


