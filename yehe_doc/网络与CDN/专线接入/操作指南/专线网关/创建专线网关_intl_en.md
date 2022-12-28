This document describes how to create a direct connect gateway and provides information on the inbound route.

## Prerequisites
- Apply for a connection. See [Applying for a Connection](https://intl.cloud.tencent.com/document/product/216/19244).
- Set up a VPC. See [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).

## Use Limits
A standard direct connect gateway supports propagating secondary CIDR blocks. Note the following limits:
- Up to 10 secondary CIDR blocks can be propagated.
- This feature is unavailable to a NAT direct connect gateway.


## Directions
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc), and click **Direct Connect Gateway** in the left sidebar.
2. Select a region and VPC at the top of the **Direct Connect Gateway** page, and click **+ New**.
![](https://main.qcloudimg.com/raw/89ddf380778948849f709ba4518198db.png)
3. Complete the configurations in the pop-up window and click **OK**.
![](https://main.qcloudimg.com/raw/d74dd96faabff1924720444e732330a9.png)
<table>
<tr>
<th width="15%">Field</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Name</td>
<td>Enter a name for the direct connect gateway.</td>
</tr>
<tr>
<td>AZ</td>
<td>Select the AZ</td>
</tr>
<tr>
<td>Associated Network</td>
<td>Select either <b>CCN</b> or <b>VPC</b>.</td>
</tr>
<tr>
<td>Network</td>
<td>A VPC instance is needed if <b>VPC</b> is selected for the <b>Associate Network</b>.</td>
</tr>
<tr>
<td>Gateway type</td>
<td>A gateway is needed if <b>VPC</b> is selected for the <b>Associate Network</b>.<ul><li>Standard: does not support the network address translation feature.</li><li>NAT Type: supports the network address translation feature.</li></ul></td>
</tr>
</table>

## Inbound Routes
The destination of the inbound routes (from your IDC to a Tencent Cloud VPC) are affected by both the creation time of the direct connect gateway and dedicated tunnel mode. For more information, see [Direct Connect Gateway Overview](https://intl.cloud.tencent.com/document/product/216/38746).
<table>
 <thead>
  <td>Gateway type</td>
  <td>Creation time</td>
  <td>Dedicated Tunnel Mode</td>
  <td>IDC Routes to Tencent Cloud</td>
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
  <td rowspan="2">After 00:00:00 on September 15, 2020</td>
  <td>Static</td>
  <td>The inbound routing policy is configured in the local router.</td>
 </tr>
 <tr>
  <td>BGP</td>
  <td>The IDC automatically obtains the VPC CIDR block based on the BGP protocol.</td>
</tbody></table>

## Related Operations
- After creating a CCN-based direct connect gateway, you need to add IDC IP ranges to the direct connect gateway to implement network communication. For more information, see [Publishing IDC IP Ranges to CCN](https://intl.cloud.tencent.com/document/product/216/39083).
- After creating a VPC-based direct connect gateway, you need to configure the VPC route table to implement network communication. For more information, see [Configuring the Route Table](https://intl.cloud.tencent.com/document/product/216/19259).
