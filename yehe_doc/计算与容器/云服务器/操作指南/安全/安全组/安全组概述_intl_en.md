A security group is a virtual firewall that features stateful data packet filtering. It is used to configure the network access control of CVM, Cloud Load Balancer, TencentDB, and other instances while controlling their outbound and inbound traffic. It is an important means of network security isolation.
You can configure security group rules to allow or reject inbound and outbound traffic of instances within the security group.

## Security Group Features
- A security group is a logical group. You can add CVM, ENI, TencentDB, and other instances in the same region with the same network security isolation requirements to the same security group.
- By default, instances in the same security group are not interconnected, unless you allow them by specifying rules.
- Security groups are stateful. Inbound traffic you have allowed can automatically become outbound and vice versa.
- You can modify security group rules at any time, and the new rules will take effect immediately.

## Use Limits

For more information on the use limits and the quotas of security groups, please see **security group limits** in [Use Limits Overview](https://intl.cloud.tencent.com/document/product/213/15379).

## Security Group Rules
### Components
A security group rule consists of:
- Source: IP address of the source data (inbound) or target data (outbound).
- Protocol type and protocol port: the protocol type, such as TCP, UDP, etc.
- Policy: allow or reject the access request.

### Rule priorities
- The rules in a security group are prioritized from top to bottom. The rule at the top of the list has the highest priority and will take effect first, while the rule at the bottom has the lowest priority and will take effect last.
- If there is a rule conflict, the rule with the higher priority will prevail by default.
- When traffic goes in or out of an instance that is bound to a security group, the security group rules will be matched sequentially from top to bottom. If a rule is matched successfully and takes effect, the subsequent rules will not be matched.

### Multiple security groups
An instance can be bound to one or multiple security groups. When it is bound to multiple security groups, the security group rules will be matched sequentially from top to bottom. You can adjust the priorities of security groups at any time.

## Security Group Templates
When creating a security group, you can select one of the two security group templates provided by Tencent Cloud:
- The template that opens all ports: all inbound and outbound traffic will be allowed to pass.
- The template that opens major ports: port TCP 22 (for Linux SSH login), ports 80 and 443 (for Web service), port 3389 (for Windows remote login), the ICMP protocol (for Ping commands), and the private network will be open to the Internet.

>?
>- If these templates cannot meet your actual needs, you can create custom security groups. For more information, see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/213/34271) and [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).
>- If you need to protect the application layer (HTTP/HTTPS), please activate [Tencent Cloud Web Application Firewall (WAF)](https://intl.cloud.tencent.com/product/waf), which provides web security at the application layer to defend against web vulnerabilities, malicious crawlers, and CC attacks, helping protect your websites and web applications.
>

## How to Use a Security Group
The following figure shows you how to use a security group:
![](https://main.qcloudimg.com/raw/fbd5b2ec62e94f2cfee45d8b125f3e82.png)

## Security Group Best Practices

### Creating a security group
- We recommend that you specify a security group while you’re purchasing a CVM via the API. Otherwise, the default security group will be used and cannot be deleted.
- If you need to change the instance protection policy, we recommend modifying the existing rules rather than creating a new security group.

### Managing rules
- Export and back up the security group rules before you modify them, so you can import and restore them if an error occurs.
- To create multiple security group rules, please use the [parameter template](https://intl.cloud.tencent.com/document/product/215/31867).

### Associating a security group
- You can add instances with the same protection requirements to the same security group, instead of configuring a separate security group for each instance.
- It’s not recommended to bind one instance to too many security groups, because rules in different security groups may conflict and result in network disconnection.

