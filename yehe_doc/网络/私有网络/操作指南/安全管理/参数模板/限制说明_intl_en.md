### Use Limits
- Formats supported by the IP address template are as follows:
 - Single IP address: such as `10.0.0.1`;
 - Consecutive IP addresses: such as `10.0.0.1`-`10.0.0.100`;
 - IP range: such as `10.0.1.0/24`.
- Formats supported by the port template are as follows:
 - Single port: such as `TCP:80`;
 - Multiple ports: such as `TCP:80,443`;
 - Port range: such as `TCP:3306-20000`;
 - All ports: such as `TCP:ALL`.

### Quota Limits 
<table>
<thead>
<tr>
<th>Instance</th>
<th>Limit per Tenant</th>
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

>?If the parameter template is referenced to by a security group, the IP/port in the parameter template will be converted to a maximum of 2,000 security group rules.

