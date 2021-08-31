Tencent Cloud will upgrade the authentication feature for certain APIs of the VPN connection on July 29, 2021 at 00:00:00 (Beijing time). After the upgrade, the root account should [grant sub-users the policy permission](#cam) to use the upgraded APIs, or the API calls may fail.

## Related APIs
<table>
<tr >
<td colspan=2>API Name</td><td>Description</td></tr>
<tr>
<td rowspan=5>GET</td>
<td><a href="https://intl.cloud.tencent.com/document/api/215/41055">DescribeVpnGatewayRoutes</a></td>
<td>Queries routes of a VPN gateway</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/215/36075">DescribeVpnGatewayCcnRoutes</a></td>
<td>Queries VPN gateway-based CCN routes</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/215/17515">DescribeVpnConnections</a></td>
<td>Queries the VPN tunnel list
</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/215/17516">DescribeCustomerGateways</a></td>
<td>Queries customer gateways
</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/215/17513">DownloadCustomerGatewayConfiguration</a></td><td>Downloads a VPN tunnel configuration
</td>
</tr>
<tr>
<td rowspan= 4>POST</td>
<td><a href="https://intl.cloud.tencent.com/document/api/215/41056">DeleteVpnGatewayRoutes</a></td>
<td>Deletes routes of a VPN gateway
</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/api/215/41054">ModifyVpnGatewayRoutes</a></td>
<td>Modifies the route status of a VPN gateway
</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/215/41057">CreateVpnGatewayRoutes</a></td><td>Creates routes of a VPN gateway
</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/215/36074">ModifyVpnGatewayCcnRoutes</a></td><td>Modifies VPN gateway-based CCN routes
</td>
</tr>
</table>

## Granting Sub-accounts the Policy Permission[](id:cam)
Please complete the policy authorization for your sub-users as instructed below to prevent failed calls to the upgraded APIs.
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Policies** on the left sidebar to access the **Policy** page.
3. Click **All Policies**.
4. Locate the target policy to authorize sub-users, and click **Associated Users/Groups** under the **Operation** column on the right.
5. [](id:step4)In the pop-up window, select target users from the box on the left to the **Selected** box on the right, and click **Confirm**.
6. (Optional) if you need to associate a user group, please click **Switch to User Groups** > **User Group** in the pop-up window, and repeat the operations in <a href="#step4">step 5</a>.

