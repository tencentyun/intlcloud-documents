This document describes how to create a direct connect gateway and provides information on the inbound route.

## Prerequisites
- Apply for a connection. For more information, see [Applying for a Connection](https://intl.cloud.tencent.com/document/product/216/19244).
- If you want to use VPC, set up a VPC. For more information, see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).
- If you want to use CCN, set up a CCN instance. For more information, see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
- If you want to use NAT Direct Connect Gateway, create a VPC NAT gateway.
>?NAT Direct Connect Gateway is available only for users who are added to the corresponding allowlist. To use the feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). For more information about the comparison between the old and new methods for configuring the mapping parameters of NAT Direct Connect Gateway, see [Overview](https://intl.cloud.tencent.com/document/product/216/38746).



## Use Limits
A standard direct connect gateway supports propagating secondary CIDR blocks. Note the following limits:
- Up to 10 secondary CIDR blocks can be propagated.
- This feature is unavailable to a NAT direct connect gateway.


## Directions
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc), and click **Direct connect gateway** in the left sidebar.
2. Select a region and VPC at the top of the **Direct connect gateway** page, and click **+ New**.
![](https://main.qcloudimg.com/raw/89ddf380778948849f709ba4518198db.png)
3. Specify gateway parameters in the pop-up window and click **OK**.
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
<td>Select the AZ.</td>
</tr>
<tr>
<td>Associated Network</td>
<td>Select the type of the direct connect gateway. Valid values: CCN, VPC, and NAT.</td>
</tr>
<tr>
<td>Network</td>
<td>Select an instance to which the created direct connect gateway associate based on the selected network type.</td>
</tr>
<tr>
<td>Gateway type</td>
<td><ul><li>If `VPC` is selected for **Associated Network**, the network address translation feature is not supported.</li><li>If `NAT` is selected for **Associated Network**, the network address translation feature is supported and you need to configure the translation rules for the NAT gateway.</li></ul></td>
</tr>
</table>

## Inbound Routes
The destination of the inbound routes (from your IDC to a Tencent Cloud VPC) are affected by both the creation time of the direct connect gateway and dedicated tunnel mode. For more information, see [Direct Connect Gateway Overview](https://www.tencentcloud.com/document/product/216/38746).
<table>
 <thead>
  <td>Gateway type</td>
  <td>Creation Time</td>
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
</tr>
<tr>
<td rowspan="2">NAT direct connect gateway</td>
<td rowspan="2">No limit</td>
<td>Static</td>
<td>The inbound routing rule is configured in the local router.
The next hop of the VPC route must point to a VPC NAT gateway.
</td>
</tr>
<tr>
<td>BGP</td>
<td>The next hop of the VPC route must point to a VPC NAT gateway.</td>
</tr>
</tbody></table>



## Related Operations
- After creating a CCN-based direct connect gateway, you need to add IDC IP ranges to the direct connect gateway to implement network communication. For more information, see [Publishing IDC IP Ranges to CCN](https://intl.cloud.tencent.com/document/product/216/39083).
- After creating a VPC-based direct connect gateway, you need to configure the VPC route table to implement network communication. For more information, see [Configuring the Route Table](https://www.tencentcloud.com/document/product/216/19259).
