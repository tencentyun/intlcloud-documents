A route table is used to control the outbound traffic of the subnet. It can contain multiple routing policies There are default route table and custom route tables. The default route table (local route) allows private network interconnection in the VPC, which cannot be deleted, but can be configured with routing policies the same way as you configure a custom route table. This document describes how to create and configure a custom route table.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Route Tables** on the left sidebar to access the management page.
3. Click **+ New**.
4. In the pop-up dialog, enter the route table name, select the VPC to which the route table belongs, and configure the routing policies.
    ![](https://main.qcloudimg.com/raw/9016a7369ffa96c05e00843602a54192.png)
    
	>? You can configure routing policies when creating a route table. Alternatively, after a route table is created, you can click the route table ID to enter the **Basic Information** page and click **+ New routing policies** to configure routing policies.
	>

	Configuring a routing policy [](id:routeParam):

<table><tbody>
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td>Destination</td><td>The destination IP range to which the traffic is forwarded. The configuration should meet the following requirements:
  <ul><li>Enter an IP range. If you want to enter a single IP, set the mask to 32 (for example, `172.16.1.1/32`).</li>
	<li>The destination cannot be an IP range of the VPC where the route table resides, because the local route already allows private network interconnection in this VPC.</li></ul>
	<p><b>Note:</b> If you have deployed a <a href="https://intl.cloud.tencent.com/document/product/457/6759">TKE service</a> in the VPC, the destination you configure in the route table policy of VPC subnet cannot fall within the VPC CIDR block or contain the TKE IP range. For example, if the VPC CIDR block is `172.168.0.0/16` and the TKE CIDR block is `192.168.0.0/16`, the destination IP range should not fall within `172.168.0.0/16`, or contain `192.168.0.0/16` when you configure routing policy for a VPC subnet.</note></td></tr>
<tr><td>Next hop type</td><td>The egress of the VPC data packets. The following types are supported:
 <ul>
<li> NAT Gateway: the traffic directed to a destination IP range is forwarded to a NAT Gateway.</li>
<li>Peering Connections: the traffic directed to a destination IP range is forwarded to a VPC on the other side of a peering connection.</li>
<li>Direct Connect Gateway: the traffic directed to a destination IP range is forwarded to a direct connect gateway.</li>
<li>High Availability Virtual IP: the traffic directed to a destination IP range is forwarded to a HAVIP.</li>
<li>VPN Gateway: the traffic directed to a destination IP range is forwarded to a VPN gateway.</li>
<li>Public IP of CVM: the traffic directed to a destination IP range is forwarded to the public IP (including EIPs) of a CVM instance in a VPC.</li>
<li>CVM: the traffic directed to a destination IP range is forwarded to a CVM instance in a VPC.</li>
</ul>
</td></tr>
<tr><td>Next hop</td><td>Specifies the next hop instance to which the traffic is redirected, such as the gateway or CVM IP.</td></tr>
<tr><td>Notes</td><td>Describes the purpose of the route for resource management. This parameter is optional.</td></tr>
<tr><td>Add a line</td><td>: configures multiple routing policies if needed. You can click the deletion icon in the **Operation** column to delete the unnecessary routing policies. A custom route table should contain at least one routing policy.</td></tr>
</tbody> 
</table>

5. After completing the configurations, click **Create**. Then the route table will be displayed in the list.
![](https://main.qcloudimg.com/raw/2cd194721906f97ff3c878b8a64a4341.png)

## Configuring HAVIP
Currently, only the routing policies whose **Next hop type** is **High Availability Virtual IP**, **VPN Gateway**, or **CVM** in the default or custom route tables can be manually published to or withdrawn from CCN.
1. Click the route table ID to enter the details page.
    ![](https://main.qcloudimg.com/raw/db9290e78cfc13b9575e590a0f3fa680.png)
2. You can perform the following operations as needed:
    + Click **Publish to CCN** to publish an enabled routing policy to CCN.
    + Click **Withdraw from CCN** to withdraw a custom routing policy that has been published to CCN.
    + Click **Edit** to modify the routing policy.
    + Click **Delete** to delete a disabled routing policy.
