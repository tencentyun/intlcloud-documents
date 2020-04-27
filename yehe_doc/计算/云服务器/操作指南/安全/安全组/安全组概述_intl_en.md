A security group is a virtual firewall and features stateful data packet filtering. It is used to configure the network access control of CVM, Cloud Load Balancer, TencentDB, and other instances, while controlling their outbound and inbound traffic. It is an important means of network security isolation.
You can configure security group rules to allow or reject inbound traffic and outbound traffic of instances within the security group.

## Security group features
- A security group is a logical group. You can add CVM, ENI, TencentDB, and other instances in the same region with the same network security isolation requirements to the same security group.
- By default, instances associated with the same security group are not interconnect with each other, unless you add relevant rules.
- Security groups are stateful. Inbound traffic you have allowed can automatically go outward and vice versa.
- You can modify security group rules at any time, and the new rules take effect immediately.

## Security group rules
### Components
A security group rule consists of the following components:
- Source: IP address of the source data (inbound) or target data (outbound).
- Protocol type and protocol port: protocol type can be TCP, UDP, HTTP, etc.
- Policy: allow or reject.

### Rule Priorities
- Security group rules have priorities, which are indicated by their positions in the list. The rule at the top of the list has the highest priority and is the first to be applied. The rule at the bottom has the lowest priority.
- In case of rule conflict, the rule that is higher in the list prevails.
- When traffic enters or exits an instance that is bound to a security group, the security group rules will be matched in order from top to bottom. If a rule is matched successfully, the traffic is allowed to pass and the system no longer matches it with subsequent rules.

### Multiple security groups
An instance can be bound with one or multiple security groups. When it is bound with multiple security groups, the security group rules will be matched in order from top to bottom. You can adjust security group priorities at any time.

## Security group templates
When creating a security group, you can use the two security group templates provided by Tencent Cloud.
- Template that opens all ports: all inbound and outbound traffic will be allowed to pass.
- Template that opens major ports: port TCP 22 (for Linux SSH login), ports 80 and 443 (for Web service), port 3389 (for Windows remote login), ICMP protocol (for Ping commands), and private network will be open to traffic.

>
If these templates cannot meet your actual needs, you can create custom security groups. For details, see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/213/34271) and [Security group use cases](https://intl.cloud.tencent.com/document/product/213/32369).
> - If you need to protect the application layer (HTTP/HTTPS), you can purchase [Tencent Cloud Web Application Firewall (WAF)](https://intl.cloud.tencent.com/product/waf). It defends web security at the application layer against web vulnerabilities, malicious crawlers, and CC attacks, helping protect your websites and web applications.


## Use Limits

For use limits and quotas of security groups, see security group limits in [Use Limits Overview] (https://intl.cloud.tencent.com/document/product/213/15379).

## Directions
The process to use the security group is shown in the following figure:

![](https://main.qcloudimg.com/raw/fbd5b2ec62e94f2cfee45d8b125f3e82.png)
