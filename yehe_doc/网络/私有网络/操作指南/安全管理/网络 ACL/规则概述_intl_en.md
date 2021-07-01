The network Access Control List (ACL) is an optional layer of security that throttles traffic to and from subnets accurate to protocol and port. This document describes how to configure network ACL rules for the access control.

## Overview
You can associate a network ACL with multiple subnets to maintain the same traffic and precisely control their inflow and outflow by setting inbound and outbound rules.
For example, when you host a multi-layer web application in a Tencent Cloud VPC instance and create different subnets for web-layer, logic-layer, and data-layer services, you can use a network ACL to ensure that the web-layer and data-layer subnets cannot access each other, but only the logic-layer subnet can access the web-layer and data-layer subnets.
![](https://main.qcloudimg.com/raw/f8490b4c94db7cd50f2cbe29524d237d.jpg)

## ACL Rules
After you add or delete a rule in a network ACL, the network traffic throttling of the associated subnets automatically changes.
A network ACL rule consists of:
- Protocol type: indicates protocol types that an ACL rule allows or denies, for example, TCP and UDP.
- Port: indicates the source port of traffic, which can be a single port or a port range, for example, port 80 or ports 90 to 100.
- Source IP: indicates the source IP address or IP range of traffic in the IP or CIDR block format, for example, `10.20.3.0` or `10.0.0.2/24`.
- Policy: indicates whether to allow or deny the access request.

### Default rules
Once created, every network ACL has two default rules that cannot be modified or deleted, with the lowest priority.
- Default inbound rule
<table>
<thead>
<tr>
<th>Protocol Type</th>
<th>Port</th>
<th>Source IP</th>
<th>Policy</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>ALL</td>
<td>All</td>
<td>0.0.0.0/0</td>
<td>Deny</td>
<td>Denies all inbound traffic.</td>
</tr>
</tbody></table>

- Default outbound rule
<table>
<thead>
<tr>
<th>Protocol Type</th>
<th>Port</th>
<th>Destination IP</th>
<th>Policy</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>All</td>
<td>All</td>
<td>0.0.0.0/0</td>
<td>Deny</td>
<td>Denies all outbound traffic.</td>
</tr>
</tbody></table>

### Rule priorities
- The rules of a network ACL are prioritized from top to bottom. The rule at the top of the list has the highest priority and will take effect first, while the rule at the bottom has the lowest priority and will take effect last.
- If there is a rule conflict, the rule with the higher priority will prevail by default.
- When traffic goes in or out of a subnet that is bound to a network ACL, the network ACL rules will be matched sequentially from top to bottom. If a rule is matched successfully and takes effect, the subsequent rules will not be matched.

#### Application example
To allow all source IP addresses to access all ports of CVMs in a subnet associated with a network ACL and deny HTTP source IP address of `192.168.200.11/24` to access port 80, add the following two network ACL rules for inbound traffic:

| Protocol Type | Port | Source IP | Policy | Description |
| --- | --- | --- | --- |---|
| HTTP | 80 | 192.168.200.11/24 | Deny | Denies this IP address of HTTP services to access port 80. |
| All | All | 0.0.0.0/0 | Allow | Allows all source IP addresses to access all ports. |


## Security Groups vs. Network ACLs
<table>
<thead>
<tr>
<th width="12%">Item</th>
<th width="45%">Security Group</th>
<th width="43%">Network ACL</th>
</tr>
</thead>
<tbody><tr>
<td>Traffic throttling</td>
<td>Traffic throttling at the instance level, such as CVM and database</td>
<td>Traffic throttling at the subnet level</td>
</tr>
<tr>
<td>Rule</td>
<td>Allow and reject rules</td>
<td>Allow and reject rules</td>
</tr>
<tr>
<td>Stateful or stateless</td>
<td>Stateful: returned traffic is automatically permitted without being subject to any rules.</td>
<td>Stateless: returned traffic must be explicitly permitted by rules.</td>
</tr>
<tr>
<td>Effective time</td>
<td>Rules are applied to an instance, such as a CVM or TencentDB, only if you specify a security group when creating the instance or associate a security group with the instance after it is created.</td>
<td>The ACL rules are automatically applied to all instances, such as CVM and TencentDB instances in the associated subnet.</td>
</tr>
<tr>
<td>Rule priority</td>
<td>If there is a rule conflict, the rule with the higher priority will prevail by default.</td>
<td>If there is a rule conflict, the rule with the higher priority will prevail by default.</td>
</tr>
</tbody></table>

