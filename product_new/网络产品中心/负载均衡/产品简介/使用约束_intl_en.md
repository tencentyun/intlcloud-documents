The use of Tencent Cloud CLB has certain restrictions, and different types of CLB instances have their own use limits. For more information on CLB instance types, please see [Instance Types](https://intl.cloud.tencent.com/document/product/214/8847).
<table>
<tbody>
<tr><th>Instance Type</th><th>Resource</th><th>Default Restriction</th></tr>
<tr>
  <td  rowspan="4">General restrictions for all instances</td>
  <td>Number of public network instances can be created under one account in a single region</td><td>100</td>
</tr>
<tr>
  <td>Number of private network instances can be created under one account in a single region</td><td>100</td>
</tr>
<tr>
  <td>Number of listeners can be added to an instance</td><td>50</td>
</tr>
<tr>
  <td>Ports that can be selected by a listener in an instance</td><td>An integer between 1 - 65535</td>
</tr>

<tr>
  <td  rowspan="3">CLB<br>(formerly "application CLB")</td>
  <td>Number of domain name and URL forwarding rules can be configured for an HTTP/HTTPS listener in a CLB instance</td><td>50</td>
</tr>
<tr>
  <td>Number of servers can be bound to a forwarding rule in a CLB instance</td><td>100</td>
</tr>
<tr>
  <td>Number of backend ports that can correspond to a frontend port of a CLB instance</td><td>Multiple ports</td>
</tr>

<tr>
  <td rowspan="2">Classic CLB</td>
  <td>Number of servers can be bound to a listener in a classic CLB instance</td><td>100</td>
</tr>  
<tr>
  <td>Number of backend ports that can correspond to a frontend port of a classic CLB instance</td><td>1 port</td>
</tr>
</tbody>
</table>

A CLB instance **will not unbind itself** from the CVM instance. After a CVM instance becomes isolated (pay-as-you-go CVM instance has been in arrears for more than 2 hours), it **will not unbind itself** from the CLB instance either.
