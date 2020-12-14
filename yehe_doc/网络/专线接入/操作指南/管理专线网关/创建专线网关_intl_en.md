This document describes how to create a direct connect gateway and provides information on the inbound route.

## Prerequisites

- You have applied for a connection as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).
- You have built a VPC as instructed in [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).

## Directions

1. Log in to the [Direct Connect Gateway console](https://console.cloud.tencent.com/vpc/dcgw?rid=1).
2. Select a region and VPC at the top of the **Direct Connect Gateway** page, and click **+New**.
   ![](https://main.qcloudimg.com/raw/5f14dab7972ba2d2843006343b3e15bb.png)
3. Complete the configurations in the pop-up window and click **OK**.
   ![](https://main.qcloudimg.com/raw/7c06c736d44895861856e86ec3820504.png)	 

<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Name</td>
<td>The name of your direct connect gateway</td>
</tr>
<tr>
<td>Associate Network</td>
<td>Select either CCN or VPC.</td>
</tr>
<tr>
<td>CCN instance</td>
<td>A CCN instance is needed if **CCN** is selected for the **Associate Network**. This field can also be left empty.</td>
</tr>
<tr>
<td>Network</td>
<td>A VPC instance is needed if **VPC** is selected for the **Associate Network**.</td>
</tr>
<tr>
<td>Gateway Type</td>
<td>A gateway is needed if **VPC** is selected for the **Associate Network*.<ul><li>Standard: does not support the network address translation feature.</li><li>NAT: supports the network address translation feature.</li></ul></td>
</tr>
</table>

## Inbound Routes

As shown in the Direct Connect network architecture, both the creation time of the direct connect gateway and dedicated tunnel mode will affect the destination IP range of the inbound route (from your IDC to a Tencent Cloud VPC). For more information, please see [Direct Connect Gateway Overview](https://intl.cloud.tencent.com/document/product/216/38746).

<table>
 <thead>
  <td>Gateway Type</td>
  <td>Creation Time</td>
  <td>Dedicated Tunnel Mode</td>
  <td>IDC Route to Tencent Cloud</td>
 </thead>
 <tbody>
 <tr>
  <td rowspan="2">VPC-based direct connect gateway</td>
  <td rowspan="2">No limit</td>
  <td>Static</td>
  <td>The inbound routing policy is configured in the local router.</td>
 </tr>
 <tr>
  <td>BGP</td>
  <td>The IDC automatically obtains the VPC CIDR block based on the BGP protocol.</td>
 </tr>
 <tr>
  <td rowspan="4">CCN-based direct connect gateway</td>
  <td rowspan="2" >Before 00:00:00 on September 15, 2020
  </td>
  <td>Static</td>
  <td>The inbound routing policy is configured in the local router.</td>
 </tr>
 <tr>
  <td>BGP</td>
  <td>The IDC automatically obtains the subnet CIDR block based on the BGP protocol.</td>
 </tr>
 <tr>
  <td rowspan="2" >After 00:00:00 on September 15, 2020</td>
  <td>Static</td>
  <td>The inbound routing policy is configured in the local router.</td>
 </tr>
 <tr>
  <td>BGP</td>
  <td>The IDC automatically obtains the VPC CIDR block based on the BGP protocol.</td>
</tbody></table>



