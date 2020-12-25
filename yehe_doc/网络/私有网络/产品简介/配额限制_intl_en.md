### VPCs and subnets
<table>
<thead>
<tr>
<th width="70%">Resource</th>
<th width="30%">Upper Limit</th>
</tr>
</thead>
<tbody><tr>
<td>Number of VPC instances per region for each account</td>
<td align="center">20</td>
</tr>
<tr>
<td>Number of subnets per VPC</td>
<td align="center">100</td>
</tr>
<tr>
<td>Number of secondary CIDR blocks per VPC</td>
<td align="center">5</td>
</tr>
<tr>
<td>Number of classic network CVMs can be associated with each VPC instance</td>
<td align="center">100</td>
</tr>
</tbody></table>

### Route tables
<table>
<thead>
<tr>
<th width="70%">Resource</th>
<th width="30%">Upper Limit</th>
</tr>
</thead>
<tbody><tr>
<td>Number of route tables per VPC </td>
<td align="center">10</td>
</tr>
<tr>
<td>Number of route tables associated with each subnet</td>
<td align="center">1</td>
</tr>
<tr>
<td>Number of routing policies per route table</td>
<td align="center">50</td>
</tr>
</tbody></table>

### ENIs
<table>
<tr>
<th width="70%">Resource</th>
<th width="30%">Upper Limit</th>
</tr>
<tr>
<td>Number of secondary ENIs per VPC</td>
<td>1000</td>
</tr>
</table>

### Security groups
<table>
<tr><th width="70%">Description</th><th width="30%">Limit</th></tr>
<tr><td>Number of security groups</td><td>50 per region</td></tr>
<tr><td>Number of rules in a security group</td><td>100 for inbound rules and 100 for outbound rules</td></tr>
<tr><td>Number of CVM instances associated with a security group</td><td>2,000</td></tr>
<tr><td>Number of security groups associated with a CVM instance</td><td>5</td></tr>
<tr><td>Number of rules in each security group that reference the security group ID</td><td>10</td></tr>
</table>

### Network ACL
<table >
<thead>
<tr>
<th width="70%">Resource</th>
<th width="30%">Limit</th>
</tr>
</thead>
<tbody><tr>
<td>Number of network ACLs per VPC</td>
<td>50</td>
</tr>
<tr>
<td>Number of rules per network ACL</td>
<td>Inbound rules: 20<br>Outbound rules: 20</td>
</tr>
<tr>
<td>Number of network ACLs associated with a subnet</td>
<td>1</td>
</tr>
</tbody></table>

### Parameter template
<table>
<thead>
<tr>
<th width="70%">Instance</th>
<th width="30%">Quota per Tenant</th>
</tr>
</thead>
<tbody><tr>
<td>IP address objects (ipm)</td>
<td>Max.: 1,000</td>
</tr>
<tr>
<td>IP address group objects (ipmg)</td>
<td>Max.: 1,000</td>
</tr>
<tr>
<td>Protocol port objects (ppm)</td>
<td>Max.: 1,000</td>
</tr>
<tr>
<td>Protocol port group objects (ppmg)</td>
<td>Max.: 1,000</td>
</tr>
<tr>
<td>IP address members in an IP address object (ipm)</td>
<td>Max.: 20</td>
</tr>
<tr>
<td>IP address object members (ipm) in an IP address group object (ipmg)</td>
<td>Max.: 20</td>
</tr>
<tr>
<td>Protocol port members in a protocol port group object (ppm) </td>
<td>Max.: 20</td>
</tr>
<tr>
<td>Protocol port object members (ppm) in a protocol port group object (ppmg)</td>
<td>Max.: 20</td>
</tr>
<tr>
<td>IP address group objects (ipmg) that can reference the same IP address object (ipm)</td>
<td>Max.: 50</td>
</tr>
<tr>
<td>Protocol port group objects (ppmg) that can reference the same protocol port object (ppm)</td>
<td>Max.: 50</td>
</tr>
</tbody></table>

### Network probe 
<table >
<thead>
<tr>
<th width="70%">Resource</th>
<th width="30%">Upper Limit</th>
</tr>
</thead>
<tbody><tr>
<td>Number of network probes per VPC</td>
<td>50</td>
</tr>
</tbody></table>
