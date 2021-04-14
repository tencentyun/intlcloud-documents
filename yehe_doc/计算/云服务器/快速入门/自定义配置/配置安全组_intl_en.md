This document uses security group creation as an example to describe how to configure security groups for the first time based on security group rules provided by Tencent Cloud when you customize instances. For other security-group-related operations, see the **Security Group** page in the CVM console. For more details on security groups, see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).


## Configuring Security Groups
1. Select **Create Security Group**, as shown in the following figure.
>? If you already have available security groups, you can select **Existing Security Groups**.
>
![](https://main.qcloudimg.com/raw/7bafed15a25c7fbfdb60d09069ea3d0b.png)
2. Select IP addresses or ports to be opened based on your actual requirements.
Rules for a new security group are as follows:<ul>
<li><b>ICMP</b>: enable ICMP and allow the public network to ping the server.</li>
<li><b>TCP:80</b>: open port 80 and allow web service access through HTTP.</li></li>
<li><b>TCP:22</b>: open port 22 and allow SSH remote connection to the Linux CVM.</li>
<li><b>TCP:443</b>: open port 443 and allow web service access through HTTPS.</li>
<li><b>TCP:3389</b>: open port 3389 and allow RDP connection to the Windows CVM.</li>
<li><b>Private network</b>: open the private network and allow intercommunication (IPv4-based) between different cloud resources through the private network.</li></ul>

>?
> - After you select the IP addresses or ports to be opened, the detailed inbound and outbound rules appear on the **Security Group Rule** tab page.
> - To open other ports for your business, refer to <a href="https://intl.cloud.tencent.com/document/product/213/32369">security group use cases</a> to <a href="https://intl.cloud.tencent.com/document/product/213/34271">create security groups</a>. For security purposes, Tencent Cloud recommends that you only open required ports to prevent potential security risks.

3. Configure other information as prompted.

## Security Group Rules

**Inbound rule**: allows traffic to CVMs associated with a security group.
**Outbound rule**: indicates outbound traffic from the CVMs.

- Rules in a security group are **prioritized from the top down**.
- When a CVM is bound to a security group without rules, all inbound and outbound traffic is rejected by default. If a rule is available, the rule prevails.
- When a CVM is bound to multiple security groups, the security groups **with smaller numbers have higher priority**.
- When a CVM is bound to multiple security groups, the rejection rule takes effect for the security group with the lowest priority by default.

## Security Group Restrictions

For details, see [Use Limits](https://intl.cloud.tencent.com/document/product/213/15379).
