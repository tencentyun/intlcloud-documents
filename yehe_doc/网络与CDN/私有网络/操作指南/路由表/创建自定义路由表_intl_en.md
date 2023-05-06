A route table consisting of multiple routing policies is used to control the outbound traffic of the subnet. There are default route table and custom route tables. The default route table (local route) allows private network interconnection in the VPC, which cannot be deleted, but can be configured with routing policies the same way as you configure a custom route table. This document describes how to create and configure a custom route table.
## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Route table** in the left sidebar to go to the route table management page.
3. Click **Create Policy**.
4. In the pop-up window, enter the route table name, select the VPC to which the route table belongs, and configure a routing policy.
![](https://main.qcloudimg.com/raw/8d001c82ce2c4ada7fba9a723a2b4e0c.png)
>? You can configure routing policies when creating a route table. Alternatively, after a route table is created, you can click the route table ID to go to the details page of the route table and click **+ Add routing policies** to configure routing policies.
>
Configuring a routing policy [](id:routeParam):
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Destination</td>
<td>Specify the destination IP range to which you want to forward traffic. Configure it as follows:
<ul>
<li>Enter an IP range. If you want to enter a single IP, set the mask to 32 (for example, `172.16.1.1/32`).</li>
<li>The destination cannot be an IP range of the VPC where the route table resides, because the local route already allows private network interconnection in this VPC.</li>
</ul>
<dx-alert infotype="explain" title="">
If you have deployed a <a href="https://intl.cloud.tencent.com/document/product/457/6759">TKE service</a> in the VPC, when you configure the routing policy of the route table for the VPC subnet, the destination cannot be within the CIDR block range of the VPC, nor can it contain the container IP range. For example, if a VPC CIDR block is `172.168.0.0/16` and the container network CIDR block is `192.168.0.0/16`, when you configure the routing policy for the VPC subnet, the destination IP range cannot be in the range of `172.168.0.0/16`, and cannot contain `192.168.0.0/16`.
</dx-alert>
</td>
</tr>
<tr>
<td>Next hop type</td><td>Indicates the egress of data packets for the VPC. Supported types:
<ul>
<li> NAT Gateway: the traffic directed to a destination IP range is forwarded to a NAT Gateway.</li>
<li>Peering connections: The traffic directed to a destination IP range is forwarded to the VPC peer of a peering connection.</li>
<li>Direct Connect Gateway: the traffic directed to a destination IP range is forwarded to a direct connect gateway.</li>
<li>High Availability Virtual IP: the traffic directed to a destination IP range is forwarded to an HAVIP.</li>
<li>VPN Gateway: the traffic directed to a destination IP range is forwarded to a VPN gateway.</li>
<li>Public IP of CVM: the traffic directed to a destination IP range is forwarded to the public IP (including EIPs) of a CVM instance in the VPC.</li>
<li>CVM: the traffic directed to a destination IP range is forwarded to a CVM instance in the VPC.</li>
<li>CDC local gateway: Tencent Cloud CDC communicates with the customer IDC by using a CDC local gateway.</li>
</ul>
</td>
</tr>
<tr>
<td>Next hop</td><td>Specify the next hop instance to which the traffic is redirected, such as a gateway or CVM IP.</td>
</tr>
<tr>
<td>Notes</td>
<td>Enter the route description for resource management. This parameter is optional.</td>
</tr>
<tr>
<td>New Line</td>
<td>You can click <b>+ New line</b> to configure multiple routing policies, or click the deletion icon in the <b>Operation</b> column to delete the unnecessary routing policies. A custom route table should contain at least one routing policy.</td>
</tr>
</tbody>
</table>
5. After completing the configurations, click **Create**. Then the route table will be displayed in the list.
![](https://main.qcloudimg.com/raw/c0e5611a3c21733e454ea0e7b8eb4430.png)

## Related Operations
Routing policies whose **Next hop type** is **High availability virtual IP** or **CVM** in the default or custom route tables can be manually published to or withdrawn from CCN.
1. Click the route table ID to enter the details page.
![](https://main.qcloudimg.com/raw/7f74257af9225a09dbbf3d2f2366c779.png)
2. You can perform the following operations as needed:
    + Click **Publish to CCN** to publish an enabled routing policy to CCN.
    + Click **Withdraw from CCN** to withdraw a custom routing policy that has been published to CCN.
    + Click **Edit** to modify a routing policy.
    + Click **Delete** to delete a disabled routing policy.
