This document describes how to purchase NAT gateways in the NAT Gateway console.

## Directions
1. Log in to the [**NAT Gateway console**](https://console.cloud.tencent.com/vpc/nat?fromNav).
2. Select a region and VPC, and then click **Create**.
3. In the NAT gateway purchase page, complete the parameters and purchase.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Gateway name</td>
<td>Enter the NAT gateway name with up to 60 characters.</td>
</tr>
<tr>
<td>Region</td>
<td>Select a region for the NAT gateway.</td>
</tr>
<tr>
<td>VPC</td>
<td>Select a VPC for the NAT gateway.</td>
</tr>
<tr>
<td>Gateway type</td>
<td>The types include: <ul><li>Small (a maximum of 1,000,000 connections)</li><li>Medium (a maximum of 3,000,000 connections)</li><li>large (a maximum of 10,000,000 connections)</li></ul></td>
</tr>
<tr>
<td>Outbound bandwidth cap</td>
<td>The maximum outbound bandwidth cap of the NAT gateway. Valid values: 10, 20, 50, 100, 200, 500, 1000, 2000 and 5000. Unit: Mbps.</td>
</tr>
<tr>
<td>EIP configuration</td>
<td>You can associate the NAT gateway with <strong>existing EIPs</strong> or <strong>create new EIPs</strong> for it.<ul><li>Using existing EIPs: Make sure that you have idle EIPs in the same region as the NAT gateway. </li><li>Creating new EIPs: Bill-by-traffic general BGP IPs are created automatically. You can configure the EIP quantity and the bandwidth cap as needed.</li></ul></td>
</tr>
</tbody></table>
>?	
>- The traffic going to the internet is limited by the bandwidth cap of both the NAT gateway and EIPs. The smaller bandwidth cap prevails. 
>- For more information about NAT gateway-related operations, see [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251).
