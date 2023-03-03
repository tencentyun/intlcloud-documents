An SSL VPN gateway works as the egress of an SSL VPN connection on the VPC side. It helps establish the secure and reliable encrypted network communication between Tencent Cloud VPC and mobile clients.

## Prerequisites
You've created a VPC. See [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN Gateway** in the left directory to enter the admin page.
3. Click **+New**.
4. Configure the following gateway parameters in the pop-up window.
<table>
<tr>
<th width="12%">Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway name</td>
<td>Enter the VPN gateway name (up to 60 characters)</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the VPN gateway</td>
</tr>
<tr>
<td>AZ</td>
<td>Select the availability zone of the current gateway</td>
</tr>
<tr>
<td>Protocol Type</td>
<td>IPSec and SSL protocols are supported.</td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios.</td>
</tr>
<tr>
<td>Associated Network</td>
<td><ul><li>This parameter specifies whether you create a CCN-based VPN/VPN gateway or a VPC-based VPN/VPN gateway. If you want to use a VPN connection to enable interconnection with multiple VPCs or other Direct Connect networks, create a <b>CCN</b>-based VPN.</li>
<dx-alert infotype="notice" title="">
You cannot associate the CCN-based VPN gateway with a CCN instance during its creation. You can associate a created VPN gateway to a CCN instance in the gateway details page. If you create a policy-based VPN tunnel, you also need to enable the route published to the CCN in the IDC IP range of the VPN gateway.
</dx-alert>
<li>If you want to communicate with a single VPC by using a VPN connection, create a <b>VPC</b>-based VPN.</li></ul></td>
</tr>
<tr>
<td>Network</td>
<td>If you set <b>Associated Network</b> to <b>VPC</b>, you must select the VPC that you want to associate with the VPN gateway.
After you create a gateway for a CCN instance, you must associate the created gateway with the CCN instance on the details page. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1037/46429">Associating a CCN instance</a>.</td>
</tr>
<tr>
<td>SSL VPN Connections</td>
<td>If you select <b>SSL</b> for <b>Protocol type</b>, you must configure this parameter. The number of supported VPN connections vary based on the gateway. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1037/32682">Use Limits</a>.</td>
</tr>
<tr>
<td>Tag</td>
<td>Tags mark VPN gateway resources so that these resources can be queried and managed efficiently. Tag is not a required configuration. You can decide whether to configure it according to your demand.</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>The SSL VPN gateway supports only the pay-as-you-go billing mode.</td>
</tr>
</table>
5. Click <b>Create</b>.
