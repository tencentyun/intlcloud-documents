### Use Limits
- The occupation of an HAVIP can be declared by the backend CVM, but you cannot manually bind HAVIPs to a specified server in the console (the experience is consistent with that of a traditional physical machine.)
- The backend RS but not the HAVIP determines whether to migrate based on the configuration file negotiation.
- Only VPC instances are supported, and the basic network is not supported.
- Heartbeat detection must be done by an application on the CVM, but not by the HAVIP, which serves only as a floating IP address declared by ARP (the experience is consistent with that of a traditional physical machine.)

### Quota Limits
<table style="width:450px !important">
<thead>
<tr>
<th width="70%">Resource</th>
<th>Limit</th>
</tr>
</thead>
<tbody><tr>
<td>Default HAVIP quota in each VPC</td>
<td>10</td>
</tr>
</tbody></table>
