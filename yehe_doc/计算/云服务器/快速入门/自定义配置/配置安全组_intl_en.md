This document describes how to create and configure a security group for an instance. For more information, please see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).


## Configuring a Security Group
1. Select **New security group**.
> If you have available security groups, you can select **Existing Security Groups**.
>
![](https://main.qcloudimg.com/raw/c08ca9a0262f4911fdac90925762e4a6.png)
2. Select IP addresses or ports to open based on your actual requirements.
Rules for a new security group are as follows:<ul>
<li><b>ICMP</b>: opens to the ICMP protocol and allows the pinging of the server over the public network.</li>
<li><b>TCP:80</b>: opens port 80 and allows access to Web services over HTTP.</li></li>
<li><b>TCP:22</b>: opens port 22 and allows a remote connection to Linux CVMs over SSH.</li>
<li><b>TCP:443</b>: opens port 443 and allows access to Web services over HTTPS.</li>
<li><b>TCP:3389</b>: opens port 3389 and allows a remote connection to Windows CVMs over RDP.</li>
<li><b>Private network</b>: opens to the private network and allows private network access among different cloud resources (IPv4).</li></ul>
<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Note:
</div>
<ul><li> After you select the IP addresses or ports to be opened, the detailed inbound and outbound rules appear on the <b>Security Group Rule</b> tab page.</li><li>To open other ports for your business, refer to <a href="https://intl.cloud.tencent.com/document/product/213/32369">Security Group Use Cases</a> to <a href="https://intl.cloud.tencent.com/document/product/213/34271">create security groups</a>. For security reasons, we recommend that you only open ports when absolutely necessary to avoid unnecessary security risks.
</li></ul>
</blockquote>
3. Configure other information as prompted.

## Security Group Rules

**Inbound rules**: allows traffic to CVMs associated with a security group.
**Outbound rules**: indicates outbound traffic from the CVMs.

- Rules in a security group are **prioritized from top to bottom**.
- When a CVM is bound to a security group without rules, all inbound and outbound traffic is rejected by default. If a rule is available, the rule prevails.
- When a CVM is bound to multiple security groups, the security groups with **smaller numbers have higher priority**.
- When a CVM is bound to multiple security groups, the rejection rule takes effect for the security group with the lowest priority by default.

## Security Group Limits

For more information, please see [Security Group Limits](https://intl.cloud.tencent.com/document/product/213/15379).
