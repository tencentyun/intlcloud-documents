## Overview
Security groups are used to manage traffic to and from public and private networks. For the sake of security, most inbound traffic is denied by default. If you selected **Open all ports** or **Open ports 22, 80, 443, 3389 and ICMP protocol** as the template when creating a security group, rules are automatically created and added to the security group to allow traffic on those ports. For more information, please see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

This document describes how to add security group rules to allow or reject traffic to and from public or private networks.

## Notes

- Security group rules support IPv4 and IPv6 rules.
- **Open all ports** allows both IPv4 and IPv6 traffic.

## Prerequisites
- You should have an existing security group. If you do not, refer to [Creating a Security Group](https://intl.cloud.tencent.com/document/product/213/34271) for details.
- You should know which traffic is allowed or rejected for your CVM instance. For more information on security group rules and their use cases, please see [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).

### Directions
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. Select [**Security Group**](https://console.cloud.tencent.com/cvm/securitygroup) on the left sidebar to access the security group management page.
3. Select a region, and locate the security group for which you want to set rules.
4. Click **Modify Rules** in the **Operation** column.
5. <span id="step05">Click **Inbound rules** and choose either of the following methods to add rules.</span>
![](https://main.qcloudimg.com/raw/e4c1f93fe75de51aa8de068da60a2206.png)
>? The following instructions use **Add a Rule** as an example.
>
 - **Open all ports**: this method is ideal if you do not need custom ICMP rules and all traffic goes through ports 20, 21, 22, 80, 443, and 3389 and the ICMP protocol.
 - **Add a Rule**: this method is ideal if you need to use multiple protocols and ports other than those mentioned above.
6. In the pop-up window, set rules.
![](https://main.qcloudimg.com/raw/0114aa46ffabc46dd9d6921095f6e8fa.png)
Configure the following parameters:
 - **Type**: **Custom** is selected by default. You can also choose another system rule template including **Login Windows CVMs (3389)**, **Login Linux CVMs (22)**, **Ping**, **HTTP (80)**, **HTTPS (443)**, **MySQL (3306)**, and **SQL Server (1433)**.
 - **Source** or **Destination**: traffic source (inbound rules) or destination (outbound rules). You need to specify one of the following options:
<table>
	<tr><th>Source or Destination</th><th>Description</th></tr>
	<tr><td>A single IPv4 address or an IPv4 range</td><td>In CIDR notation, such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code> or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses will be matched.</td></tr>
	<tr><td>A single IPv6 address or an IPv6 range</td><td>In CIDR notation, such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicates all IPv6 addresses will be matched.</td></tr>
	<tr><td>ID of the referenced security group. You can reference the ID of:<ul  style="margin: 0;"><li>Current security group</li><li>Other security group</li></ul>
</td><td><ul  style="margin: 0;"><li>To reference the current security group, please enter the ID of security group associated with the CVM.</li><li>You can also reference another security group in the same region and belongs to the same project by entering the security group ID.</li></ul>
<blockquote class="d-mod-explain"><div class="d-mod-title d-explain-title"><i class="d-icon-explain"></i>Notes:</div>
<p></p><ul>
<li>The referenced security group is available to you as an advanced feature. The rules of the referenced security group are not added to the current security group.</li>
<li>If you enter the security group ID in Source/Destination when configuring security group rules, the private IP addresses of the CVM instances and the ENIs that are associated with this security group ID are used as the source/destination. This does not include public IP addresses.</li>
</ul>
</blockquote>
</td></tr>
	<tr><td>Reference an IP address object or IP address group object in a <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td><td>-</td></tr>
</table>
 - **Protocol port**: enter the protocol type and port range or reference a protocol/port or protocol/port group in a [parameter template](https://intl.cloud.tencent.com/document/product/215/31867). The supported protocol type includes TCP, UDP, ICMP, ICMPv6 and GRE in the following formats.
    - Single port: such as `TCP:80`.
    - Multiple ports: such as `TCP:80,443`.
    - Port range: such as `TCP:3306-20000`.
    - All ports: such as `TCP:ALL`.
 - **Policy**: **Allow** or **Refuse**. **Allow** is selected by default.
    - Allow: traffic to this port is allowed.
    - Refuse: data packets will be discarded without any response.
 - **Notes**: a short description of the rule for easier management.
7. <span id="step07">Click **Complete** to finish adding the rule.</span>
8. To add an outbound rule, click **Outbound rule** and refer to [Step 5](#step05) to [Step 7](#step07).
