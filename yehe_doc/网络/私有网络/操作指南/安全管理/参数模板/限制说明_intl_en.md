### Use Limits
- Formats supported by the IP address template are as follows:
 - A single IP address, for example, `10.0.0.1`;
 - Consecutive IP addresses, for example, `10.0.0.1` - `10.0.0.100`;
 - An IP range, for example, `10.0.1.0/24`.
- Formats supported by the port template are as follows:
 - A single port, for example, `TCP:80`;
 - Multiple discrete ports, for example, `TCP:80,443`;
 - Consecutive ports, for example, `TCP:3306-20000`;
 - All ports, for example, `TCP:ALL`.

### Quota Limits
<table>
<thead>
<tr>
<th>Instance</th>
<th>Limit (Qty)</th>
</tr>
</thead>
<tbody><tr>
<td>IP address object (ipm)</td>
<td>Max 1,000/tenant</td>
</tr>
<tr>
<td>IP address group object (ipmg)</td>
<td>Max 1,000/tenant</td>
</tr>
<tr>
<td>Protocol port object (ppm)</td>
<td>Max 1,000/tenant</td>
</tr>
<tr>
<td>Protocol port group object (ppmg)</td>
<td>Max 1,000/tenant</td>
</tr>
<tr>
<td>IP address members in an IP address object (ipm)</td>
<td>Max 20/tenant</td>
</tr>
<tr>
<td>IP address object members (ipm) in an IP address group object (ipmg)</td>
<td>Max 20/tenant</td>
</tr>
<tr>
<td>Protocol port members in a protocol port group object (ppm)</td>
<td>Max 20/tenant</td>
</tr>
<tr>
<td>Protocol port object members (ppm) in a protocol port group object (ppmg)</td>
<td>Max 20/tenant</td>
</tr>
<tr>
<td>IP address group objects (ipmg) that can import IP address objects (ipm)</td>
<td>Max 50/tenant</td>
</tr>
<tr>
<td>Protocol port group objects (ppmg) that can import protocol port objects (ppm)</td>
<td>Max 50/tenant</td>
</tr>
</tbody></table>

>? Parameter templates can be imported by security groups. After importing parameter template features, security groups will convert the IP addresses and ports in the parameter template into multiple security group rules. Note that the total number of rules in each security group after the conversion cannot exceed 2,000.

