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
<th>Upper Limit</th>
</tr>
</thead>
<tbody><tr>
<td>IP address objects (ipm)</td>
<td>1,000 per tenant</td>
</tr>
<tr>
<td>IP address group objects (ipmg)</td>
<td>1,000 per tenant</td>
</tr>
<tr>
<td>Protocol port objects (ppm)</td>
<td>1,000 per tenant</td>
</tr>
<tr>
<td>Protocol port group objects (ppmg)</td>
<td>1,000 per tenant</td>
</tr>
<tr>
<td>IP address members in an IP address object (ipm)</td>
<td>20 per tenant</td>
</tr>
<tr>
<td>IP address object members (ipm) in an IP address group object (ipmg)</td>
<td>20 per tenant</td>
</tr>
<tr>
<td>Protocol port members in a protocol port group object (ppm) </td>
<td>20 per tenant</td>
</tr>
<tr>
<td>Protocol port object members (ppm) in a protocol port group object (ppmg)</td>
<td>20 per tenant</td>
</tr>
<tr>
<td>IP address group objects (ipmg) that can reference the same IP address object (ipm)</td>
<td>50 per tenant</td>
</tr>
<tr>
<td>Protocol port group objects (ppmg) that can reference the same protocol port object (ppm)</td>
<td>50 per tenant</td>
</tr>
</tbody></table>

>?If the parameter template is referenced by a security group, the IPs and ports in the template will be converted to multiple security group rules (up to 2000).

