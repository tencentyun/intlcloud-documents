>?The VPN route table is currently in a beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Prerequisites
Make sure the VPN gateway, customer gateway and VPN tunnel have been configured before configuring the route table.

## Operation Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Gateway** on the left navigation bar.
3. On the “VPN Gateway” page, select the region and VPC, and click the VPN gateway instance ID to go to the details page.
4. Click the **Route Table** tab on the “Instance Details” page.
5. Click **Add Routing** and configure routing policies.
<table>
<tr>
<th>Configuration Item</th>
<th>Note</th>
</tr>
<tr>
<td>Destination Port</td>
<td>Enter the private network IP range of the peer network to be accessed.</td>
</tr>
<tr>
<td>Next Hop Type</td>
<td>VPN tunnel.<p>Note: In terms of a VPN gateway for CCN, if the VPN gateway is associated with the CCN, you also need to add next hop to the routing policies in <b>CCN</b>.</td>
</tr>
<tr>
<td>Next Hop</td>
<td>Select a VPN tunnel that has been created.</td>
</tr>
<tr>
<td>Weight</td>
<td>Choose the weighted values of VPN tunnels:<ul><li>0: high priority</li><li>100: low priority</li></ul></td>
</tr>
<tr>
<td>New Line</td>
<td>Multiple routing policies can be added.</td>
</tr>
<tr>
<td>Delete</td>
<td>Routing policies can be deleted, except for the last one.</td>
</tr>
</table>
6. Click **Confirm** after configuring routing policies.
7. Other executable operations.
    1. Enabling or disabling routing policies.
    2. Disabled routing policies can be deleted.
