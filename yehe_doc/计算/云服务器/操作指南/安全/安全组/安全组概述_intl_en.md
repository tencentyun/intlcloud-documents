A security group is a virtual firewall that features stateful data packet filtering. It is used to configure the network access control of CVM, Cloud Load Balancer, TencentDB, and other instances while controlling their outbound and inbound traffic. It is an important means of network security isolation.
You can configure security group rules to allow or reject inbound traffic and outbound traffic of instances within the security group.

## Security Group Features
- A security group is a logical group. You can add CVM, ENI, TencentDB, and other instances in the same region with the same network security isolation requirements to the same security group.
- By default, instances in the same security group are not interconnected, unless you allow them by specifying rules.
- Security groups are stateful. Inbound traffic you have allowed can automatically go outward and vice versa.
- You can modify security group rules at any time, and the new rule takes effect immediately.

## Use Limits

For use limits and quotas of security groups, see security group limits in [Use Limits Overview](https://intl.cloud.tencent.com/document/product/213/15379).

## Security Group Rules
### Components
A security group rule consists of:
- Source: IP address of the source data (inbound) or target data (outbound).
- Protocol type and protocol port: protocol type can be TCP, UDP, HTTP, etc.
- Policy: allow or reject the access request.

### Rule Priorities
- The rules in a security group are prioritized from top to bottom. The rule at the top of the list has the highest priority and first take effect, while the rule at the bottom has the lowest priority.
- In case of rule conflict, the rule with a higher priority prevails.
- When traffic goes in or out an instance that is bound to a security group, the security group rules will be matched sequentially from top to bottom. If a rule is matched successfully and takes effect, the subsequent rules will be ignored.

### Multiple Security Groups
An instance can be bound with one or multiple security groups. When it is bound with multiple security groups, the security group rules will be matched sequentially from top to bottom. You can adjust security group priorities at any time.

## Security Group Templates
When creating a security group, you can use either of the two security group templates provided by Tencent Cloud.
- Template that opens all ports: all inbound and outbound traffic will be allowed to pass.
- Template that opens major ports: port TCP 22 (for Linux SSH login), ports 80 and 443 (for Web service), port 3389 (for Windows remote login), ICMP protocol (for Ping commands), and private network will be open to Internet.

>
>- If these templates cannot meet your actual needs, you can create custom security groups. For more information, see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/213/34271) and [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).
>- If you need to protect the application layer (HTTP/HTTPS), you can purchase a [Tencent Cloud Web Application Firewall (WAF)](https://intl.cloud.tencent.com/product/waf). It defends web security at the application layer against web vulnerabilities, malicious crawlers, and CC attacks, helping protect your websites and web applications.
>

## Directions
The following figure shows how to use a security group:
![](https://main.qcloudimg.com/raw/fbd5b2ec62e94f2cfee45d8b125f3e82.png)