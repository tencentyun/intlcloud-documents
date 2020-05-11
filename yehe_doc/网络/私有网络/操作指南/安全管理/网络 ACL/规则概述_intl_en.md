The network Access Control List (ACL) is an optional security layer that throttles traffic to and from subnets accurate to protocol and port.
![](https://main.qcloudimg.com/raw/f8490b4c94db7cd50f2cbe29524d237d.jpg)

## Use Cases
You can associate a network ACL with multiple subnets to maintain the same traffic and precisely control their inflow and outflow by setting inbound and outbound rules.
For example, when you host a multi-layer web application in a Tencent Cloud VPC instance and create different subnets for web-layer, logic-layer, and data-layer services, you can use a network ACL to ensure that the web-layer and data-layer subnets cannot access each other, but only the logic-layer subnet can access the web-layer and data-layer subnets.

## ACL Rules
After you add or delete a rule in a network ACL, the network traffic throttling of the associated subnets automatically changes.
A network ACL rule consists of:
- Protocol type: indicates protocol types that an ACL rule accepts or rejects, for example, TCP and UDP.
- Port: indicates the source port of traffic, which can be a single port or a port segment, for example, port 80 or ports 90 to 100.
- Source IP address: indicates the source IP address or IP range of traffic with the format of IP or CIDR, for example, `10.20.3.0` or `10.0.0.2/24`.
- Policy: indicates whether to permit or reject the traffic.

### Default rules
Once created, every network ACL has two default rules that cannot be modified or deleted, with the lowest priority.
- Default rule for inbound traffic
<table>
<thead>
<tr>
<th>Protocol Type</th>
<th>Port</th>
<th>Source IP Address</th>
<th>Policy</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>All</td>
<td>All</td>
<td>0.0.0.0/0</td>
<td>Reject</td>
<td>Rejects all inbound traffic.</td>
</tr>
</tbody></table>

- Default rule for outbound traffic
<table>
<thead>
<tr>
<th>Protocol Type</th>
<th>Port</th>
<th>Source IP Address</th>
<th>Policy</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>All</td>
<td>All</td>
<td>0.0.0.0/0</td>
<td>Reject</td>
<td>Rejects all outbound traffic.</td>
</tr>
</tbody></table>

### Rule priorities
- The priorities of network ACL rules are expressed by their positions in the list. The rule at the top of the list has the highest priority and is applied first. The rule at the bottom of the list has the lowest priority.
- In case of a conflict, the rule with a higher priority prevails by default.
- When traffic flows in or out a subnet that is associated with a network ACL, the system matches rules in the network ACL from top down. If a rule is hit, the system no longer matches subsequent rules and accepts the access.

#### Application example
To allow all source IP addresses to access all ports of CVMs in a subnet associated with a network ACL and reject HTTP source IP address of `192.168.200.11/24` to access port 80, add the following two network ACL rules for inbound traffic:

| Protocol Type | Port | Source IP Address | Policy | Description |
| --- | --- | --- | --- |---|
| HTTP | 80 | 192.168.200.11/24 | Reject | Rejects this IP address of HTTP services to access port 80.|
| All | All | 0.0.0.0/0 | Allow | Allows all source IP addresses to access all ports. |


## Security Groups vs. Network ACLs
<table>
<thead>
<tr>
th width="12%">Item</th>
<th width="45%">Security Group</th>
<th width="43%">Network ACL</th>
</tr>
</thead>
<tbody><tr>
<td>Traffic throttling</td>
<td>Traffic throttling at the instance level, such as CVM and database traffic throttling</td>
<td>Traffic throttling at the subnet level</td>
</tr>
<tr>
<td>Rule</td>
<td>Allow and reject rules</td>
<td>Allow and reject rules</td>
</tr>
<tr>
<td>Stateful or stateless</td>
<td>Stateful: returned traffic is automatically permitted without being subjected to any rules.</td>
<td>Stateless: returned traffic must be explicitly permitted by rules.</td>
</tr>
<tr>
<td>Effective time</td>
<td>Rules are applied to an instance, such as a CVM or cloud database, only if you specify a security group when creating the instance or associate a security group with an existing instance.</td>
<td>The ACL rules are automatically applied to all instances, such as CVMs and cloud databases in the associated subnet.</td>
</tr>
<tr>
<td>Rule priority</td>
<td>In case of a conflict, the rule with a higher priority prevails by default.</td>
<td>In case of a conflict, the rule with a higher priority prevails by default.</td>
</tr>
</tbody></table>

