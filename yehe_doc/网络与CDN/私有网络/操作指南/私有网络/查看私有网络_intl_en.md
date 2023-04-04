You can query all VPC resources via the VPC console, such as cloud resources and connections in a VPC.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page. You can check the information of all VPC in this region in the list.

<table>
<tr>
<th width="15%">Column</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>ID/Name</td>
<td>The ID and name of the VPC. The name can be modified.</td>
</tr>
<tr>
<td>IPv4 CIDR Block</td>
<td>The IPv4 CIDR block of the VPC. It cannot be modified.</td>
</tr>
<tr>
<td>IPv6 CIDR block</td>
<td>The IPv6 CIDR block of the VPC. This feature is currently in beta. To use it, please <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1">submit a ticket</a>.</td>
</tr>
<tr>
<td>Subnet</td>
<td>The number of subnets in the VPC. Click the number to access the <b>Subnet</b> page.</td>
</tr>
<tr>
<td>Route Table</td>
<td>The number of route tables in the VPC. Click the number to access the <b>Route Table</b> page.</td>
</tr>
<tr>
<td>NAT Gateway</td>
<td>The number of NAT Gateways in the VPC. Click the number to access the <b>NAT Gateway</b> page.</td>
</tr>
<tr>
<td>VPN Gateway</td>
<td>The number of VPN gateways in the VPC. Click the number to access the <b>VPN Gateway</b> page.</td>
</tr>
<tr>
<td>CVM</td>
<td>The number of CVMs in the VPC. Click the number to access the CVM page. Click the CVM icon to redirect to the CVM purchase page.</td>
</tr>
<tr>
<td>Direct Connect Gateway</td>
<td>The number of direct connect gateways in the VPC. Click the number to access the Direct Connect Gateway page.</td>
</tr>
<tr>
<td>Default VPC</td>
<td>Indicates whether the VPC is the default VPC of the region. There can only be one default VPC in a region. The default VPC is automatically created when you purchase resources like CVM. It works the same as the manually-created ones.</td>
</tr>
<tr>
<td>Creation Time</td>
<td>The time when the VPC was created.</td>
</tr>
<tr>
<td>Operation</td>
<td>The supported operations of the VPC. Only a VPC without any resource can be deleted. You can click <b>More</b> to edit IPv4 CIDR block and IPv6 CIDR block if applicable.</td>
</tr>
</table>

3. Click the VPC ID to view details, including the basic information, CCN association, and associated resources. Click the number next to a resource to access the resource management page.

4. Return to the VPC list, and click in the top-right corner search box to filter VPC by different resource attributes.

5. Click the setting icon in the upper-right corner to customize display columns.
