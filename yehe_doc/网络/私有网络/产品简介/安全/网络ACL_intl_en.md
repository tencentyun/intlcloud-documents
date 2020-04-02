The network access control list (ACL) is an optional security layer at the subnet level for controlling the inbound and outbound traffic of subnets, with an accuracy up to protocol and port granularity.
![](https://main.qcloudimg.com/raw/5418cbe507ad725e7073c0bbbe1bb9dc.png)

## Use Cases
You can associate a network ACL with multiple subnets for the same network traffic control. By setting the outbound and inbound rules, you can precisely control the inbound and outbound traffic of subnets.
For example, when multiple layers of web applications are hosted in Tencent Cloud VPC instances, and web-layer, logic-layer, and data-layer services are deployed in different subnets, you can control the access among the three subnets through the network ACL. As a result, the web-layer subnet and the data-layer subnet cannot access each other, and only the logic layer can access the web-layer and data-layer subnets.

## ACL Rules
When you add or delete rules in the network ACL, the change is automatically applied to the network traffic control of associated subnets.
A network ACL rule consists of the following parts:
- Protocol type: select the protocol types to be allowed or rejected by the ACL rule, such as TCP and UDP.
- Port: the source port of the traffic. It can be a single port or port range, for example port 80 or ports 90–100.
- Source IP: the source IP address or source IP range of the traffic. It can be an IP address or CIDR block, for example, `10.20.3.0` or `10.0.0.2/24`.
- Policy: allow or reject.

### Default rules
After creation, each network ACL contains two default rules. Default rules cannot be modified or deleted and have the lowest priority.
- Default inbound rule
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
<td>Reject all inbound traffic</td>
</tr>
</tbody></table>

- Default outbound rule
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
<td>Reject all outbound traffic</td>
</tr>
</tbody></table>

### Priorities of rules
- The priorities of network ACL rules are indicated by their positions in the list. The rule at the top of the list has highest priority and is the first to be applied. The rule at the bottom has the lowest priority.
- In case of rule conflict, the rule that ranks higher in the list prevails by default.
- When traffic enters or exits from a subnet associated with the network ACL, the system performs rule matching on the rules in the network ACL list one by one from the top to the bottom of the list. If a certain rule is hit, the traffic is permitted, and the system no longer matches it with subsequent rules.

#### Application examples
Example: to allow all source IP addresses to access all ports of CVMs in the subnet associated with the ACL and to reject the access request of the HTTP service whose server source IP address is `192.168.200.11/24` for accessing port 80, you can add these two network ACL inbound rules:

| Protocol Type | Port | Source IP Address | Policy | Notes |
| --- | --- | --- | --- |---|
| HTTP | 80 |192.168.200.11/24 | Reject | Reject the access request of the HTTP service of that IP address for accessing port 80. |
| All | All | 0.0.0.0/0 | Allow | Allow all source IP addresses to access all ports. |


## Comparison Between Security Groups and Network ACLs
<table>
<thead>
<tr>
<th width="60%">Comparison Item</th>
<th width="45%">Security Group</th>
<th width="43%">Network ACL</th>
</tr>
</thead>
<tbody><tr>
<td>Traffic control</td>
<td>Traffic control at the instance level, such as CVMs and databases</td>
<td>Traffic control at the subnet level</td>
</tr>
<tr>
<td>Rule</td>
<td>Allow and reject rules are supported.</td>
<td>Allow and reject rules are supported.</td>
</tr>
<tr>
<td>Stateful/Stateless</td>
<td>Stateful: returned traffic is automatically permitted without being subjected to any rules.</td>
<td>Stateless: returned traffic must be explicitly allowed by rules.</td>
</tr>
<tr>
<td>Effective time</td>
<td>Rules will be applied to an instance such as a CVM or a cloud database only if you specify a security group during the creation of the instance or associate the instance with a security group after creation.</td>
<td>After you create an ACL and bind it with a subnet, the ACL will be automatically applied to all instances such as CVMs and cloud databases within the subnet.</td>
</tr>
<tr>
<td>Rule priority</td>
<td>In case of rule conflict, the rule that ranks higher in the list prevails by default.</td>
<td>In case of rule conflict, the rule that ranks higher in the list prevails by default.</td>
</tr>
</tbody></table>

