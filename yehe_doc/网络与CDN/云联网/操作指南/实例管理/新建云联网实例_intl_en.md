CCN connects a VPC with another or with IDCs. This document describes how to create a CCN instance.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Cloud Connect Network** on the left sidebar.
2. Click **+New** at the top of the **CCN** page. 
3. Complete the following configurations in the **Create CCN instance** pop-up window.
![](https://main.qcloudimg.com/raw/b72cc7c286f94d8b958def554dfc0150.png)
<table>
<thead>
<tr>
 <th >Field</th>
 <th >Subfield</th>
 <th >Description</th>
</tr>
 </thead>
<tr>
 <td align="center">Name</td>
	<td align="center">-</td>
 <td >Name of the CCN instance</td>
</tr>
<tr >
 <td align="center" >Billing Mode</td>
 <td align="center" style='white-space:nowrap'>Pay-as-you-go by monthly 95 percentile</td>
 <td>Bill the actual bandwidth usage of the current month on 95th percentile basis. It's applicable to business with fluctuating bandwidth demands.</td>
</tr>
<tr>
 <td rowspan=3 align="center">Service Level</td>
 <td align="center">Platinum</td>
 <td>It’s ideal for key businesses that require extremely high communication quality, such as payment.</td>
</tr>
<tr>
 <td align="center" white-space="nowrap">Gold</td>
 <td >It’s suitable for businesses that require high communication quality, such as game acceleration.</td>
</tr>
<tr >
 <td align="center">Silver</td>
 <td >It’s suitable for cost-sensitive and jitter-insensitive businesses, such as data backup.</td>
</tr>
<tr>
 <td rowspan=2>Bandwidth Limit Mode</td>
 <td align="center" style='white-space:nowrap'>Regional Outbound Bandwidth Cap</td>
 <td>The total outbound bandwidth cap from a single region to other regions</td>
</tr>
<tr>
	<td align="center" style='white-space:nowrap'>Inter-region Bandwidth Cap</td>
 <td>The inbound and outbound bandwidth cap between two regions</td>
</tr>
<tr>
 <td   align="center">Associated Instances</td>
 <td   align="center">-</td>
 <td >The options include VPC, Direct Connect Gateway, BM Virtual Private Cloud, and VPN Gateway. 
 If there is no available instance, you can directly create a CCN instance and associate a network instance later. You can optionally enter the description for the CCN instance.
</tr>
</table>
4. Click **OK**.

## Subsequent Operations
After creating a CCN instance, you need to associate network instances with it, check its route table, and configure the bandwidth to enable interconnection.
- For more information on how to associate network instances, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
- For more information on how to check whether the routing policies of each subnet in the VPC associated with the CCN take effect, see [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).
- For pay-as-you-go CCN instances billed by monthly 95th percentile, you can configure a cross-region bandwidth cap as needed to control the bandwidth cost. For detailed directions, see [Configuring Bandwidth](https://intl.cloud.tencent.com/document/product/1003/38894).

