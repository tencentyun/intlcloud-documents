This document describes the use limits of CLB.

## General Restrictions
The use of Tencent Cloud CLB has certain restrictions, and different types of CLB instances have their own use limits. For more information on CLB instance types, see [Instance Types](https://intl.cloud.tencent.com/document/product/214/8847).
<table>
<tbody>
<tr><th>Instance Type</th><th>Resource</th><th>Default Restriction</th></tr>
<tr>
  <td  rowspan="4">General restrictions for all instances</td>
  <td>Number of public network CLB instances that can be created in a single region</td><td><ul><li>100 general IP-based instances</li><li>3 static IP-based instances under one individual account or 15 under one organizational account.</li></ul></td>
</tr>
<tr>
  <td>Number of private network instances that can be created under one account in a single region</td><td>100</td>
</tr>
<tr>
  <td>Number of listeners that can be added to an instance</td><td>50</td>
</tr>
<tr>
  <td>Ports that can be selected by a listener in an instance</td><td>An integer between 1 and 65535</td>
</tr>
<tr>
  <td  rowspan="3">CLB<br>(formerly "application CLB")</td>
  <td>Number of domain name and URL forwarding rules that can be configured for an HTTP/HTTPS listener in a CLB instance</td><td>50</td>
</tr>
<tr>
  <td>Number of servers that can be bound to a forwarding rule in a CLB instance</td><td>100</td>
</tr>
<tr>
  <td>Number of backend ports that can correspond to a frontend port of a CLB instance</td><td>Multiple ports</td>
</tr>
<tr>
  <td rowspan="2">Classic CLB</td>
  <td>Number of servers that can be bound to a listener in a classic CLB instance</td><td>100</td>
</tr>  
<tr>
  <td>Number of backend ports that can correspond to a frontend port of a classic CLB instance</td><td>1 port</td>
</tr>
</tbody>
</table>

A CLB instance **will not unbind itself** from the CVM instance. After a CVM instance becomes isolated (pay-as-you-go CVM instance has been in arrears for more than 2 hours), it **will not unbind itself** from the CLB instance either.


## Peak Bandwidth
The meaning of peak bandwidth varies by network billing modes as detailed below:
<table>
       <tbody><tr>
			 <th width="17%">Billing Mode</th>
			 <th>Difference</th>
			 <th>Description</th>
       </tr>
       <tr>          
            <td>Billed by fixed bandwidth<br/>(including hourly bandwidth subscription and monthly bandwidth)</td>
            <td>This peak bandwidth is the committed bandwidth, and is guaranteed in case of bandwidth competition.</td>
						<td>The sum of peak bandwidth of all the running instances that are billed at a fixed bandwidth (including hourly-subscribed bandwidth and monthly-subscribed bandwidth) cannot exceed 50 Gbps in one region. If you require a higher bandwidth, contact your sales rep.

</td> 
            </tr> 
						<tr>
			 <td>Bill-by-traffic</td>
			 <td  rowspan="2">The peak bandwidth is only regarded as the <strong>maximum peak bandwidth</strong>, and not as the committed bandwidth. When bandwidth resources are contested, the peak bandwidth may be limited.</td> 
			 <td>The sum of peak bandwidth of all the running bill-by-traffic instances cannot exceed 5 Gbps in one region. If your application requires a guaranteed or higher bandwidth, choose bill-by-bandwidth.</td> 
			 </tr>
			 <tr>          
            <td>Bandwidth packages</td>
						<td>The sum of peak bandwidth of all the running instances that are billed by shared bandwidth package cannot exceed 50 Gbps in one region. If you require a higher bandwidth, contact your sales rep.

</td> 
            </tr> 
</tbody></table>
