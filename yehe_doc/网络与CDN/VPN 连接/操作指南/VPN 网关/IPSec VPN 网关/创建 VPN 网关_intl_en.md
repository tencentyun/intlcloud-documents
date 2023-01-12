A VPN gateway is a VPN connection instance. Therefore, please create an IPsec VPN gateway before using a VPN connection to securely access the Tencent Cloud Virtual Private Cloud (VPC) from external networks. This document shows you how to create a VPN gateway in the console.

## Prerequisites
To create a VPC-based VPN gateway, you need to create a VPC in the same region as the VPN gateway first. For more information, see [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN Gateway** in the left directory to enter the admin page.
3. Click **+New**.
4. Configure the following gateway parameters in the pop-up window.
>?
>- Only new gateways but not existing gateways are supported on 200 Mbps, 500 Mbps, 1,000 Mbps and 3,000 Mbps bandwidths.
>- If the VPN gateway uses 200 Mbps, 500 Mbps, 1,000 Mbps or 3,000 Mbps bandwidths, AES128+MD5 is recommended for VPN tunnel encryption.
>
![]()
<table>
<tr>
<th>Parameter Name</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway Name</td>
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
<td>Set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios.
</td>
</tr>
<tr>
<td>Associated Network</td>
<td>This parameter indicates whether you create a CCN-based VPN/VPN gateway or a VPC-based VPN/VPN gateway.<ul><li>If you want to use a VPN connection to implement the interconnection with multiple VPCs or other Direct Connect networks, please create the <b>CCN</b> based VPN.
<dx-alert infotype="notice" title="">
You cannot associate the CCN-based VPN gateway with a CCN instance during its creation. You can associate a created VPN gateway to a CCN instance in the gateway details page. If you create a policy-based VPN tunnel, you also need to enable the route published to the CCN in the IDC IP range of the VPN gateway.
</dx-alert>
</li><li>If you want to communicate with a single VPC through a VPN connection, please create a <b>VPC</b> based VPN.</li></ul></td>
</tr>
<tr>
<td>Network</td>
<td>Specify the VPC to be associated with the VPN gateway only when the associated network is <b>VPC</b>.</td>
</tr>
<tr>
<td>Tag</td>
<td>Tags mark VPN gateway resources so that these resources can be queried and managed efficiently. Tag is not a required configuration. You can decide whether to configure it according to your demand.</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>Bill-by-traffic mode is supported. This billing mode is applicable to scenarios with significant bandwidth fluctuations.</td>
</tr>
</table>
5. After completing the gateway parameter settings, click <b>Create</b>, and the <b>Status</b> of the gateway is <b>Creating</b>. In 1 to 2 minutes after the gateway is successfully created, the status turns to <b>Running</b>, and the system assigns a public IP to the VPN gateway.
<img src="">

