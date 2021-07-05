## Prerequisites
You have completed the configurations of VPN gateway, customer gateway and VPN tunnel before configuring a routing policy.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Gateway** on the left sidebar.
3. On the **VPN Gateway** page, select the target region and VPC, and click the **ID/Name** of the VPN gateway to go to its details page.
4. Click the **Route Table** tab.
5. Click **Add a route** and configure routing policies.
<table>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
<tr>
<td>Destination</td>
<td>Enter the IP range of the network to access.</td>
</tr>
<tr>
<td>Next hop type</td>
<td>Select <b>VPN tunnel</b> or <b>CCN</b>.<p>Note: if the VPN gateway for CCN is associates with a CCN instance, the routing policy with <b>CCN</b> as the next hop will be automatically obtained and displayed in the route table. Do not manually configure it.</td>
</tr>
<tr>
<td>Next hop</td>
<td>Select the instance ID of the next hop.<ul><li>If you select <b>VPN tunnel</b> for the <b>Next hop type</b>, select a VPN tunnel that has been created.</li><li>If you select <b>CCN</b> for the <b>Next hop type</b>, the CCN instance associated with the VPN gateway will be automatically displayed.</li></ul></td>
</tr>
<tr>
<td>Weight</td>
<td>Choose the weighted values of VPN tunnels:<ul><li>0: high priority</li><li>100: low priority</li></ul></td>
</tr>
<tr>
<td>Add a line</td>
<td>Configure multiple routing policies as needed.</td>
</tr>
<tr>
<td>Delete</td>
<td>Delete the routing policies, except for the last one.</td>
</tr>
</table>
6. Click **OK**.
7. Perform other operations as needed.
    1. Enable or disable routing policies.
    2. Delete the disabled routing policies.
